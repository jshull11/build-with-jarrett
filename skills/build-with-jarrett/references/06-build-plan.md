# Stage 6: Build plan

Turn the plan, design and storyboard into the order you'll build in. The result is
`docs/BUILD-PLAN.md` (for you) and the **Build plan page** (for the user).

## Decide the technical shape

Make these calls yourself and explain each in one plain sentence.

**App:** Expo (React Native) + Expo Router + TypeScript, with the design-system stack
from stage 4. Runs on iPhone and Android, testable in Expo Go.

**Accounts: every app gets Sign in with Apple.** It's the one sign-in method for every
Build with Jarrett app: one tap, no password, and Apple's privacy rules are already met.
- Use `expo-apple-authentication` for the button and native sheet, and Supabase Auth
  (`signInWithIdToken({ provider: 'apple', token })`) to turn it into a user. Pass a
  hashed nonce.
- **Place it after the magic moment**, usually right before or after the paywall, or when
  the user does something worth saving ("Save your results"). Never before the magic
  moment. Until then the app works on a device ID, and signing in moves that data onto
  the account.
- Ask for name and email only on the first sign-in (Apple sends them once). Store them
  right away. Honour "Hide My Email".
- **Account deletion is required** by App Review: a findable "Delete account" in
  Settings that deletes the user's server data and revokes the Apple token.
- Don't add Google, email or phone sign-in in v1. Android users get Apple's web flow
  (or the device-ID mode) until there's a real need.
- Use Apple's own button (black, white or outlined), never a custom-drawn one.

**Backend:** every app has accounts, so every app uses **Supabase**:

- **Auth:** Sign in with Apple, as above. Row-level security uses `auth.uid()`.
- **Database:** Postgres tables with **row-level security on every table**. Write the
  data model as a short table list (table, key columns, who can read and write it).
- **Storage:** for photos, audio or files.
- **Edge Functions:** for anything that needs a secret, especially AI calls. AI keys
  never ship inside the app.
- The user creates the Supabase project themselves at supabase.com (free tier) and
  pastes in the project URL and the anon key. Explain that the anon key is designed to
  be public; the service role key must never go in the app.

If the app needs none of that, keep everything on the device (AsyncStorage or SQLite)
and say so.

**AI features:** put per-user daily limits on every paid AI call from day one, and show
a friendly message when someone hits one. If personal data goes to AI services, the app
needs a **permanent, findable** disclosure screen (for example in Settings) and consent
before the first AI call. App Review checks this, and a one-time screen the reviewer
never sees doesn't count.

**Payments:** RevenueCat for subscriptions (works with Apple in-app purchase), set up
after the core works. Paywall placement as in the storyboard.

**Analytics:** track the funnel from the first build: `app_opened`, `onboarding_step`
(with the step), `magic_moment_reached`, `shared`, `paywall_shown`, `purchased`, and
day-2 return. A Supabase table is enough to start; a product analytics tool (e.g.
PostHog) is fine too.

**Notifications:** `expo-notifications`. Local reminders first; push only if the app
needs messages between users.

## Milestones

Break the build into 5–8 milestones. Each one ends with something the user can try on
their phone. A typical order:

1. **Skeleton:** project created, design tokens, fonts, the `Screen` component, the
   splash screen running in Expo Go.
2. **The magic moment, end to end** (rough is fine): the core feature working.
3. **Onboarding flow** as storyboarded, with the clock checked.
4. **Backend and Sign in with Apple:** Supabase project, schema with RLS, the Apple
   button after the magic moment, device data moved onto the account, and Delete account.
5. **Main screens** for returning users.
6. **Sharing** (share card, link, invite).
7. **Paywall and analytics.**
8. **Polish:** haptics, motion, sound, empty states, error states, copy pass,
   accessibility pass.

For each milestone list: what gets built, the files (roughly), how to test it, and
what "done" looks like.

## The Build plan page

From the shell, in the brand:

1. The milestones as a vertical track, each with "what you'll be able to try".
2. The technical shape as a simple diagram: app → (Supabase: auth, database, storage,
   functions) → outside services (AI, payments). Plain labels.
3. The data model as a small table, if there's a backend.
4. Things the user will need to do, with when: create a Supabase project (milestone 4),
   turn on the Sign in with Apple capability for the bundle ID and the Apple provider in
   Supabase Auth (milestone 4),
   Apple Developer account ($99/year, before stage 8), RevenueCat account (milestone 7).
5. Analytics events as a funnel graphic.
6. Reel card: "The roadmap", the milestone track.
7. Footer with the brand mark.

## Gate

Approve, or change something? Also ask: ready to start building now, or next session?

## Reel moment

The roadmap. See [reel-kit](reel-kit.md).
