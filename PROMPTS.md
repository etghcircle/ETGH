# PROMPTS.md — Reusable Prompt Templates

Use these instead of open-ended requests so the AI's output stays scoped and consistent.

## Add a new backend endpoint
```
Add a Ktor route `[METHOD] [PATH]` in routes/[FileName].kt.
- Auth requirement: [none / any of the 4 accounts / Admin only / owner-only]
- Request body: [fields]
- Response: [fields]
- Must reuse existing PermissionService for visibility checks — do not write new auth logic inline.
- Add a test in the matching *Test.kt file covering: authorized access, unauthorized access, and wrong-owner access.
```

## Add a new memory type/field
```
Add [field name] to the Memory model (models/Memory.kt) and its Exposed table.
- Type: [type]
- Nullable: [yes/no]
- Update MemoryRepository, MemoryService, and the DTO used by the frontend.
- Do not change existing field names or the public/private enum.
```

## Add/modify a Compose UI screen
```
Build a Compose screen for [purpose] in frontend/composables/[Name].kt.
- Data comes from [endpoint].
- Must visually distinguish public vs private items (e.g. a lock icon on private).
- Follow the existing design tokens in ARCHITECTURE.md — do not introduce a new color palette or font.
```

## Permission/auth change
```
Modify permission logic for [scenario].
- Current rule: [what it is now]
- New rule: [what it should be]
- Check DECISIONS.md first — do not change something that was already decided against.
- Update permission tests to reflect the new rule.
```

## Bug fix
```
Fix: [bug description]
- Reproduce steps: [steps]
- Expected: [expected behavior]
- Do not refactor unrelated code in the same change.
```
