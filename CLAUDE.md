# CLAUDE.md — Quick Rules

## Style
- Kotlin, official style guide (4-space indent, no wildcard imports).
- Backend: Ktor idioms — routes in `routes/`, business logic in `services/`, DB access in `repositories/`.
- Frontend: Compose Multiplatform (Web/Wasm) — composables are small, stateless where possible; state hoisted to view models.
- No hardcoded secrets (Cloudinary keys, JWT secret, DB creds) — always read from environment variables / `.env` (never commit `.env`).
- Names: Admin, F1, F2, F3 are fixed constants — never treat as user-editable data.

## Build
```bash
# Backend (Ktor)
./gradlew :backend:build
./gradlew :backend:run

# Frontend (Compose for Web)
./gradlew :frontend:wasmJsBrowserRun
```

## Test
```bash
./gradlew :backend:test        # unit + auth/permission tests
./gradlew :backend:test --tests "*AuthTest*"   # auth-only
```
- Every new endpoint touching auth or visibility (public/private) MUST have a permission test before merge.
- Manual check before any release: log in as each of Admin/F1/F2/F3 and confirm edit/view boundaries hold.

## Before committing
1. Run backend tests.
2. Confirm no secrets in diff.
3. Confirm private content never leaks through a public-facing route (spot check `GET` endpoints without auth headers).
