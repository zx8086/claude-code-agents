# Agent Directory

Complete directory of specialized agents for technical tasks. Use this as a reference when you need expert help.

## Getting Help with Specialized Tasks

### API & Architecture

- **API design**: `api-designer` - REST and GraphQL API architecture, OpenAPI specs, Kong integration
- **System architecture**: `architect-reviewer` - Architecture validation, design patterns, scalability review
- **API gateway**: `kong-konnect-engineer` - Kong Konnect configuration, deck deployment, plugin orchestration

### Configuration & Validation

- **Configuration management**: `config-reviewer` - 4-pillar configuration pattern orchestrator
- **Schema validation**: `zod-validator` - Zod v4 schemas, validation patterns, format functions
- **Code quality**: `biome-config` - Biome linting/formatting, ESLint/Prettier migration

### Testing & Quality

- **Test strategy**: `test-orchestrator` - Coordinates unit, E2E, and performance testing
- **Unit testing**: `bun-test-specialist` - Bun test framework, TypeScript testing patterns
- **E2E testing**: `playwright-specialist` - Browser automation, visual testing, cross-browser compatibility
- **Performance testing**: `k6-specialist` - Load testing, stress testing, performance monitoring
- **Code refactoring**: `refactoring-specialist` - Safe code transformation, complexity reduction

### Runtime & Deployment

- **Bun optimization**: `bun-reviewer` - Bun v1.3+ native APIs, performance patterns
- **Docker containers**: `docker-reviewer` - Multi-stage builds, security hardening, optimization
- **CI/CD pipelines**: `github-deployment-specialist` - GitHub Actions workflows, deployment automation
- **Observability**: `observability-engineer` - OpenTelemetry, logging, tracing, metrics, APM

### Database (Couchbase)

- **Database specialist**: `couchbase-capella-specialist` - N1QL optimization, troubleshooting, health monitoring
- **Connection management**: `couchbase-connection-specialist` - Singleton pattern, connection lifecycle
- **Document operations**: `couchbase-document-specialist` - CRUD operations, transactions, validation
- **Query optimization**: `couchbase-query-specialist` - N1QL queries, index design, EXPLAIN analysis
- **Performance tuning**: `couchbase-performance-specialist` - Metrics, caching, batch operations
- **Error handling**: `couchbase-resilience-specialist` - Retry logic, circuit breakers, timeouts

### Frontend & GraphQL

- **Svelte development**: `svelte5-developer` - Svelte 5 runes, SvelteKit, reactive patterns
- **GraphQL**: `graphql-specialist` - GraphQL Yoga v5.x, Houdini, schema design, federation
- **UI/UX design**: `ux-ui-design-expert` - Design systems, accessibility, Tailwind CSS

### Advanced Development

- **MCP development**: `mcp-developer` - Model Context Protocol servers/clients, LangSmith instrumentation

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
