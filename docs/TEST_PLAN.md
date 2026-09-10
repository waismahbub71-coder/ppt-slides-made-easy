# Test Plan

## v1 Success Scenario (manual)
1. Open app — see demo presentations in sidebar (no login)
2. Click "New Presentation" → enter: title "Q3 Investor Pitch", audience "Investors", purpose "Fundraise", tone "persuasive", slide_count 8
3. Click "Generate Slides" → 8 slides appear with headings + bullets + notes
4. Click a slide → edit heading and a bullet → changes persist on refresh
5. Drag slide 3 to position 1 → order updates
6. Pick "Corporate Bold" theme → font + colours applied to all slides
7. Click "Export" → printable view opens, one slide per page
8. Verify: all data visible after refresh

## Empty States
- No presentations → show "Create your first presentation" CTA
- No slides in a presentation → show "Add or generate slides"
- No themes → fallback to default theme

## Error Cases
- AI generation fails → show error + retry button
- DB write fails → toast with error, form stays populated
- Invalid slide_count (0 or >30) → validation message, no submission
- Network offline → graceful error, no silent failure

## AI Output Validation
- Missing heading → flag slide, user edits manually
- Empty bullets array → flag, user adds bullets
- Confidence < 0.5 → marked "review needed", not auto-applied
- Malformed JSON from model → retry once, then show raw brief for manual entry