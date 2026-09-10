# Agentic Layer

## Draftable Actions (auto, low risk)
- Generate slide content from brief → ContentDraft
- Auto-assign theme based on tone/audience
- Score and validate generated content

## Executable After Approval (medium risk)
- Apply generated content to slides (user clicks "Use this")
- Apply a theme to a presentation

## Human-Only (critical)
- Delete a presentation
- Export (user action, not automated)

## Named Tools
| Tool | Risk | Boundary |
|---|---|---|
| generate_slide_content | low | Takes brief, returns structured JSON; no external calls |
| auto_assign_theme | low | Maps tone→theme_id from existing themes |
| apply_draft_to_slide | medium | Requires user approval; updates slide fields |
| delete_presentation | critical | Human-only; requires confirmation |

## Audit Log Fields
action, actor, target_table, target_id, timestamp, detail (jsonb)

## v1
- generate_slide_content + auto_assign_theme + apply_draft_to_slide

## Later
- Full audit log persistence
- Scheduled content refresh
- Multi-presentation content reuse