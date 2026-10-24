# Stage 7: Build

Build the app milestone by milestone from `docs/BUILD-PLAN.md`, matching the Design and
Storyboard.

## Before the first milestone: check the tools

Check, and explain anything missing in plain words:

- Node.js 20 or newer (`node -v`).
- On a Mac, **Xcode** from the App Store gives an iPhone simulator on screen (no paid
  developer account needed). Optional but very useful.
- The free **Expo Go** app on their phone.

## Scaffold

```bash
npx create-expo-app@latest .     # in the project folder; TypeScript + Expo Router
```

Install packages with `npx expo install <package>` so versions match the Expo SDK. Then
set up the design system from stage 4 before any screens: `constants/tokens.js`,
`constants/Theme.ts`, fonts, motion presets and the `Screen` component.

Show them how to run it on their phone: `npx expo start`, then scan the QR code with
the iPhone camera (Expo Go opens it). Celebrate the first time it appears.

## Building each milestone

1. Say what this milestone is and what they'll be able to try at the end.
2. Build it. Match the Design and Storyboard: the same words, layout and order. Don't
   add anything that isn't in the plan.
3. Verify (below).
4. Have them try it on their phone. Fix what they find.
5. Update `progress.json` (`milestonesDone`), append to `docs/JOURNEY.md`, update the
   Journey page, and give the reel moment for that milestone.
6. Ask before starting the next milestone.

Build the interdependent core (the data, the main flow, the magic moment) in one
session if you can. Polish and copy passes can be separate sessions.

## Verify after every change

```bash
npx tsc --noEmit                 # types
npx expo export --platform ios   # the real bundler; catches config and Babel problems tsc can't
```

Before calling a milestone done, run it in the simulator or Expo Go and **screenshot
every changed screen**. Compare with the Design. Fix what the screenshots show.
Typechecking clean is the start of verified, not the end. When you build something you
can't see (an animation, a shader, a generated image), build a way to see it.

## Supabase steps (milestone 4, if needed)

1. The user creates a project at supabase.com and gives you the project URL and anon
   key. Put them in `.env` as `EXPO_PUBLIC_SUPABASE_URL` and
   `EXPO_PUBLIC_SUPABASE_ANON_KEY`, and later also in `eas.json` (see stage 8: `.env`
   doesn't reach cloud builds).
2. Write the schema as SQL migrations in `supabase/migrations/`, with row-level
   security on every table. The user can run them in the Supabase SQL editor, or with
   the Supabase CLI if they've installed it.
3. AI and other secret-holding calls go in Edge Functions; set their keys as Supabase
   secrets, never in the app.

## Polish milestone checklist

- Haptics on every primary action; a bigger one on the magic moment.
- Motion uses the shared presets; nothing linear.
- Empty, loading and error states for every screen, written in the app's voice.
- Copy pass: every screen has one big line and one obvious action.
- Accessibility: contrast check, labels on icon buttons, a typed alternative to voice.
- Permission prompt wording in `app.json` is final (it only changes with a new build).

## Reel moments

First run on their phone; the magic moment working; before/after of the polish pass.
See [reel-kit](reel-kit.md).
