# Security

## Secret Handling
- OpenAI API key stored in environment variables (server-side only)
- Never exposed in frontend code or client bundles
- Supabase service key server-side only; anon key in NEXT_PUBLIC_

## Permission Model
- v1: permissive RLS (demo works without login)
- Lock-down sprint: owner-scoped (`auth.uid() = user_id`) on all tables
- AI inherits the calling user's permissions — no elevated access

## Approved Tools Rule
- Only named server-side functions interact with AI or DB
- No raw `eval`, no arbitrary code execution
- Structured errors: retryable vs terminal, human-readable reason

## Audit Principle
Every content generation, theme application, and slide edit is logged. Admin can trace who did what and when.

## What Could NOT Be Verified (v1)
- Rate-limiting on AI calls (add in lock-down sprint)
- PII scrubbing on user briefs (assess in later sprint)
- Prompt-injection hardening (basic validation in v1, full pass later)