# Stage 2: The Plan page

Turn the interview into two things: the **Plan page** (a visual page they'll be proud
to show) and `HANDOFF.md` (the written source of truth you'll build from). Both say the
same thing.

## 1. Write HANDOFF.md

Use [templates/handoff-template.md](../templates/handoff-template.md). Also create:

- `CLAUDE.md` in the project root (contents below), so every future session follows
  the plan.
- `docs/JOURNEY.md`, the build log, with a first entry.

```markdown
# [App Name]

- This app is built with the build-with-jarrett skill. At the start of every session,
  read .buildwithjarrett/progress.json and continue the current stage.
- Read HANDOFF.md before any product decision. Build only what it lists; new ideas go
  on its cut list and get flagged to me.
- After every code change run `npx tsc --noEmit`, and `npx expo export --platform ios`
  before calling anything done. Screenshot changed screens.
- Append to docs/JOURNEY.md at the end of each session.
- Never start an App Store / EAS build or submission, or anything that costs money,
  without my go-ahead.
- Never commit secrets. Real API keys live on the server, never in the app.
- Taste, brand, copy and pricing are my calls: suggest, don't decide.
- Never fake users, activity, messages, reviews or counts.
```

## 2. Make the Plan page

Build it from [templates/page-shell.html](../templates/page-shell.html), using the
shell's neutral defaults (the app has no brand yet). Sections, in this order:

1. **The one sentence**, huge, as the page's hero. Above it, small: the working name.
2. **Who it's for and the feeling.** One short line each, plus a simple persona chip
   ("Maya, 24, wants to…").
3. **The magic moment**, as a 60-second timeline: a horizontal bar from 0s to 60s with
   marks for each step up to the moment, so the speed is visible.
4. **The core loop**, drawn as a loop: day 1 action → reward → reason to come back →
   day 2. Arrows, not paragraphs.
5. **The share moment**: a phone-sized card showing what gets shared, and an arrow to
   what the friend does.
6. **v1 screens**: small labelled phone outlines in order (just names and one line
   each; the real design comes in stage 4).
7. **In v1 / Not yet**: two columns. The cut list is as visible as the feature list.
8. **Money**: free / paid, the price idea, where the paywall sits.
9. **Risks and open questions**: short, honest, with who decides.
10. **Reel card** (9:16), from reel-kit: "My app plan" with the one sentence.
11. Footer with the brand mark.

Keep text short everywhere. If a section needs a paragraph, it needs a diagram instead.

## 3. Make the Journey page

After the Plan page, create the Journey page: the app's working name, the one sentence,
and the ten stages as a vertical track with status (done / now / next) and a link to
each page made so far. Update it at the end of every later stage.

## Gate

Show the Plan page link and a two-line summary. Ask: approve, or change something?

## Reel moment

The plan reveal. See [reel-kit](reel-kit.md).
