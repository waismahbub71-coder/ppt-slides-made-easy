# Security

## Secret Handling
- OpenAI API key stored in server-side env (`OPENAI_API_KEY`). Never exposed to the client. All AI calls happen in server actions or `lib/ai/`.
- Supabase service key in server env only; anon key in client is safe.
- No secrets in `.env.local` committed to repo.

## Permission Model
- **v1 (demo-first)**: permissive RLS — all tables readable/writable by anyone so the app works without login. Seeded demo decks visible to all.
- **Lock-down sprint**: replace with owner-scoped policies (`auth.uid() = user_id`). Presentations + slides visible only to their owner. Templates remain shared read-only.

## Approved-Tools Rule
- Only named, server-side tools in `lib/ai/` and `lib/actions/` may call external services.
- No raw `eval`, `exec`, or arbitrary HTTP calls from the client.
- AI calls use a single `generate_deck_content` function with a strict output schema; invalid output is retried once then routed to manual entry.

## Audit Principle
Every meaningful action (generate, apply template, export, delete) is logged with tool name, input summary, and timestamp.

## What Could NOT Be Verified
- Rate limiting on AI generation (add in lock-down sprint).
- XSS on user-entered slide content — v1 renders as plain text; if rich text added later, needs sanitisation.
- npm audit — run before lock-down sprint.