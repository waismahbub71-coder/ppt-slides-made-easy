# Tasks

## Sprint 1 — Database + Core Presentation CRUD
**Goal:** Presentations + slides + themes tables, seeded, viewable without login.
- [ ] Create Supabase tables (presentations, slides, themes, content_drafts) with permissive RLS + seed data
- [ ] `lib/data/` — typed access functions for all CRUD
- [ ] Presentations list page (sidebar shell, seed data visible)
- [ ] Create presentation form (title, audience, purpose, tone, slide_count)
- [ ] Presentation detail with slide list
- [ ] Inline slide editor (heading, bullets, notes — editable, persists)
- [ ] Slide reorder (drag or up/down)
- [ ] Theme picker — apply theme to presentation
- [ ] Printable export view (one slide per page)
**DoD:** A user creates a presentation, adds/edits/reorders slides, picks a theme, and exports a printable preview — all without logging in.

## Sprint 2 — AI Content Generation (v1 functional milestone)
**Goal:** Brief → auto-generated slides working end-to-end.
- [ ] `lib/ai/` — generate_slide_content server function
- [ ] "Generate slides" button on presentation create
- [ ] ContentDraft storage with value+source+confidence+review_status
- [ ] Low-confidence flagging + human review UI
- [ ] Auto-assign theme based on tone
- [ ] Slide preview with theme styling (font + colours)
**DoD:** User types a brief, clicks generate, gets populated slides with correct theme — editable and exportable.

## Sprint 3 — Polish + Edge Cases
**Goal:** Handle empty/error/loading states everywhere.
- [ ] Loading skeletons on all async ops
- [ ] Empty states (no presentations, no slides)
- [ ] Error boundaries + retry on AI failure
- [ ] Validation on form inputs
- [ ] Theme styling applied to printable export
**DoD:** Every screen handles loading, empty, and error gracefully; no dead-ends.

## Sprint 4 — Lock It Down
**Goal:** Auth + owner-scoped data isolation.
- [ ] Login/signup (email + OAuth)
- [ ] Replace permissive RLS with owner-scoped policies
- [ ] user_id populated on all new rows
- [ ] Rate-limiting on AI calls
- [ ] Security pass (injection, XSS, PII, prompt-injection)
**DoD:** Logged-in user sees only their presentations; anonymous user can still see a demo but cannot edit.

## Gantt
```
S1: ████████ DB + CRUD + slide editor + export
S2: ████████ AI generation + theme styling
S3: ████ Edge cases + polish
S4: ████ Auth + RLS lockdown + security
```

**First works end-to-end:** end of Sprint 2 (v1 functional milestone)