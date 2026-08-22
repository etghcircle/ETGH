# CONTEXT.md

## What this app is
A private website for a 4-person friend group (Admin + F1, F2, F3). It hosts their
first-meeting story, an animated video, shared memories, and fun content. Some
content is public (anyone can view), some is private (only the 4 accounts can
view/edit).

## Core goals
- Let each of F1/F2/F3 manage (add/edit) their own memories, stories, and fun facts.
- Let Admin manage everyone's content.
- Cleanly separate public vs. private visibility, enforced server-side (not just hidden in the UI).
- Keep it simple — this is a personal project, not a product with growth targets.

## Tech stack (summary — see TECH_STACK.md for exact versions)
- **Backend**: Kotlin + Ktor
- **DB**: MongoDB
- **Frontend**: Kotlin + Kobweb
- **Auth**: Fixed 4-account model (Admin, F1, F2, F3), username fixed, password changeable, session via JWT
- **Video hosting**: Cloudinary (signed URLs for private videos)
- **Deployment**: GitHub Actions (private monorepo)

## Folder layout (high level — see ARCHITECTURE.md for detail)
```
/backend
  /routes
  /services
  /repositories
  /models
/frontend
  /pages
  /components
  /viewmodels
  /assets
```

## Who uses this
Just the 4 friends. No public sign-up, no growth/scale concerns, no multi-tenant needs.
