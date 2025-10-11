# Configuration Architecture Guide

This guide documents the configuration system architecture used in this project, featuring a clean separation of concerns between schema definitions and configuration logic.

## Overview

The configuration system is split into two main files:
- `schemas.ts` - Pure schema definitions and type exports
- `config.ts` - Configuration logic using the 4-pillar pattern

This separation provides better maintainability, reusability, and follows single responsibility principle.

## Architecture Benefits

### Before Refactoring
- Single 571-line file mixing schema definitions and configuration logic
- Difficult to maintain and understand
- Schema changes required touching configuration code
- Poor separation of concerns

### After Refactoring
- `schemas.ts`: 247 lines focused purely on schema definitions
- `config.ts`: 401 lines (30% reduction) focused on configuration logic
- Clear separation of concerns
- Better maintainability and reusability
- Independent evolution of schemas and configuration

## File Structure

```
├── schemas.ts          # Schema definitions and types
├── config.ts           # Configuration logic and initialization
└── guides/
    └── CONFIGURATION_ARCHITECTURE.md  # This guide
```

## Import Strategy

The configuration system uses clean imports with proper TypeScript support:

```typescript
// config.ts imports from schemas.ts
import {
  ConfigSchema,
  SchemaRegistry,
  type Config,
  type ServerConfig,
  type BrowserConfig,
  // ... other types
} from "./schemas";
```

### Bun vs Node.js Import Differences

- **Bun**: Can import `.ts` files directly: `from "./schemas"`
- **Node.js ES modules**: Requires `.js` extension: `from "./schemas.js"`

This project uses Bun, so we use the simpler `.ts` import syntax.

## Key Design Principles

1. **Separation of Concerns**: Schemas are independent of configuration logic
2. **Type Safety**: All schemas generate TypeScript types automatically
3. **Reusability**: Schemas can be imported by other modules independently
4. **Maintainability**: Changes to schemas don't affect configuration logic
5. **Single Source of Truth**: Schema registry provides centralized access

## Usage Examples

### Importing Specific Schemas
```typescript
import { ServerConfigSchema, type ServerConfig } from "./schemas";
```

### Importing Configuration
```typescript
import { config, type Config } from "./config";
```

### Accessing Schema Registry
```typescript
import { SchemaRegistry } from "./schemas";

// Access any schema
const serverSchema = SchemaRegistry.Server;
const configSchema = SchemaRegistry.Config;
```

## Next Steps

For detailed information about each file:
- Schema organization: See [schemas.ts structure documentation](#schemas-structure)
- Configuration pattern: See [config.ts 4-pillar pattern documentation](#config-structure)

---

## Schemas Structure

The `schemas.ts` file is organized into logical sections with clear hierarchy and exports.

### File Organization

#### 1. Basic Enums
Foundation enums for configuration options:
```typescript
export const EnvironmentType = z.enum(["development", "staging", "production", "test"]);
export const ScreenshotMode = z.enum(["on", "off", "only-on-failure"]);
export const VideoMode = z.enum(["on", "off", "retain-on-failure"]);
export const TraceMode = z.enum(["on", "off", "retain-on-failure"]);
```

#### 2. Format Functions
Reusable Zod validators using v4 format functions:
```typescript
export const HttpsUrl = z.url();
export const PositiveInt = z.int32().min(1);
export const FileSizeBytes = z.int32().min(1);
export const Milliseconds = z.int32().min(0);
```

#### 3. Complex Validators
Custom validation logic with detailed error messages:
```typescript
export const DirectoryPath = z
  .string()
  .refine(
    (val) => val.startsWith("./") || val.startsWith("/") || val.startsWith("../"),
    { message: "Directory path must be relative (./) or absolute (/)" }
  );

export const MimeType = z.string().superRefine((val, ctx) => {
  const mimePattern = /^[a-z]+\/[a-z0-9.+-]+$/i;
  if (!mimePattern.test(val)) {
    ctx.addIssue({
      code: "custom",
      message: "Invalid MIME type format",
    });
  }
});
```

#### 4. Configuration Schemas
Main configuration object schemas:
```typescript
export const ServerConfigSchema = z.strictObject({
  baseUrl: HttpsUrl,
  screenshotDir: DirectoryPath,
  downloadsDir: DirectoryPath,
  // ... other fields
});
```

#### 5. Main Configuration Schema
Root schema with cross-field validation:
```typescript
export const ConfigSchema = z
  .strictObject({
    server: ServerConfigSchema,
    browser: BrowserConfigSchema,
    allowedDownloads: DownloadConfigSchema,
  })
  .superRefine((data, ctx) => {
    // Cross-field validation logic
  });
```

#### 6. Application-Specific Schemas
Domain-specific schemas for reports and analytics:
```typescript
export const BrokenLinksReportSchema = z.object({
  reportDate: z.iso.datetime({ offset: true }),
  baseUrl: z.url(),
  totalBrokenLinks: z.number().int().nonnegative(),
  // ... other fields
});
```

#### 7. Schema Registry
Centralized access to all schemas:
```typescript
export const SchemaRegistry = {
  Server: ServerConfigSchema,
  Browser: BrowserConfigSchema,
  Config: ConfigSchema,
  // ... all schemas
} as const;
```

#### 8. Type Definitions
Automatically generated TypeScript types:
```typescript
export type Config = z.infer<typeof ConfigSchema>;
export type ServerConfig = z.infer<typeof ServerConfigSchema>;
// ... all types
```

### Schema Design Patterns

#### Zod v4 Features
- **Format Functions**: `z.int32()`, `z.url()`, `z.iso.datetime()`
- **Performance**: Optimized parsing for better runtime performance
- **Type Safety**: Enhanced TypeScript integration

#### Validation Strategies
- **Progressive Enhancement**: Basic types → format validation → business rules
- **Descriptive Errors**: Clear error messages for debugging
- **Cross-Field Validation**: Complex validation in `superRefine`

#### Reusability
- **Composable Schemas**: Small schemas compose into larger ones
- **Shared Validators**: Common patterns like `PositiveInt`, `HttpsUrl`
- **Registry Pattern**: Centralized access via `SchemaRegistry`

---

## Config Structure

The `config.ts` file implements a robust 4-pillar configuration pattern for production-ready applications.

### 4-Pillar Configuration Pattern

#### Pillar 1: Default Values
Comprehensive default configuration covering all scenarios:
```typescript
const defaultConfig: Config = {
  server: {
    baseUrl: "https://www.prd.presskits.eu.pvh.cloud/tommyxmercedes-amgf1xclarenceruth/",
    screenshotDir: "./navigation-screenshots",
    downloadsDir: "./downloads",
    // ... all server config
  },
  browser: {
    headless: false,
    viewport: { width: 1280, height: 720 },
    // ... all browser config
  },
  allowedDownloads: {
    extensions: enhancedAllowedDownloads.extensions,
    maxFileSize: enhancedAllowedDownloads.maxFileSize,
    // ... all download config
  },
};
```

#### Pillar 2: Environment Variable Mapping
Explicit mapping between config fields and environment variables:
```typescript
const envVarMapping = {
  server: {
    baseUrl: "BASE_URL",
    screenshotDir: "SCREENSHOT_DIR",
    pauseBetweenClicks: "PAUSE_BETWEEN_CLICKS",
    // ... all server mappings
  },
  browser: {
    headless: "BROWSER_HEADLESS",
    "viewport.width": "VIEWPORT_WIDTH",
    // ... all browser mappings
  },
  // ... all sections
} as const;
```

#### Pillar 3: Environment Loading
Type-safe environment variable parsing with fallbacks:
```typescript
function loadConfigFromEnv(): Partial<Config> {
  const envSource = typeof Bun !== "undefined" ? Bun.env : process.env;

  return {
    server: {
      baseUrl:
        (parseEnvVar(envSource[envVarMapping.server.baseUrl], "string") as string) ||
        defaultConfig.server.baseUrl,
      // ... all fields with parsing and fallbacks
    },
    // ... all sections
  };
}
```

#### Pillar 4: Configuration Initialization
Safe initialization with validation and error handling:
```typescript
function initializeConfig(): Config {
  try {
    const envConfig = loadConfigFromEnv();
    const mergedConfig = {
      // Deep merge with directory creation
    };

    const result = ConfigSchema.safeParse(mergedConfig);

    if (!result.success) {
      // Detailed error reporting
      throw new Error(/* formatted errors */);
    }

    return result.data;
  } catch (error) {
    console.error("Configuration initialization failed:", error);
    throw error;
  }
}
```

### Key Features

#### Environment Variable Parsing
Type-safe parsing with proper type conversion:
```typescript
function parseEnvVar(value: string | undefined, type: "string" | "number" | "boolean"): unknown {
  if (!value) return undefined;

  switch (type) {
    case "number": {
      const num = Number(value);
      return Number.isNaN(num) ? undefined : num;
    }
    case "boolean":
      return value.toLowerCase() === "true" || value === "1";
    default:
      return value;
  }
}
```

#### Runtime Environment Detection
Supports both Bun and Node.js environments:
```typescript
// Automatic environment detection
if (typeof Bun === "undefined") {
  dotenv.config();
}

// Runtime-appropriate environment source
const envSource = typeof Bun !== "undefined" ? Bun.env : process.env;
```

#### Directory Management
Automatic directory creation during configuration:
```typescript
function ensureDirectoryExists(dirPath: string): string {
  const fullPath = path.resolve(dirPath);
  if (!fs.existsSync(fullPath)) {
    fs.mkdirSync(fullPath, { recursive: true });
  }
  return dirPath;
}
```

#### Comprehensive Error Handling
Detailed validation errors with suggestions:
```typescript
if (!result.success) {
  console.error("Configuration validation failed:");
  const prettyError = z.prettifyError(result.error);
  console.error(prettyError);

  const issues = result.error.issues
    .map((issue) => {
      const path = issue.path.length > 0 ? issue.path.join(".") : "root";
      return `  - ${path}: ${issue.message}`;
    })
    .join("\n");

  throw new Error(`Invalid configuration:\n${issues}\n\nPlease check your environment variables and default configuration.`);
}
```

### Configuration Exports

#### Primary Export
Ready-to-use configuration instance:
```typescript
export const config = initializeConfig();
```

#### Re-exports from Schemas
Clean access to types and schemas:
```typescript
export { SchemaRegistry };
export type {
  Config,
  ServerConfig,
  BrowserConfig,
  // ... all types
};
```

#### Utility Functions
Helper functions for advanced use cases:
```typescript
export const getConfigJSONSchema = () => ConfigSchema;

export const validateConfiguration = (data: unknown) => {
  const result = ConfigSchema.safeParse(data);
  if (!result.success) {
    throw new Error(JSON.stringify(result.error.issues, null, 2));
  }
  return result.data;
};
```

### Best Practices Demonstrated

1. **Fail Fast**: Configuration validation happens at startup
2. **Clear Errors**: Descriptive error messages with paths and suggestions
3. **Type Safety**: Full TypeScript integration throughout
4. **Environment Flexibility**: Works in multiple JavaScript runtimes
5. **Production Ready**: Comprehensive error handling and logging
6. **Maintainable**: Clear separation and organization of concerns