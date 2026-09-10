# Intelligence Layer

## Messy Inputs
Raw user brief: a topic string, audience string, and tone string — unstructured, varying length.

## Auto-Structure Schema
AI returns this JSON per deck:
```json
{
  "deck_title": "Photosynthesis",
  "slides": [
    {
      "title": "What is Photosynthesis?",
      "body_content": "Plants convert sunlight into energy\nChlorophyll captures light\nProduces glucose and oxygen",
      "speaker_notes": "Start with the big idea — plants make their own food.",
      "layout_type": "bullet"
    }
  ],
  "confidence": 0.92
}
```

## Events Tracked
- `deck.generated` — content created, confidence + source stored per slide.
- `slide.edited` — user manually changed AI content (flags review).
- `template.applied` — design template changed.

## Scoring Rules (rule-based, v1)
- **Confidence**: AI model self-report (0–1), stored per slide. Below 0.7 → `review_status = 'unreviewed'` and surfaced with a visual flag.
- **Content quality**: `≥3 bullets and ≤6 bullets = pass`; `<3 or >6 = flag for trim`.
- **Readability**: body_content ≤ 120 chars per slide → pass; else flag.

## What Gets Ranked
- Slides by review_status: `unreviewed` surfaced first in a review queue.
- Templates by usage (default = most-used template for the audience/tone).

## v1 vs Later
- **v1**: one-shot AI generation, per-slide confidence, manual review flags.
- **Later**: iterative refinement prompts, multi-pass structuring, per-slide layout suggestions, image search.