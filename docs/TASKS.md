# Tasks

## Sprint 1 — Core Engine (DB + Deck CRUD)
**Goal:** A user can create a deck, add/edit/delete/reorder slides, and see a live preview — no AI, no login.
- [ ] Create Supabase tables + seed data + RLS (permissive v1).
- [ ] Build `lib/data/` data-access layer for presentations + slides + templates.
- [ ] Deck list page (home) — shows seeded + created decks.
- [ ] Deck editor — create deck from form (title, topic, audience, tone).
- [ ] Slide editor — add/edit/delete/reorder slides; inline fields persist.
- [ ] Live slide preview pane.
- [ ] Template picker — switch font/colour across deck (seeded templates).
- [ ] Responsive sidebar nav (desktop) / hamburger (mobile).
- **Definition of Done:** User creates a deck manually, adds 5 slides by hand, applies a template, and sees the preview update — all persisted to the DB.

## Sprint 2 — AI Content Generation (**v1 functional milestone**)
**Goal:** User types a topic and gets a full structured deck.
- [ ] Build `lib/ai/generate_deck_content.ts` — strict JSON schema, retry on failure.
- [ ] Wire generate button → server action → save slides with ai_source/confidence/review_status.
- [ ] Low-confidence slides flagged in editor with review badge.
- [ ] Edit AI-generated content inline (same editor as manual).
- **Definition of Done:** User types "Photosynthesis for 8th grade", gets 8 slides with structured content + confidence scores, edits one bullet — the success scenario works end-to-end.

## Sprint 3 — Export + Polish
**Goal:** User can export the deck.
- [ ] Build `lib/export/` — generate PDF from current slides + template.
- [ ] Export button → server action → file download.
- [ ] Handle empty deck / empty slide states.
- [ ] Error + loading states on all screens.
- **Definition of Done:** User exports a finished deck as PDF and the file opens correctly.

## Sprint 4 — Lock It Down
**Goal:** Real users, per-user data, security pass.
- [ ] Add auth (Supabase auth) — login/signup.
- [ ] Replace permissive RLS with owner-scoped policies (`auth.uid() = user_id`).
- [ ] Templates remain shared read-only.
- [ ] Security pass: XSS, injection, npm audit, rate-limit AI.
- **Definition of Done:** Logged-out user sees demo deck; logged-in user sees only their own decks.

## Gantt
```
Sprint 1  ████  Core engine (DB + CRUD)
Sprint 2  ████  AI content generation
Sprint 3  ████  Export + polish
Sprint 4  ████  Lock-down (auth + RLS)
```