# Agentic Layer

## Draftable Actions (low risk — auto)
- **Generate slide content** — AI drafts title + body + notes from brief. Risk: low. Stored with confidence; low-confidence routed to review queue.
- **Suggest template** — pick a template matching audience/tone. Risk: low. User can override.

## Executable After Approval (medium risk)
- **Apply template to all slides** — changes font/colour/layout across deck. Risk: medium. User confirms before applying.
- **Export deck** — generates PDF/PPTX file. Risk: medium. User clicks export; server builds file.

## Human-Only Actions (high risk)
- **Delete presentation** — irrecoverable. Risk: high. Always user-initiated with confirm.
- **Bulk regenerate all slides** — overwrites manual edits. Risk: high. Confirm + shows diff.

## Named Tools
| Tool | Risk | Boundary |
|---|---|---|
| `generate_deck_content` | low | input: topic/audience/tone → output: structured JSON |
| `suggest_template` | low | input: audience/tone → output: template_id |
| `apply_template` | medium | input: presentation_id + template_id → updates presentation |
| `export_deck` | medium | input: presentation_id → returns file URL |
| `delete_presentation` | high | input: presentation_id → cascade delete |

## Audit Log Fields
Every agentic action logs: `id`, `tool_name`, `presentation_id`, `user_id` (nullable v1), `input_summary`, `output_summary`, `status`, `created_at`.

## v1 vs Later
- **v1**: generate content, apply template, export, delete — all user-triggered.
- **Later**: auto-suggest next slides, auto-rebalance content, scheduled deck generation.