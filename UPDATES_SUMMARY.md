# Tech Stack Update Summary — 2026-08-23

All project documentation has been updated to reflect the new architecture:

## 🔴 CRITICAL FILES UPDATED

### 1. **TECH_STACK.md** ✅
- **Removed**: PostgreSQL 16.x, Exposed 0.55.x
- **Added**: MongoDB Driver 5.2.x (Kotlin), Kobweb 0.21.x
- **Updated libraries**:
  - Backend: removed `exposed-*`, `postgresql`; added `mongodb-driver-kotlin-coroutine`
  - Frontend: replaced Compose Web with Kobweb built-in composables
  - Testing: Testcontainers for MongoDB instead of PostgreSQL
- **Updated banned list**: No raw MongoDB queries (instead of Exposed), no Kobweb UI-only checks

### 2. **ARCHITECTURE.md** ✅
- **Folder tree**: Changed `frontend/src/wasmJsMain/kotlin/` → `frontend/src/jsMain/kotlin/`
  - `composables/` → `pages/` + `components/`
- **File placement rules**: MongoDB collections instead of Exposed tables
- **Data flow diagram**: PostgreSQL (via Exposed) → MongoDB (via Kotlin driver)
- All references to "Compose Web" updated to "Kobweb"

### 3. **CONTEXT.md** ✅
- Tech stack: PostgreSQL via Exposed → MongoDB
- Tech stack: Compose Multiplatform Web → Kobweb
- Added: GitHub Actions deployment
- Folder layout updated to reflect Kobweb structure

### 4. **DECISIONS.md** ✅
- **Added (newest at top)**:
  - `[2026-08-23] Frontend: Kobweb instead of Compose Multiplatform Web`
  - `[2026-08-23] Database: MongoDB instead of PostgreSQL/Exposed`
  - `[2026-08-23] Repository/Deployment: Private monorepo with GitHub Actions`
- Preserved all previous decisions (append-only log maintained)

## 🟠 SUPPORTING FILES UPDATED

### 5. **README.md** ✅
- Setup instructions:
  - Old: `./gradlew :frontend:wasmJsBrowserRun`
  - New: `./gradlew :frontend:kobwebStart` (dev server on http://localhost:8080)
- Environment variables: `DATABASE_URL=` → `MONGODB_URI=mongodb://localhost:27017/memory-vault`
- Clarified MongoDB and Cloudinary as prerequisites

### 6. **CLAUDE.md** ✅
- Frontend style: "Compose Multiplatform (Web/Wasm)" → "Kobweb"
- Build commands:
  - Backend: `./gradlew :backend:build` / `./gradlew :backend:run`
  - Frontend: `./gradlew :frontend:kobwebStart`

### 7. **PROMPTS.md** ✅
- "Add a new memory type/field": Exposed table → MongoDB schema
- "Add/modify a Compose UI screen" → "Add/modify a Kobweb page or component"
- File paths: `frontend/composables/` → `frontend/pages/` or `frontend/components/`

## 🟢 NO CHANGES NEEDED

### 8. **AGENTS.md** ✅
- Already generic (no tech-specific language)
- Roles (Coder, Tester, Reviewer) remain unchanged

### 9. **SRS.md** ✅
- Functional requirements unchanged
- 4-account auth model, permission model, content visibility all the same
- No tech stack details in this file

---

## Key Architecture Shifts

| Component | Old | New |
|-----------|-----|-----|
| **Frontend** | Compose Multiplatform Web (Wasm) | Kobweb |
| **Database** | PostgreSQL + Exposed ORM | MongoDB |
| **Frontend folder** | `composables/`, `viewmodels/` | `pages/`, `components/`, `viewmodels/` |
| **Frontend build** | `kobwebStart` doesn't exist in old setup | `:frontend:kobwebStart` (dev server) |
| **Data access** | Exposed repositories | MongoDB Kotlin driver repositories |
| **Deployment** | Not mentioned | GitHub Actions |

---

## Next Steps

1. ✅ All documentation is now in sync with Kobweb + MongoDB
2. 📝 When building the project, follow ARCHITECTURE.md folder layout
3. 🔧 Start with backend (Ktor + MongoDB) — see CLAUDE.md for build commands
4. 🎨 Then frontend (Kobweb) — follow TECH_STACK.md and CLAUDE.md
5. 🧪 Test coverage per CLAUDE.md (backend tests mandatory before merge)
6. 🚀 Deploy via GitHub Actions (workflow to be set up)

All files are ready to go in your private monorepo! 🗝️
