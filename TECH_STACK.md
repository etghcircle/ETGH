# TECH_STACK.md — Tooling Guardrails

## Exact versions
| Component        | Version (pin these — update deliberately, not silently) |
|-------------------|----------------------------------------------------------|
| Kotlin            | 2.1.x                                                     |
| Ktor              | 3.x                                                       |
| Kobweb            | 0.21.x                                                    |
| MongoDB Driver    | 5.2.x (Kotlin: `mongodb-driver-kotlin-coroutine`)         |
| Cloudinary        | latest (Kotlin/Java SDK)                                 |
| Gradle            | 8.x (Kotlin DSL, `build.gradle.kts`)                      |
| JDK               | 21 (LTS)                                                  |

> When any version above needs bumping, update this file in the same change — do not let it drift silently.

## Approved libraries
- **Backend**: `ktor-server-core`, `ktor-server-auth`, `ktor-server-auth-jwt`, `ktor-server-content-negotiation`, `ktor-serialization-kotlinx-json`, `mongodb-driver-kotlin-coroutine`, `cloudinary-http44` (Cloudinary's Kotlin/Java SDK), `bcrypt` (for password hashing, e.g. `at.favre.lib:bcrypt`), `kotlinx-serialization-json`.
- **Frontend**: Kobweb's built-in composables, `kotlinx-coroutines-core`, `kotlinx-serialization-json`.
- **Testing**: `kotlin.test`, `ktor-server-test-host`, `testcontainers` (for MongoDB integration tests) — optional but preferred over mocking.

## Banned list
- **No OAuth libraries** (`ktor-server-auth` OAuth providers, Firebase Auth, Auth0 SDKs) — the auth model is fixed 4-account, not third-party identity. (See DECISIONS.md.)
- **No raw MongoDB queries** outside `repositories/` — always use the MongoDB Kotlin driver through typed repositories.
- **No client-side-only permission checks** — anything gating private content must be enforced in `services/`, never just hidden in Kobweb UI.
- **No plaintext password storage** — always bcrypt (or equivalent) hash before persisting.
- **No self-hosted video storage** — Cloudinary only (see DECISIONS.md), unless that decision is explicitly revisited.
- **No unmanaged global mutable state** in the frontend — state lives in viewmodels, not top-level `var`s.
