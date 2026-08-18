# SRS.md — Source of Truth

## User personas
- **Admin** — the site owner/organizer. Can view and edit all content across all users. Only one Admin account exists.
- **F1, F2, F3** — the three friends. Each can view/edit only their own content. Usernames are fixed; only their password is changeable.
- **Public visitor** — anyone with the site URL, no login. Can only see content explicitly marked public. Cannot edit anything, cannot see private content.

## Core features (MVP)
1. **Authentication**
   - 4 fixed accounts (Admin, F1, F2, F3). Fixed usernames, changeable passwords.
   - Session/JWT-based login.
2. **Content model**
   - "Memory" items: title, description, date, media (image/video), tags (optional).
   - Every item has an owner (Admin/F1/F2/F3) and a visibility flag (public/private).
3. **Permissions**
   - Admin: view/edit all memories regardless of owner or visibility.
   - F1/F2/F3: view/edit only memories they own.
   - Public visitors: view-only, public-visibility items only.
4. **Public pages**
   - First-meeting story page.
   - Animated video (public, via Cloudinary).
   - Any memory explicitly marked public.
5. **Private pages**
   - Memories marked private — visible only after login as one of the 4 accounts.
6. **Media handling**
   - Video/image upload via Cloudinary.
   - Private media served via signed, expiring URLs — never a raw public Cloudinary link for private content.

## Explicitly out of scope for MVP
- Public sign-up / new accounts beyond the fixed 4.
- Comments, likes, or any social feature involving people outside the 4.
- Mobile app (web-only for now).
- Multi-language support.
- Real-time features (chat, live notifications).

## Non-functional rules
- **Security**: private content must never be reachable via a guessable or unauthenticated URL. Passwords always hashed (bcrypt). No secrets committed to the repo.
- **Performance**: personal-scale traffic only (4 users + occasional public visitors) — no need to over-engineer for scale.
- **Screens**: must be usable on both desktop and mobile browser widths (responsive, not necessarily a separate mobile layout).
- **Simplicity**: prefer the smallest solution that satisfies a feature over a more "impressive" but complex one — this is a personal project, not a portfolio scale-demo.
