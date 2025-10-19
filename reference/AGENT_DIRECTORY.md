# Agent Directory

Complete directory of specialized agents for technical tasks. Use this as a reference when you need expert help.

## Getting Help with Specialized Tasks

### API & Architecture

- **API design**: `api-designer` - Expert in designing scalable, developer-friendly APIs using REST and GraphQL patterns. Creates comprehensive OpenAPI 3.1 specifications, implements versioning strategies, designs consistent error handling, and integrates with Kong API Gateway. Focuses on API contract design, developer experience, and production-ready documentation with tools like Swagger UI, Spectral validation, and Postman collections.

- **System architecture**: `architect-reviewer` - Senior architect specializing in system design validation and technical decision review. Evaluates architectural patterns, identifies scalability bottlenecks, reviews technology stack choices, validates microservices design, and ensures alignment with best practices. Use proactively for architectural decisions, refactoring strategies, and system design improvements before implementation begins.

- **API gateway**: `kong-konnect-engineer` - Kong Konnect enterprise specialist managing API gateway infrastructure using declarative deck configuration. Handles plugin orchestration (rate limiting, authentication, CORS, logging), service mesh integration, multi-environment deployments, and production-ready patterns for enterprise-scale API management. Equipped with battle-tested Kong MCP tools for comprehensive gateway management.

### Configuration & Validation

- **Configuration management**: `config-reviewer` - Orchestrator for the 4-pillar configuration pattern (environment variables, config.ts, Zod validation, Biome linting). Enforces type-safe configuration management across development, staging, and production environments. Automatically delegates Zod schema creation to zod-validator and Biome setup to biome-config while maintaining overall configuration architecture consistency. Never handles schemas or linting rules directly.

- **Schema validation**: `zod-validator` - Zod v4 validation expert specializing in modern schema patterns using top-level format functions (replacing deprecated .refine()). Creates production-ready validation schemas with proper error messages, implements complex validation logic, optimizes schema performance, and handles Zod v3 to v4 migrations. Critical for all runtime validation, API request/response validation, and configuration validation.

- **Code quality**: `biome-config` - Modern code quality specialist for Biome toolchain (successor to ESLint/Prettier). Configures unified linting and formatting, handles ESLint/Prettier migrations, sets up CI/CD integration, and optimizes performance for large codebases. Specializes in creating consistent code quality standards across teams with fast, zero-config defaults.

### Testing & Quality

- **Test strategy**: `test-orchestrator` - Comprehensive testing coordinator orchestrating unit, integration, E2E, and performance testing strategies across multiple frameworks. Plans test coverage, coordinates bun-test-specialist, playwright-specialist, and k6-specialist, designs testing workflows, and ensures cross-framework integration. Creates holistic test execution plans for CI/CD pipelines and quality gates.

- **Unit testing**: `bun-test-specialist` - High-performance unit testing expert using Bun's native test framework. Specializes in TypeScript testing patterns, test performance optimization, mock strategies, snapshot testing, and coverage analysis. Works with test-orchestrator for cross-framework coordination. Leverages Bun's speed for rapid test execution in development and CI environments.

- **E2E testing**: `playwright-specialist` - End-to-end testing expert specializing in browser automation, visual regression testing, and cross-browser compatibility (Chrome, Firefox, Safari, Edge). Masters Playwright configuration, page object models, test parallelization, trace viewing, and accessibility testing. Coordinates with test-orchestrator for comprehensive testing workflows and handles complex user journey validation.

- **Performance testing**: `k6-specialist` - Load testing and performance validation specialist using K6 framework. Designs realistic load test scenarios, stress tests, spike tests, and soak tests. Analyzes performance metrics, identifies bottlenecks, creates custom metrics, and integrates with monitoring systems. Works with test-orchestrator for comprehensive performance validation strategies.

- **Code refactoring**: `refactoring-specialist` - Expert in safe code transformation and design pattern application. Masters systematic refactoring techniques, complexity reduction, legacy code modernization, and performance optimization while preserving behavior through test-driven approaches. Use proactively for code quality improvements, architectural cleanup, and technical debt reduction.

### Runtime & Deployment

- **Bun optimization**: `bun-reviewer` - Bun v1.3+ runtime specialist validating native API usage and performance patterns. Ensures proper use of Bun.serve(), Bun.file(), Bun.spawn(), and other native APIs instead of Node.js compatibility layers. Validates runtime-specific optimizations but delegates configuration to config-reviewer, testing to bun-test-specialist, and deployment to github-deployment-specialist. Critical for maximizing Bun's performance advantages.

- **Docker containers**: `docker-reviewer` - Production containerization expert specializing in multi-stage builds, security hardening, and CI/CD optimization. Implements distroless/Alpine patterns, enforces non-root execution, ensures proper PID 1 signal handling (dumb-init/tini), optimizes layer caching, and validates CIS Docker Benchmark compliance. Works with config-reviewer for environment integration and github-deployment-specialist for CI/CD workflows. MUST BE USED for all Dockerfile reviews and container security audits.

- **CI/CD pipelines**: `github-deployment-specialist` - GitHub Actions workflow orchestrator specializing in deployment automation and CI/CD optimization patterns. Delegates Bun runtime validation to bun-reviewer and security scanning to observability-engineer while enforcing deployment best practices. Handles multi-platform builds, automated testing integration, security scanning orchestration (Trivy, Snyk), SBOM generation, and workflow performance optimization.

- **Observability**: `observability-engineer` - OpenTelemetry-native observability specialist for ALL monitoring, logging, tracing, and metrics needs. Implements production-ready telemetry using 2025 OpenTelemetry standards with Bun runtime optimization. Masters distributed tracing, APM integration, custom metrics, structured logging, alerting strategies, and performance monitoring. Use proactively for any observability, debugging, or system health requirements.

### Database (Couchbase)

- **Database specialist**: `couchbase-capella-specialist` - Expert Couchbase Capella coordinator for all database issues, slow queries, connection failures, and health monitoring. Coordinates all Couchbase specialists, provides evidence-based analysis with specific code references, and implements production-ready patterns for cloud deployments, timeout management, circuit breaker integration, and cross-system health correlation. Use proactively when working with Couchbase SDK or troubleshooting database problems.

- **Connection management**: `couchbase-connection-specialist` - Implements unified KISS-principle singleton pattern for Couchbase Capella SDK connections. Handles connection setup, lifecycle management, graceful shutdown handlers, configuration management, and connection pooling. Ensures single source of truth for database connections across the application. MUST BE USED for initial connection setup and connection-related issues.

- **Document operations**: `couchbase-document-specialist` - CRUD operations specialist focused on document mutations, schema validation, transaction management, and CAS (Compare-And-Swap) conflict handling. Designs document structures, implements validation logic, manages multi-document transactions, and optimizes document access patterns. Use proactively when implementing data layer operations or handling document conflicts.

- **Query optimization**: `couchbase-query-specialist` - N1QL query performance expert implementing the 32 Essential N1QL Optimization Rules. Analyzes EXPLAIN plans, designs covering indexes, optimizes slow queries, implements prepared statements, and provides evidence-based query optimization. MUST BE USED for slow queries, query optimization, index design, and N1QL best practices. Specializes in systematic query performance improvement.

- **Performance tuning**: `couchbase-performance-specialist` - Performance monitoring and optimization expert focused on metrics collection, caching strategies, batch operations, and performance baselines. Implements performance monitoring, analyzes slow operations, designs caching layers, and optimizes high-throughput scenarios. Use proactively when investigating performance degradation or implementing metrics collection.

- **Error handling**: `couchbase-resilience-specialist` - Resilience and fault tolerance specialist implementing retry logic with exponential backoff, circuit breaker patterns, timeout configuration, and graceful degradation strategies. Handles transient errors, manages ambiguous operations, and designs resilient database access patterns. Use proactively when implementing error handling or designing fault-tolerant database operations.

### Frontend & GraphQL

- **Svelte development**: `svelte5-developer` - Expert Svelte 5 and SvelteKit developer specializing in modern reactive patterns using the runes system ($state, $derived, $effect). Masters component architecture, full-stack TypeScript applications, advanced reactivity, state management, and production-ready patterns. Has live access to Svelte documentation via MCP server for real-time guidance. Use for Svelte 5 development, component design systems, SvelteKit routing, and performance optimization.

- **GraphQL**: `graphql-specialist` - Comprehensive GraphQL expert specializing in GraphQL Yoga v5.x server implementation and Houdini client integration. Masters schema design, resolver optimization, federation architecture, real-time subscriptions, security patterns, and performance optimization. MUST BE USED for all GraphQL schema design, resolver implementation, client integration, and subscription handling. Implements production-ready patterns with type safety and developer experience optimization.

- **UI/UX design**: `ux-ui-design-expert` - Expert visual and interaction designer creating intuitive, beautiful, accessible user interfaces using Svelte 5, Bun, and Tailwind CSS. Masters design systems, user research, interaction patterns, visual hierarchy, and accessibility standards (WCAG). Implements designs directly in code with pixel-perfect precision while maintaining exceptional performance. Balances aesthetics with functionality and usability.

### Advanced Development

- **MCP development**: `mcp-developer` - Expert Model Context Protocol developer specializing in MCP server and client development with production-ready patterns. Masters protocol implementation, SDK usage, JSON-RPC compliance, transport configuration, and building robust integrations between AI systems and external tools/data sources. CRITICAL: All implementations REQUIRE mandatory LangSmith instrumentation for AI implementation observability and debugging. Equipped with battle-tested patterns including advanced monitoring, caching, fault tolerance, multi-agent coordination, and graceful degradation. Use proactively for MCP server/client development, protocol implementation, AI-tool integration, production deployment, and performance optimization.

---

## Quick Reference by Task

### When you need to...

**Build an API:**
1. `api-designer` - Design REST/GraphQL endpoints
2. `kong-konnect-engineer` - Configure API gateway
3. `observability-engineer` - Add monitoring

**Setup configuration:**
1. `config-reviewer` - Implement 4-pillar pattern
2. `zod-validator` - Create validation schemas
3. `biome-config` - Setup code quality tools

**Implement testing:**
1. `test-orchestrator` - Plan testing strategy
2. `bun-test-specialist` - Write unit tests
3. `playwright-specialist` - Create E2E tests
4. `k6-specialist` - Add performance tests

**Work with Couchbase:**
1. `couchbase-connection-specialist` - Setup connection
2. `couchbase-document-specialist` - Implement CRUD
3. `couchbase-query-specialist` - Optimize queries
4. `couchbase-performance-specialist` - Add caching/metrics
5. `couchbase-resilience-specialist` - Handle errors

**Deploy application:**
1. `docker-reviewer` - Create Dockerfile
2. `github-deployment-specialist` - Setup CI/CD
3. `observability-engineer` - Add monitoring

**Build frontend:**
1. `svelte5-developer` - Create Svelte components
2. `graphql-specialist` - Implement GraphQL client
3. `ux-ui-design-expert` - Design UI/UX

**Optimize performance:**
1. `bun-reviewer` - Optimize Bun runtime usage
2. `couchbase-performance-specialist` - Database performance
3. `k6-specialist` - Load test application

**Review architecture:**
1. `architect-reviewer` - System design validation
2. `refactoring-specialist` - Code quality improvements

---

## Agent Capabilities Summary

### API & Gateway
| Agent | Primary Focus | Key Capabilities |
|-------|--------------|------------------|
| `api-designer` | API architecture | REST/GraphQL design, OpenAPI 3.1, Kong integration, versioning |
| `kong-konnect-engineer` | API gateway | Deck deployment, plugin config, rate limiting, authentication |

### Architecture & Code Quality
| Agent | Primary Focus | Key Capabilities |
|-------|--------------|------------------|
| `architect-reviewer` | System design | Architecture validation, scalability review, pattern selection |
| `refactoring-specialist` | Code transformation | Safe refactoring, complexity reduction, design patterns |
| `biome-config` | Code quality | Biome setup, linting rules, formatting standards |

### Configuration & Validation
| Agent | Primary Focus | Key Capabilities |
|-------|--------------|------------------|
| `config-reviewer` | Configuration patterns | 4-pillar pattern, environment variables, orchestration |
| `zod-validator` | Schema validation | Zod v4 schemas, format functions, validation patterns |

### Testing
| Agent | Primary Focus | Key Capabilities |
|-------|--------------|------------------|
| `test-orchestrator` | Test strategy | Cross-framework coordination, comprehensive planning |
| `bun-test-specialist` | Unit testing | Bun test framework, TypeScript patterns, coverage |
| `playwright-specialist` | E2E testing | Browser automation, visual testing, cross-browser |
| `k6-specialist` | Performance testing | Load testing, stress testing, metrics |

### Runtime & Deployment
| Agent | Primary Focus | Key Capabilities |
|-------|--------------|------------------|
| `bun-reviewer` | Bun optimization | Native APIs, performance patterns, runtime validation |
| `docker-reviewer` | Containerization | Multi-stage builds, security hardening, optimization |
| `github-deployment-specialist` | CI/CD | GitHub Actions, workflow optimization, deployment |
| `observability-engineer` | Monitoring | OpenTelemetry, tracing, metrics, logging, APM |

### Database (Couchbase Specialists)
| Agent | Primary Focus | Key Capabilities |
|-------|--------------|------------------|
| `couchbase-capella-specialist` | Database expert | N1QL optimization, troubleshooting, health monitoring |
| `couchbase-connection-specialist` | Connection management | Singleton pattern, lifecycle, graceful shutdown |
| `couchbase-document-specialist` | Document operations | CRUD, transactions, CAS conflicts, validation |
| `couchbase-query-specialist` | Query optimization | Index design, EXPLAIN plans, prepared statements |
| `couchbase-performance-specialist` | Performance | Metrics collection, caching, batch operations |
| `couchbase-resilience-specialist` | Error handling | Retry logic, circuit breakers, timeout management |

### Frontend & GraphQL
| Agent | Primary Focus | Key Capabilities |
|-------|--------------|------------------|
| `svelte5-developer` | Svelte development | Runes system, SvelteKit, reactive patterns, state management |
| `graphql-specialist` | GraphQL | Yoga v5.x, Houdini, federation, subscriptions |
| `ux-ui-design-expert` | UI/UX design | Design systems, accessibility, Tailwind CSS |

### Advanced Development
| Agent | Primary Focus | Key Capabilities |
|-------|--------------|------------------|
| `mcp-developer` | MCP protocol | Server/client development, LangSmith instrumentation |

---

## Common Workflows

### 1. New API Development
```
api-designer → kong-konnect-engineer → observability-engineer
```

### 2. Database Integration
```
couchbase-connection-specialist → couchbase-document-specialist → 
couchbase-query-specialist → couchbase-performance-specialist
```

### 3. Full Testing Suite
```
test-orchestrator → bun-test-specialist + playwright-specialist + k6-specialist
```

### 4. Production Deployment
```
docker-reviewer → github-deployment-specialist → observability-engineer
```

### 5. Configuration Setup
```
config-reviewer → zod-validator + biome-config
```

### 6. Frontend Development
```
svelte5-developer → graphql-specialist → ux-ui-design-expert
```

---

## Agent Coordination Patterns

### Orchestrator Agents
These agents coordinate with specialists:
- `config-reviewer` - Delegates to `zod-validator` and `biome-config`
- `test-orchestrator` - Delegates to `bun-test-specialist`, `playwright-specialist`, `k6-specialist`
- `couchbase-capella-specialist` - Coordinates all Couchbase specialists

### Specialist Agents
These agents focus on specific technical domains and delegate outside their scope:
- All Couchbase specialists delegate to each other as needed
- Runtime specialists (`bun-reviewer`, `docker-reviewer`) delegate to deployment specialists
- Testing specialists delegate to `test-orchestrator` for strategy

---

## How to Use This Directory

1. **Identify your task** - What do you need to accomplish?
2. **Find the matching agent** - Use the tables or "When you need to..." section
3. **Request the agent** - Ask for help from the specific agent by name
4. **Follow the workflow** - Use the common workflows as a guide for multi-step tasks

Example request:
```
"Please invoke the couchbase-query-specialist to optimize this N1QL query"
```

---

## Notes

- Agents with "ALWAYS USE" or "MUST BE USED" descriptions should be invoked for their specific domains
- Orchestrator agents automatically coordinate with specialists
- Most agents can work together - don't hesitate to request multiple agents for complex tasks
- Agents marked "Use PROACTIVELY" will be automatically invoked when relevant

---

Last updated: 2025-01-14
Total agents: 25
