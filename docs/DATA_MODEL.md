# Data Model

## presentations
| Field | Type |
|---|---|
| id | uuid pk |
| user_id | uuid nullable |
| title | text |
| audience | text |
| purpose | text |
| tone | text |
| slide_count | int |
| theme_id | uuid nullable fk -> themes |
| created_at | timestamptz |

## slides
| Field | Type |
|---|---|
| id | uuid pk |
| presentation_id | uuid fk -> presentations |
| order_index | int |
| layout_type | text (default 'title_bullets') |
| heading | text |
| bullets | text[] (nullable) |
| notes | text (nullable) |
| created_at | timestamptz |

## content_drafts
| Field | Type |
|---|---|
| id | uuid pk |
| slide_id | uuid fk -> slides |
| value | jsonb |
| source | text |
| confidence | numeric |
| review_status | text default 'unreviewed' |
| created_at | timestamptz |

AI field: `value` stores generated heading + bullets + notes. `source` = model name. `confidence` = 0–1. `review_status`: unreviewed / approved / rejected.

## themes
| Field | Type |
|---|---|
| id | uuid pk |
| name | text |
| font | text |
| primary_colour | text |
| secondary_colour | text |
| accent_colour | text |
| layout_template | text |
| created_at | timestamptz |

## RLS
All tables: permissive v1 policies (read/write open for demo). Lock-down sprint replaces with `auth.uid() = user_id` owner policies.