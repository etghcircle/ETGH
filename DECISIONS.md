# DECISIONS.md — Design History

Append-only log. Newest at top. Never delete an entry — if a decision is reversed, add a new entry noting the reversal and why.

---

**[2026-08-23] Frontend: Kobweb instead of Compose Multiplatform Web**
- Considered: Direct Compose Multiplatform Web (Wasm), React with TypeScript.
- Chose Kobweb: provides a Kotlin-first web framework with built-in routing and simpler dev experience. Enables full-Kotlin stack (backend + frontend) without the complexity of raw Wasm compilation.
- This reverses the [2026-08-15] Compose decision — Kobweb is Kotlin for web, maintains single-language goal while being more practical for web development.

**[2026-08-23] Database: MongoDB instead of PostgreSQL/Exposed**
- Considered: PostgreSQL + Exposed ORM.
- Chose MongoDB: simpler persistence model for this personal-scale project. No schema migrations needed, flexible document structure fits the memory/content model naturally.
- Reason: reduces operational overhead, easier to evolve the data model without migrations.

**[2026-08-23] Repository/Deployment: Private GitHub monorepo with GitHub Actions**
- Frontend and backend remain in one private GitHub repository.
- GitHub Actions will handle: build, test, and deployment workflows.
- Reason: all code in one place (single monorepo), CI/CD via GitHub native tools, no external services needed for deployment.

**[2026-08-15] Video hosting: Cloudinary, not YouTube/self-hosted**
- Considered: YouTube (unlisted), Bunny.net Stream, Cloudflare Stream, self-hosted S3.
- Chose Cloudinary: free tier is enough for personal-project scale, API is straightforward for a backend-first dev, supports signed URLs so private videos can be gated by the app's own auth instead of relying on an unlisted link.
- Do not switch to relying on "unlisted" links for anything marked private — that is not real access control.

**[2026-08-15] Auth model: 4 fixed named accounts, not OAuth**
- Considered: Google/GitHub OAuth.
- Rejected in favor of: fixed accounts (Admin, F1, F2, F3), usernames not editable, only passwords changeable.
- Reason: exactly 4 known users, no need for third-party identity, simpler to reason about permissions.
- Do not reintroduce OAuth login unless the user base changes.

**[2026-08-15] Permission model**
- Admin: view/edit all content.
- F1/F2/F3: view/edit only their own content.
- Every piece of content also carries a public/private visibility flag, independent of ownership.
- Enforcement must happen server-side (Ktor route/service layer), never only in the frontend.

**[2026-08-15] Frontend: Compose Multiplatform, not React/plain HTML**
- Reason: user wants a full-Kotlin stack; comfortable staying in one language across backend and frontend.
