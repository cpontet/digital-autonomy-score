---
name: abstraction-patterns
user-invocable: false
description: |
  Heuristics for detecting vendor abstraction layers during DAS scanning.
  Helps distinguish direct vendor coupling from properly abstracted usage
  to produce more nuanced sovereignty and portability scores.
---

## How to Use This Reference

- After detecting vendor SDK imports (via vendor-db patterns), check whether those imports are behind an abstraction layer
- Use the abstraction level to adjust scoring — do not penalise a well-abstracted vendor dependency the same as a deeply coupled one
- Check the directory structure first (fastest signal), then look for interface patterns, then assess coupling depth

## Abstraction Levels

### Level 0: Direct Coupling

- Vendor SDK called directly from business logic / controllers / services
- Detection: vendor imports in files under `src/`, `app/`, `lib/` alongside business logic; no interface layer
- Example: `import boto3` in a Django view, `new S3Client()` in an Express route handler
- Score adjustment: **none** — apply full vendor penalty from vendor-db
- P3 impact: P3 ≤ 3 (proprietary SDK required)

### Level 1: Thin Wrapper

- Vendor calls centralised in a utility module, but no interface/contract
- Detection: vendor imports confined to 1-2 utility files (e.g., `utils/s3.ts`, `helpers/aws.py`); rest of codebase imports the wrapper
- Example: `storage.upload()` wrapping `s3.putObject()` but with no interface definition
- Score adjustment: **-1 on penalty** — still coupled but migration requires changing only the wrapper
- P3 impact: P3 = 4 (vendor-specific but localised)

### Level 2: Port/Adapter (Interface-based)

- An interface/contract defines the capability; vendor SDK is one implementation
- Detection: interface file (e.g., `ports/storage.ts`, `domain/repository.py`) + implementation file (e.g., `adapters/s3-storage.ts`, `infrastructure/aws_repository.py`); business logic imports the interface, not the implementation
- Example: `interface StoragePort { upload(file): Promise<void> }` with `class S3Storage implements StoragePort`
- Score adjustment: **-2 on penalty** — alternative implementations can be swapped
- P3 impact: P3 ≥ 6 (abstracted behind standard interface)

### Level 3: Full Abstraction (Hexagonal / Clean Architecture)

- Dependency injection, no vendor references in domain/application layers
- Detection: clear directory separation (`domain/`, `application/`, `infrastructure/`, `adapters/`); DI container or factory wiring implementations; vendor imports ONLY in infrastructure/adapter layer; domain layer has zero external imports
- Example: Spring `@Bean` configuration injecting `S3StorageAdapter` as `StoragePort`; NestJS module providing `S3_STORAGE` token
- Score adjustment: **-3 on penalty** (minimum penalty = 0) — migration is a configuration change
- P3 impact: P3 ≥ 7 (fully decoupled)

## Directory Structure Signals

Quick heuristics based on directory names. If these directories exist, check their contents:

| Directory Pattern | Suggests | Check |
|---|---|---|
| `adapters/`, `adapter/` | Port/adapter pattern (Level 2-3) | Verify interfaces exist alongside |
| `infrastructure/`, `infra/` | Infrastructure isolation (Level 2-3) | Check if vendor imports are confined here |
| `ports/`, `interfaces/`, `contracts/` | Explicit port definitions (Level 2-3) | Verify implementations exist separately |
| `domain/`, `core/`, `entities/` | Domain-driven design (Level 2-3) | Check this layer is vendor-free |
| `providers/`, `services/` | Could be Level 1 or 2 | Check if interfaces are defined |
| `utils/`, `helpers/`, `lib/` | Often Level 1 wrappers | Check if there's an interface contract |
| `plugins/`, `drivers/`, `backends/` | Pluggable architecture (Level 2-3) | Check for plugin interface/registry |

## Framework-Specific Patterns

### Java / Spring

- `@Repository` + interface → Level 2+
- `@Service` injecting interface → Level 2+
- Spring Cloud abstractions (Spring Cloud AWS, Spring Cloud GCP) → Level 1 (framework-mediated but still vendor-specific)

### TypeScript / NestJS

- Custom providers with `useClass`/`useFactory` → Level 2+
- Injection tokens with interface → Level 2+
- Direct SDK import in controller/service → Level 0

### Python / Django / FastAPI

- ABC (Abstract Base Class) + concrete implementations → Level 2+
- Django storage backends (`DEFAULT_FILE_STORAGE` setting) → Level 2
- Direct `boto3` in views/serializers → Level 0

### Go

- Interface type + struct implementation → Level 2+
- Package-level interface in `domain/` or `ports/` → Level 2+
- Direct SDK calls in handlers → Level 0

### .NET / C#

- `IStorageService` interface + DI registration → Level 2+
- `services.AddScoped<IStorage, AzureBlobStorage>()` → Level 2+

## Assessment Workflow

When vendor SDK detected:

1. **Locate all import sites** — grep for the vendor package across the codebase
2. **Count files with vendor imports** — if >5 files import the vendor directly → likely Level 0
3. **Check directory containment** — are all vendor imports in one directory? → likely Level 1+
4. **Look for interfaces** — search for interface/abstract class definitions related to the capability (storage, auth, messaging, etc.)
5. **Check DI wiring** — search for dependency injection configuration that binds interfaces to implementations
6. **Determine level** and apply score adjustment

## Reporting

When abstraction is detected, note it in the assessment:

- "AWS S3 SDK detected in `infrastructure/storage/s3.ts`, but usage is behind a `StoragePort` interface (`domain/ports/storage.ts`). Business logic references only the interface. Abstraction level: 2 (Port/Adapter). Score penalty reduced."
- "Azure SDK detected in 12 files across `src/services/`, `src/controllers/`, and `src/utils/`. No abstraction layer. Abstraction level: 0 (Direct Coupling). Full vendor penalty applied."
