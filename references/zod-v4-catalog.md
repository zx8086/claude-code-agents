# Zod v4 Comprehensive Catalog
> External reference for config-reviewer agent
> Invoke via Read tool when specific validation patterns needed

## Complete Top-Level Format Functions

### String Validations
```typescript
// Email validation
z.email()  // Basic email validation
z.email({ pattern: 'strict' })  // RFC 5322 compliant
z.email({ pattern: 'simple' })  // Simple validation
z.email({ pattern: /^[a-z]+@company\.com$/ })  // Custom regex

// UUID variants
z.uuidv4()  // UUID version 4
z.uuidv7()  // UUID version 7
z.uuidv8()  // UUID version 8

// Network formats
z.ipv4()  // IPv4 address
z.ipv6()  // IPv6 address
z.cidrv4()  // CIDR v4 notation
z.cidrv6()  // CIDR v6 notation
z.url()  // URL validation

// Phone and encoding
z.e164()  // E.164 phone number format
z.base64()  // Base64 encoded string
z.base64url()  // Base64URL encoded string

// Authentication
z.jwt()  // JWT token validation

// Text transformations
z.lowercase()  // Lowercase string
```

### ISO Formats
```typescript
z.iso.date()  // ISO 8601 date (YYYY-MM-DD)
z.iso.datetime()  // ISO 8601 datetime
z.iso.duration()  // ISO 8601 duration (P1Y2M3DT4H5M6S)
z.iso.time()  // ISO 8601 time (HH:MM:SS)
```

### Numeric Types
```typescript
// Integer types
z.int32()  // 32-bit signed integer
z.int64()  // 64-bit signed integer
z.uint64()  // 64-bit unsigned integer

// Floating point
z.float32()  // 32-bit floating point
z.float64()  // 64-bit floating point

// BigInt
z.bigint()  // JavaScript BigInt

// With constraints (chained methods allowed here)
z.int32().min(1).max(10000)
z.float64().min(0.1).max(30.0)
z.bigint().min(1024n)
```

### Boolean Coercion
```typescript
z.stringbool()  // Converts string to boolean
// Accepts: "true", "false", "1", "0", "yes", "no"
```

### Object Strictness
```typescript
z.strictObject({})  // Replaces .strict() - no unknown keys allowed
z.looseObject({})  // Replaces .passthrough() - allows unknown keys
```

## Template Literals

```typescript
// Version patterns
const VersionSchema = z.template`v${'1' | '2' | '3'}.${'0' | '1' | '2'}`;
// Matches: "v1.0", "v2.1", "v3.2"

// Environment patterns
const EnvSchema = z.template`${string}-${'staging' | 'production'}`;
// Matches: "myapp-staging", "api-production"

// URL patterns
const EndpointSchema = z.template`https://${'api' | 'staging-api'}.${string}.com`;
// Matches: "https://api.example.com", "https://staging-api.example.com"

// Complex patterns
const ResourceSchema = z.template`/api/v${'1' | '2'}/${string}/${'users' | 'posts'}`;
// Matches: "/api/v1/resource/users", "/api/v2/another/posts"
```

## Discriminated Unions

```typescript
// Simple discriminated union
const EnvironmentConfigSchema = z.discriminatedUnion('type', [
  z.object({
    type: z.literal('development'),
    debugMode: z.boolean(),
    hotReload: z.boolean(),
    mockServices: z.boolean(),
  }),
  z.object({
    type: z.literal('production'),
    ssl: z.boolean(),
    monitoring: z.boolean(),
    backupEnabled: z.boolean(),
  }),
]);

// Multi-environment configuration
const DeploymentConfigSchema = z.discriminatedUnion('environment', [
  z.object({
    environment: z.literal('local'),
    debugLevel: z.literal('verbose', 'debug', 'info'),
    enableProfiler: z.boolean(),
  }),
  z.object({
    environment: z.literal('staging'),
    logLevel: z.literal('info', 'warn', 'error'),
    enableMonitoring: z.boolean(),
  }),
  z.object({
    environment: z.literal('production'),
    logLevel: z.literal('warn', 'error'),
    enableMonitoring: z.literal(true),
    ssl: z.literal(true),
  }),
]);
```

## Literal Types

```typescript
// Multiple values in single literal
const StatusSchema = z.literal('active', 'inactive', 'pending');

// Role-based literals
const RoleSchema = z.literal('admin', 'user', 'guest', 'moderator');

// Environment literals
const EnvironmentSchema = z.literal('development', 'staging', 'production');

// Log level literals
const LogLevelSchema = z.literal('debug', 'info', 'warn', 'error', 'fatal');
```

## Recursive Types

```typescript
// Service dependency tree
type ServiceConfig = {
  name: string;
  endpoint: string;
  dependencies?: ServiceConfig[];
};

const ServiceConfigSchema: z.ZodType<ServiceConfig> = z.object({
  name: z.string(),
  endpoint: z.url(),
  dependencies: z.array(z.lazy(() => ServiceConfigSchema)).optional(),
});

// Nested configuration sections
type NestedConfig = {
  key: string;
  value: string | number;
  children?: NestedConfig[];
};

const NestedConfigSchema: z.ZodType<NestedConfig> = z.object({
  key: z.string(),
  value: z.union([z.string(), z.number()]),
  children: z.array(z.lazy(() => NestedConfigSchema)).optional(),
});
```

## Object Composition

```typescript
// Base schema
const BaseSchema = z.object({
  id: z.string(),
  createdAt: z.iso.datetime(),
});

// Extend with additional fields
const ExtendedSchema = BaseSchema.extend({
  name: z.string(),
  email: z.email(),
});

// Omit fields
const PartialSchema = ExtendedSchema.omit({ id: true });

// Pick specific fields
const PickedSchema = ExtendedSchema.pick({ name: true, email: true });

// Overwrite for transformations
const TransformedSchema = BaseSchema.overwrite(z.object({
  id: z.string().transform(val => val.toUpperCase()),
  createdAt: z.iso.datetime().transform(val => new Date(val)),
}));

// Partial (all fields optional)
const OptionalSchema = ExtendedSchema.partial();

// Required (all fields required)
const RequiredSchema = OptionalSchema.required();
```

## File Validation

```typescript
// Image files
const ImageFileSchema = z.file({
  mimeTypes: ['image/png', 'image/jpeg', 'image/gif', 'image/webp'],
  maxSize: 5 * 1024 * 1024,  // 5MB
});

// Document files
const DocumentFileSchema = z.file({
  mimeTypes: ['application/pdf', 'application/msword', 'application/vnd.openxmlformats-officedocument.wordprocessingml.document'],
  maxSize: 10 * 1024 * 1024,  // 10MB
});

// Video files
const VideoFileSchema = z.file({
  mimeTypes: ['video/mp4', 'video/mpeg', 'video/quicktime'],
  maxSize: 100 * 1024 * 1024,  // 100MB
});

// Audio files
const AudioFileSchema = z.file({
  mimeTypes: ['audio/mpeg', 'audio/wav', 'audio/ogg'],
  maxSize: 20 * 1024 * 1024,  // 20MB
});

// CSV files
const CsvFileSchema = z.file({
  mimeTypes: ['text/csv'],
  maxSize: 50 * 1024 * 1024,  // 50MB
});
```

## JSON Schema and Registry

```typescript
// Convert Zod schema to JSON Schema
const ConfigSchema = z.object({
  apiUrl: z.url(),
  apiKey: z.jwt(),
  timeout: z.int32().min(1000).max(30000),
});

const jsonSchema = z.toJSONSchema(ConfigSchema, {
  name: 'APIConfiguration',
  description: 'API client configuration schema',
});

// Schema registry for metadata
const registry = z.registry();

registry.set(ConfigSchema, {
  title: "Application Configuration",
  version: "1.0.0",
  description: "Production-ready configuration schema",
  tags: ["config", "validation", "production"],
  examples: [{
    apiUrl: "https://api.example.com",
    apiKey: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    timeout: 5000,
  }],
});

// Add metadata to schemas
const UserSchema = z.object({
  email: z.email(),
  userId: z.uuidv4(),
  ipAddress: z.ipv4(),
  serverUrl: z.url(),
  apiToken: z.jwt(),
  phoneNumber: z.e164(),
  enabled: z.stringbool(),
}).meta({
  description: "User configuration schema",
  version: "1.0.0",
  deprecated: false,
});
```

## Error Handling (Zod v4)

```typescript
// DEPRECATED (DO NOT USE)
ctx.addIssue({ code: "custom", message: "..." })
z.object({}).parse(data, { errorMap: customErrorMap })
error.format()
error.flatten()

// MODERN (USE THESE)
ctx.error({ code: "custom", message: "..." })
z.object({}).parse(data, { error: customError })
z.prettifyError(error)

// Custom error messages
const schema = z.object({
  email: z.email(),
  age: z.int32().min(18),
}).superRefine((data, ctx) => {
  if (data.age < 21 && data.email.includes('restricted')) {
    return ctx.error({
      code: "custom",
      message: "Users under 21 cannot use restricted email domains",
      path: ['email'],
    });
  }
});

// Pretty error formatting
try {
  schema.parse(invalidData);
} catch (error) {
  const prettyError = z.prettifyError(error);
  console.error(prettyError);
  // Outputs user-friendly error messages with:
  // - Field paths
  // - Validation failures
  // - Suggested fixes
}
```

## Production Configuration Examples

### Complete Application Configuration
```typescript
const ConfigurationSchema = z.object({
  // Server configuration
  server: z.object({
    host: z.string(),
    port: z.int32().min(1).max(65535),
    protocol: z.literal('http', 'https'),
  }),

  // Database configuration
  database: z.object({
    url: z.url(),
    poolSize: z.int32().min(1).max(100),
    timeout: z.iso.duration(),
    ssl: z.boolean(),
  }),

  // Network configuration
  network: z.object({
    serverIpv4: z.ipv4(),
    serverIpv6: z.ipv6().optional(),
    allowedCidrv4: z.array(z.cidrv4()),
    allowedCidrv6: z.array(z.cidrv6()).optional(),
  }),

  // Security configuration
  security: z.object({
    sessionToken: z.jwt(),
    secretKey: z.base64(),
    publicKey: z.base64url(),
  }),

  // User configuration
  user: z.object({
    userId: z.uuidv7(),
    email: z.email({ pattern: 'strict' }),
    phoneNumber: z.e164().optional(),
  }),

  // Timing configuration
  timing: z.object({
    createdAt: z.iso.datetime(),
    validFrom: z.iso.date(),
    sessionDuration: z.iso.duration(),
    dailyResetTime: z.iso.time(),
  }),

  // Performance configuration
  performance: z.object({
    maxConnections: z.int32().min(1).max(10000),
    responseTimeout: z.float64().min(0.1).max(30.0),
    memoryLimit: z.bigint().min(1024n),
  }),
});
```

### Multi-Environment Configuration
```typescript
const MultiEnvConfigSchema = z.discriminatedUnion('environment', [
  // Development environment
  z.object({
    environment: z.literal('development'),
    debug: z.boolean(),
    logLevel: z.literal('verbose', 'debug', 'info'),
    hotReload: z.boolean(),
    mockServices: z.boolean(),
    database: z.object({
      url: z.url(),
      ssl: z.boolean(),
      poolSize: z.int32().min(1).max(20),
    }),
  }),

  // Staging environment
  z.object({
    environment: z.literal('staging'),
    debug: z.boolean(),
    logLevel: z.literal('info', 'warn', 'error'),
    database: z.object({
      url: z.url(),
      ssl: z.literal(true),
      poolSize: z.int32().min(10).max(50),
    }),
    monitoring: z.object({
      enabled: z.boolean(),
      endpoint: z.url(),
    }),
  }),

  // Production environment
  z.object({
    environment: z.literal('production'),
    debug: z.literal(false),
    logLevel: z.literal('warn', 'error'),
    database: z.object({
      url: z.url(),
      ssl: z.literal(true),
      poolSize: z.int32().min(20).max(100),
      backupEnabled: z.literal(true),
    }),
    monitoring: z.object({
      enabled: z.literal(true),
      endpoint: z.url(),
      alerting: z.boolean(),
    }),
    security: z.object({
      enforceHttps: z.literal(true),
      corsOrigins: z.array(z.url()),
    }),
  }),
]);
```

## Zod Mini (Minimal Bundle)

```typescript
import { object, string, number, boolean, array, parse } from 'zod/mini';

// Minimal configuration (1.88kb bundle)
const MiniConfigSchema = object({
  port: number(),
  host: string(),
  debug: boolean(),
  allowedHosts: array(string()),
});

const config = parse(MiniConfigSchema, Bun.env);

// Note: Zod Mini has limited feature set
// Use for performance-critical applications with simple validation needs
// For complex validation, use full Zod
```

## Testing Configuration Patterns

```typescript
// Test different environments
describe('Configuration Loading', () => {
  it('should load development config', () => {
    const devConfig = {
      environment: 'development',
      debug: true,
      logLevel: 'verbose',
    };

    expect(() => ConfigSchema.parse(devConfig)).not.toThrow();
  });

  it('should enforce production security', () => {
    const prodConfig = {
      environment: 'production',
      database: {
        password: 'password',  // Should fail
        ssl: false,  // Should fail
      },
    };

    expect(() => ConfigSchema.parse(prodConfig)).toThrow();
  });

  it('should validate email patterns', () => {
    const strictEmail = 'user@example.com';
    expect(() => z.email({ pattern: 'strict' }).parse(strictEmail)).not.toThrow();

    const invalidEmail = 'not-an-email';
    expect(() => z.email().parse(invalidEmail)).toThrow();
  });
});
```

## Common Configuration Patterns

### API Client Configuration
```typescript
const ApiClientConfigSchema = z.object({
  baseUrl: z.url(),
  apiKey: z.jwt(),
  timeout: z.iso.duration(),
  retryAttempts: z.int32().min(0).max(5),
  headers: z.record(z.string(), z.string()),
  rateLimit: z.object({
    maxRequests: z.int32().min(1),
    perDuration: z.iso.duration(),
  }),
});
```

### Database Configuration
```typescript
const DatabaseConfigSchema = z.object({
  host: z.string(),
  port: z.int32().min(1).max(65535),
  database: z.string(),
  username: z.string(),
  password: z.string().min(8),
  ssl: z.boolean(),
  poolSize: z.int32().min(1).max(100),
  connectionTimeout: z.iso.duration(),
  idleTimeout: z.iso.duration(),
});
```

### Logging Configuration
```typescript
const LoggingConfigSchema = z.object({
  level: z.literal('debug', 'info', 'warn', 'error', 'fatal'),
  format: z.literal('json', 'text', 'structured'),
  outputs: z.array(z.literal('console', 'file', 'syslog')),
  rotation: z.object({
    enabled: z.boolean(),
    maxSize: z.bigint(),
    maxFiles: z.int32().min(1),
  }).optional(),
});
```

### Cache Configuration
```typescript
const CacheConfigSchema = z.object({
  provider: z.literal('memory', 'redis', 'memcached'),
  ttl: z.iso.duration(),
  maxSize: z.bigint(),
  redis: z.object({
    host: z.string(),
    port: z.int32(),
    password: z.string().optional(),
    database: z.int32().min(0).max(15),
  }).optional(),
});
```

## Migration Guide (Deprecated → Modern)

```typescript
// DEPRECATED Chained Methods
z.string().email()  →  z.email()
z.string().url()  →  z.url()
z.string().uuid()  →  z.uuidv4()
z.string().ip()  →  z.ipv4() or z.ipv6()
z.string().cidr()  →  z.cidrv4() or z.cidrv6()
z.number().int()  →  z.int32()

// DEPRECATED Object Methods
z.object({}).strict()  →  z.strictObject({})
z.object({}).passthrough()  →  z.looseObject({})
schema1.merge(schema2)  →  schema1.extend({ ...schema2.shape })

// DEPRECATED Error Handling
ctx.addIssue({ ... })  →  ctx.error({ ... })
z.object({}).parse(data, { errorMap })  →  z.object({}).parse(data, { error })
error.format()  →  z.prettifyError(error)
error.flatten()  →  z.prettifyError(error)
```
