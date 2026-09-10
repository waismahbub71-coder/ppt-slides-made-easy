# Intelligence Layer

## Messy Input
User provides a free-text brief: title, audience, purpose, tone, slide_count.

## Auto-Structure Schema
```json
{
  "slides": [
    {"heading": "Market Opportunity", "bullets": ["$50B TAM", "12% YoY growth"], "notes": "Open with the market size to frame urgency."}
  ]
}
```

## Events Tracked
- `content.generated` — AI produced slide content
- `content.approved` — user accepted draft
- `content.edited` — user modified AI content
- `theme.applied` — theme chosen for presentation

## Scoring (rule-based v1)
- Confidence = 1.0 if all slides have heading + >=1 bullet, else proportional
- Below 0.5 → flagged for human review, not auto-applied
- Each slide checked: heading non-empty, bullets <= 5, notes present

## v1
- Single-pass generation from brief → structured slides
- Per-slide validation (heading + bullets + notes)
- Low-confidence drafts flagged, editable

## Later
- Section-aware generation (intro/body/closing)
- Audience-tuned tone adjustment
- Content quality scoring across slides