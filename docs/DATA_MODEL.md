# Data Model

## presentations
| Field | Type | Notes |
|---|---|---|
| id | uuid | PK, default gen_random_uuid() |
| user_id | uuid | nullable (owner-scope at lock-down) |
| title | text | deck title |
| topic | text | raw topic input |
| audience | text | e.g. "8th grade students" |
| tone | text | e.g. "classroom lecture", "investor pitch" |
| template_id | uuid | FK → design_templates, nullable |
| created_at | timestamptz | default now() |

RLS: v1 permissive (read+write for all). Lock-down: `auth.uid() = user_id`.

## slides
| Field | Type | Notes |
|---|---|---|
| id | uuid | PK |
| presentation_id | uuid | FK → presentations |
| slide_number | int | order in deck |
| title | text | slide heading |
| body_content | text | bullet content (plain text) |
| speaker_notes | text | nullable |
| layout_type | text | default 'bullet' (options: bullet, title_only, two_column) |
| ai_source | text | nullable — model name if AI-generated |
| ai_confidence | numeric | nullable — 0..1 |
| ai_review_status | text | default 'unreviewed' (unreviewed / approved / rejected) |
| created_at | timestamptz | default now() |

RLS: v1 permissive. Lock-down: owner-scoped via presentation.

## design_templates
| Field | Type | Notes |
|---|---|---|
| id | uuid | PK |
| name | text | e.g. "Boardroom Blue" |
| font_pairing | text | e.g. "Inter / Merriweather" |
| primary_color | text | hex |
| accent_color | text | hex |
| bg_color | text | hex |
| layout_type | text | default 'bullet' |
| created_at | timestamptz | default now() |

RLS: v1 permissive (read for all, write for all). Lock-down: templates are shared read-only; only owners create.

## Relationships
- presentation 1—* slides (cascade delete)
- design_templates 1—* presentations (a deck uses one template)