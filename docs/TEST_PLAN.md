# Test Plan

## Success Scenario (v1)
1. Open the app — see the deck list with seeded demo deck ("Photosynthesis").
2. Click "New Deck" — enter title "Climate Change", topic "climate science", audience "high school", tone "classroom lecture".
3. Click "Generate" — wait for loading state — 8 slides appear with content + confidence badges.
4. Click a slide — edit the body content inline — save persists.
5. Open template picker — switch to "Boardroom Blue" — all slides update colours.
6. Click "Export" — PDF downloads and opens.

## Empty States
- **No decks**: Deck list shows "No decks yet — create one to get started" with a CTA button.
- **Empty deck**: Editor shows "This deck has no slides yet — add one or generate from a topic."
- **Empty slide body**: Preview shows "Click to add content."

## Error States
- **AI generation fails**: Show "Couldn't generate content — try again or add slides manually." Retry button. Manual add still works.
- **AI returns invalid JSON**: Retry once, then fall back to manual entry. No crash.
- **DB write fails**: Inline save shows "Save failed — retry" on the field.
- **Export fails**: "Export failed — try again" toast.

## Loading States
- **Generating**: Button shows spinner + "Generating slides…" — other UI remains interactive.
- **Saving**: Field shows subtle "Saving…" then "Saved".
- **Exporting**: "Building your PDF…" spinner.

## Permissions
- v1: all actions work without login.
- Lock-down: logged-out user sees demo deck only; cannot create decks without auth.