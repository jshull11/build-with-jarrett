# HANDOFF.md template

Fill this in with the user in Step 1. Delete sections that don't apply. Write
outcomes, not implementations: "the result appears within 10 seconds and the wait
feels intentional", not "use a spinner".

```markdown
# [App Name] — Handoff

## The one sentence
[What it does, for whom. Under ten words if possible. Used word for word on the
first screen, the first App Store screenshot and every ad.]

## Who it's for and the feeling
[The person, and the core desire it serves: being liked, looking cool, feeling
better, knowing more. How they feel at the magic moment.]

## The core loop
[Day 1: what the user does. Day 2: what brings them back. 3–6 bullets.]

## The magic moment (within ~60 seconds)
[The moment, and how we make it shocking and delightful: haptics, motion, sound.
If something slow comes before it, how we fill the wait.]

## The share moment
[What the user shows a friend, what the friend sees, and what the friend does next.]

## v1 screens, in order
1. Splash — the one sentence and one button
2. ... — [what this screen must do]
3. ...
[If a screen isn't listed, it's not in v1.]

## Permissions, and when we ask
- Notifications — [the moment it makes sense, and the screen that sets it up]
- [Others, e.g. camera, microphone, location]

## Features
### In v1
- [feature] — [why it must be in v1]
### Deliberately NOT in v1 (the cut list)
- [feature] — [why it waits, and what would make us build it]

## Hard rules
- Never fake users, activity, messages, reviews or counts.
- [e.g. "no account needed before the magic moment", "free users never trigger the
  expensive AI call", "works offline"]

## Design register
[Three adjectives. One anti-reference ("NOT another white minimal wellness app").
Two or three apps whose feel we want ("celebrations like Duolingo, calm like Calm").]

## Money
[Free, soft paywall or hard paywall. What's free forever, what's paid. Weekly,
monthly or annual. Web checkout or Apple only.]

## Open questions (the user decides these, not Claude)
- OPEN: [thing not decided yet]
```

## Rules for a good handoff

1. **The one sentence comes first.** If you can't write it, the app isn't ready.
2. **The cut list matters as much as the feature list.** Every idea that waits goes
   on it, so it's a recorded decision instead of something re-decided every session.
3. **Hard rules are gates**, not preferences.
4. **Screens in order become the file structure** almost one to one.
5. **Open questions stay open** until the user decides. Never bake in a guess.
