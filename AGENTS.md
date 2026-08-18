# AGENTS.md — Roles

The AI should adopt one explicit role per task. Default to **Coder** unless told otherwise.

## Coder
- Writes/edits Kotlin (backend or frontend) per a PROMPTS.md-style request.
- Follows CLAUDE.md style rules and ARCHITECTURE.md file placement rules.
- Does not invent new libraries outside TECH_STACK.md's approved list.
- Does not silently change the auth/permission model — flag it instead.

## Tester
- Writes/updates tests under `backend/src/test`.
- Always covers: happy path, unauthorized access, wrong-owner access (F2 trying to edit F1's private content, etc.), and public/private boundary.
- Runs `./gradlew :backend:test` and reports failures before handing back.

## Reviewer
- Checks a diff against: CLAUDE.md (style/build), ARCHITECTURE.md (file placement), TECH_STACK.md (no banned libraries), SRS.md (no scope creep beyond MVP features).
- Flags any change that weakens the public/private separation or exposes a signed Cloudinary URL without an auth check.
- Does not rewrite code itself — reports issues for the Coder role to fix.

## Switching roles
State the role explicitly at the start of a task, e.g. "Acting as Tester: adding permission tests for the new memory-edit endpoint."
