# PRD — Slides Made Easy

## Problem
Creating a good presentation takes too long — researching content, structuring slides, and designing layouts are three separate jobs done in three separate tools.

## Target User
Teachers, coaches, and top executives who need a clean presentation fast and currently lose hours to design tools or heavy research.

## Core Objects
- **Presentation** — a deck with a title, topic, audience, and tone.
- **Slide** — one slide: title, body content, speaker notes, layout type, slide number.
- **Design Template** — a reusable pairing of fonts, colours, and layout style.

## MVP (v1) — Checklist
- [ ] Enter a topic + audience + tone → generate a full slide deck (content per slide).
- [ ] AI-generated content stored with source, confidence, review_status.
- [ ] Pick / change a design template (font + colour + layout) applied across all slides.
- [ ] Edit any slide's title, body, and notes inline — persists to DB.
- [ ] Add, reorder, and delete slides.
- [ ] Preview the deck as a clean slide view.
- [ ] Export to a downloadable format (PDF or PPTX stub).
- [ ] All screens viewable without login (seeded demo deck on first load).

## Non-goals (v1)
- Complex multi-column or animated layouts.
- Text-heavy slides (keep slides lean — max ~5 bullets).
- User accounts / login / per-user isolation (later sprint).
- Real-time collaborative editing.
- Image generation or stock-photo search.

## Success Criteria
A teacher types "Photosynthesis for 8th grade" with tone "classroom lecture", gets a 8-slide deck with correct structured content and a clean applied design, edits one bullet, changes the colour template, and exports a PDF — all without leaving the app and without signing in.