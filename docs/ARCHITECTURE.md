# Architecture

## Stack
- **Next.js (App Router)** — UI, server actions, routing.
- **Supabase (Postgres)** — database, RLS.
- **Vercel** — deployment.
- **AI content generation** — OpenAI API (server-side only, key never in frontend).

## Key User Action Flow
1. User enters topic + audience + tone on the home screen.
2. Server action calls AI module → returns structured slide content (JSON).
3. Content saved to `slides` table with `source`, `confidence`, `review_status`.
4. Default design template applied to the new presentation.
5. Deck editor renders slides in editable fields + live slide preview.
6. User edits slides, changes template, reorders — each change persists.
7. User exports → server generates PDF → download starts.

## Nav Shell
Desktop: persistent left sidebar (Decks, Templates, Export). Mobile: hamburger menu.

## Layer Order (what to build first)
1. **Data** — tables, seed data, data-access layer (`lib/data/`).
2. **App logic** — CRUD for presentations + slides, inline editing, reordering.
3. **Smart features** — AI content generation (`lib/ai/`), template application, export.

The core (create deck, edit slides, change template) runs without the AI — a user can build a deck manually and apply a template with zero AI calls. AI fills content faster but isn't required for the engine to work.

## Repo Structure
```
app/                    # routes + pages
  decks/                 # deck list + editor
  templates/             # template gallery
components/              # UI components (SlideEditor, DeckPreview, etc.)
lib/data/                # ALL DB reads/writes — single data-access layer
lib/ai/                  # AI content generation + confidence scoring
lib/export/              # PDF/PPTX generation
lib/actions/             # server actions
__tests__/               # tests beside code
```

## Module Map
| Module | Responsibility | Owns | Build order |
|---|---|---|---|
| decks | Presentation CRUD + deck editor | presentations table | 1st |
| slides | Slide content, reordering, inline edit | slides table | 1st (after decks) |
| templates | Design templates (font/colour/layout) | design_templates table | 2nd |
| content-gen | AI content generation per deck brief | slides AI fields | 2nd |
| export | Download deck as PDF | n/a (reads slides) | 3rd |