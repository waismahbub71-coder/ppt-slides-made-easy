# Architecture

## Stack
- **Next.js** (App Router) + **Supabase** (Postgres + RLS) + **Vercel** deploy
- AI: OpenAI API (server-side only)

## Core Flow (one user action)
1. User creates a presentation brief (title, audience, purpose, slide_count)
2. Server calls AI to generate slide-by-slide content → stored as ContentDraft rows
3. User picks / AI auto-assigns a Theme (font + colours + layout)
4. Slides render in editable preview — user edits headings/bullets/notes inline
5. User reorders slides, exports printable preview
6. Every save persists to Supabase; refresh shows same state

## Nav Shell
Persistent left sidebar on desktop (Presentations, Themes), collapses to hamburger on mobile. Current section highlighted.

## Build Order
1. Database tables + RLS (permissive v1) + seed data
2. Data-access layer (`lib/data/`) — all DB reads/writes
3. Presentation CRUD UI (create, list, edit slides)
4. Inline slide editor + reorder
5. Theme picker + printable export
6. AI content generation (server-side `lib/ai/`)
7. Auth + owner-scoped RLS (later sprint)

## Why Core Works Without AI
Slides can be created and edited manually. AI auto-fill is an enhancement; the app is fully functional with blank slides typed by hand.

## Repo Structure
```
src/
  app/
    (presentations)/  — list + editor pages
    (themes)/         — theme browser
    components/        — shared UI
  features/
    presentations/    — components + logic
    slides/           — slide editor + reorder
    themes/           — theme picker
  lib/
    data/             — all DB access (one place)
    ai/               — content generation
    server/           — server actions
  test/               — beside code
```

## Module Map
| Module | Owns | Data | Build Order |
|---|---|---|---|
| presentations | list + create + brief | presentations table | 1 |
| slides | edit + reorder + render | slides table | 2 |
| themes | pick + apply | themes table | 3 |
| ai-content | generate content | content_drafts table | 4 |
| auth | login + RLS lockdown | user_id scoping | 5 |