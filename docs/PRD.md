# PRD — PPT Slides Made Easy

## Problem
Creating presentation slides for lectures, classes, and business pitches is slow. Teachers, coaches, and executives spend hours researching content and fighting with design tools instead of presenting.

## Target User
Coaches, teachers, and top executives who need quality slide content with a clean layout — fast.

## Core Objects
- **Presentation** — title, audience, purpose, tone, slide_count
- **Slide** — order, layout_type, content blocks (heading, bullets, image_desc), notes
- **Theme** — font, primary/secondary/accent colours, layout template
- **ContentDraft** — AI-generated slide content (value + source + confidence + review_status)

## MVP (v1) — Must-Haves
- [ ] Create a presentation with title + audience + purpose
- [ ] Auto-generate slide-by-slide content from the presentation brief
- [ ] Pick or auto-apply a theme (font + colours + layout)
- [ ] Edit slide content inline (heading, bullets, notes)
 [ ] Reorder slides
- [ ] Export to a printable slide preview (rendered HTML, one slide per page)
- [ ] All above viewable without login (seeded demo data, no auth wall)

## Non-Goals (v1)
- Complex multi-element design (shapes, animations, transitions)
- Text-heavy slides with long paragraphs
- Real-time collaboration / multi-user editing
- Export to .pptx file format
- Image generation or stock photo search
- Billing / paid tiers

## Success Criteria
A coach types "Sales enablement for SaaS startup, 10 slides, persuasive" → the app generates 10 slides with headings + bullet points + speaker notes, applies a clean theme, and the coach edits content and exports a printable preview — in under 5 minutes, no design tool opened.