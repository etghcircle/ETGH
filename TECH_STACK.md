# TECH_STACK.md — Tooling Guardrails

## Exact versions
| Component        | Version (pin these — update deliberately, not silently) |
|-------------------|----------------------------------------------------------|
| Kotlin            | 2.1.x                                                     |
| Ktor              | 3.x                                                       |
| Exposed (ORM)     | 0.55.x                                                    |
| PostgreSQL        | 16.x                                                      |
| Compose Multiplatform (Web/Wasm) | 1.7.x                                       |
| Gradle            | 8.x (Kotlin DSL, `build.gradle.kts`)                      |
| JDK               | 21 (LTS)                                                  |

> When any version above needs bumping, update this file in the same change — do not let it drift silently.

## Approved libraries
- **Backend**: `ktor-server-core`, `ktor-server-auth`, `ktor-server-auth-jwt`, `ktor-server-content-negotiation`, `ktor-serialization-kotlinx-json`, `exposed-core`, `exposed-dao`, `exposed-jdbc`, `postgresql` (JDBC driver), `cloudinary-http44` (or Cloudinary's Kotlin/Java SDK), `bcrypt` (for password hashing, e.g. `at.favre.lib:bcrypt`).
- **Frontend**: `compose.runtime`, `compose.foundation`, `compose.material3` (or a hand-rolled minimal theme if Material3-for-Web isn't stable), `kotlinx-coroutines-core`, `kotlinx-serialization-json`.
- **Testing**: `kotlin.test`, `ktor-server-test-host`, `testcontainers` (for Postgres integration tests) — optional but preferred over mocking the DB.

## Banned list
- **No OAuth libraries** (`ktor-server-auth` OAuth providers, Firebase Auth, Auth0 SDKs) — the auth model is fixed 4-account, not third-party identity. (See DECISIONS.md.)
- **No raw JDBC/plain SQL strings** outside `repositories/` — always go through Exposed.
- **No client-side-only permission checks** — anything gating private content must be enforced in `services/`, never just hidden in Compose UI.
- **No plaintext password storage** — always bcrypt (or equivalent) hash before persisting.
- **No self-hosted video storage** — Cloudinary only (see DECISIONS.md), unless that decision is explicitly revisited.
- **No unmanaged global mutable state** in the frontend — state lives in viewmodels, not top-level `var`s.
