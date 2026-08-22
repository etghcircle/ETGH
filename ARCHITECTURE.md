# ARCHITECTURE.md — The Map

## Folder tree
```
project-root/
├── backend/
│   ├── src/main/kotlin/
│   │   ├── routes/          # Ktor route definitions only — no business logic here
│   │   │   ├── AuthRoutes.kt
│   │   │   ├── MemoryRoutes.kt
│   │   │   └── MediaRoutes.kt
│   │   ├── services/        # Business logic, permission checks
│   │   │   ├── AuthService.kt
│   │   │   ├── PermissionService.kt
│   │   │   ├── MemoryService.kt
│   │   │   └── CloudinaryService.kt
│   │   ├── repositories/    # DB access via Exposed — no business logic here
│   │   │   ├── UserRepository.kt
│   │   │   └── MemoryRepository.kt
│   │   ├── models/           # Data classes + Exposed table objects
│   │   │   ├── User.kt
│   │   │   └── Memory.kt
│   │   └── Application.kt   # Ktor entry point, plugin/module wiring
│   └── src/test/kotlin/     # Mirrors main/ structure
├── frontend/
│   └── src/jsMain/kotlin/
│       ├── pages/          # Kobweb page routes
│       ├── components/     # Reusable Kobweb composables
│       ├── viewmodels/     # State holders, API calls
│       └── assets/         # Static design tokens, fonts
├── CLAUDE.md
├── CONTEXT.md
├── PROMPTS.md
├── AGENTS.md
├── DECISIONS.md
├── ARCHITECTURE.md
├── TECH_STACK.md
└── SRS.md
```

## File placement rules
- New Ktor route → `routes/`. Never put DB queries or permission logic directly in a route handler; call a service.
- New business rule (e.g. "can F2 edit this?") → `services/PermissionService.kt`. Do not duplicate permission checks inline elsewhere.
- New MongoDB collection/query → `repositories/`. Repositories return domain models, not raw DB documents.
- New UI page/screen → `frontend/pages/` (for Kobweb routes) or `frontend/components/` (for reusable composables). Pages should call viewmodels for data/state, not the API directly.
- Shared design values (colors, spacing, fonts) → `frontend/assets/`. No component should hardcode a hex color inline.

## Data flow (request → UI)
```
Browser (Kobweb)
   │  HTTP request (with session/JWT cookie if authenticated)
   ▼
Ktor route (routes/*)
   │  delegates to
   ▼
Service layer (services/*)
   │  checks PermissionService (Admin? owner? public content?)
   │  calls
   ▼
Repository (repositories/*) ──▶ MongoDB (via Kotlin driver)
   │
   ▼ (for media)
CloudinaryService ──▶ Cloudinary API (returns signed URL if private, plain URL if public)
   │
   ▼
Response DTO ──▶ back to Kobweb frontend ──▶ rendered in component
```

## Rule of thumb
If the AI is unsure where a new file goes, it should ask rather than guess — do not create new top-level folders without updating this file first.
