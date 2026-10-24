# Stage 4: Design

Design the app before building it: the design system, and the key screens drawn at
phone size in the app's own brand. This is the stage that makes the app look premium,
and the most filmable one.

## What to make

**The Design** shows, in the brand from stage 3:

1. **The design system** at a glance: colour tokens, the type scale at real sizes,
   spacing and corner radius, buttons (primary, secondary, pressed, disabled), a card,
   an input, a toggle, and the motion feel in one line.
2. **4–6 key screens** at iPhone size (393×852 points), with real copy from the plan:
   - the splash screen (the one sentence, one button),
   - the screen just before the magic moment,
   - **the magic moment itself** (the most important frame: give it the most care),
   - the paywall, if there is one,
   - the share card or share screen,
   - the main home screen a returning user sees.
3. A short line under each screen: what the user does there.

**Where to make it:**

- If the Artifact tool offers a **Design** artifact type (a canvas of artboards), use
  it: one artboard per screen plus one for the design system, following that type's
  instructions.
- Otherwise, make it as a page from the shell: a design-system section, then the
  screens side by side in phone frames (one column on narrow screens). Build each
  screen in HTML and CSS so it's crisp at any size.

**Design to the principles:** one big line and one obvious action per screen, real
words, generous space, and a magic-moment screen that looks like a celebration. Every
screen should be buildable in React Native with the stack below; don't design what
can't be built.

**Then write the code tokens:** create `constants/tokens.js` and `constants/Theme.ts`
from the approved design (structure below), so the build starts from the same values.

**Reel card:** the magic-moment screen, large, with the app name.

## Gate

Approve, or change something? Design changes are cheap now and slow once screens are
built.

---

# Design system reference

How the design becomes code. It keeps the app consistent and lets the whole look
change in one file. Written for Expo; the ideas carry over to Swift.

## The stack

```
Expo (managed) + Expo Router + TypeScript
├── NativeWind v4 + Tailwind v3    → layout, spacing, static colours
├── react-native-reanimated        → all motion (runs on the UI thread)
├── @shopify/react-native-skia     → backgrounds, glows, anything painterly (optional)
├── @expo-google-fonts/*           → fonts loaded at startup
├── expo-haptics                   → feedback on every primary action
└── react-native-safe-area-context → insets (never hard-code status bar heights)
```

Install packages with `npx expo install <pkg>` so versions match the Expo SDK.
**Choose boring versions:** for an app headed to App Review, pick stable releases with
a year of answered GitHub issues, not previews or nightlies. `babel-preset-expo` must
be a direct dependency, or the bundler can fail in a way `tsc` won't catch.

## Tokens: one source of truth

Put every colour, spacing step, radius and font name in `constants/tokens.js`. Use
CommonJS on purpose: `tailwind.config.js` runs in plain Node and can't import
TypeScript, but the app can `require` a `.js` file. Both read the same object, so they
never drift. `constants/Theme.ts` re-exports the tokens with types and adds the type
scale and motion presets.

Example tokens for a dark app (adapt to the brand):

```js
const STATIC = {
  // Translucent surfaces read as glass over the background, not painted boxes.
  glass:      'rgba(255,255,255,0.045)',
  glassHi:    'rgba(255,255,255,0.075)',
  glassEdge:  'rgba(255,255,255,0.10)',
  glassInner: 'rgba(255,255,255,0.14)',
  paper:      '#FBF7F2',                 // warm white; pure #FFF reads clinical
  paperMuted: 'rgba(251,247,242,0.78)',  // accessibility floor, do not lower
  paperFaint: 'rgba(251,247,242,0.55)',  // accessibility floor, do not lower
  ink:        '#04040A',                 // near-black; never pure #000
};
const SPACE  = { xs: 4, sm: 8, md: 16, lg: 24, xl: 32, xxl: 48, huge: 72, screenX: 24 };
const RADIUS = { sm: 12, md: 18, lg: 26, xl: 34, pill: 999 };
module.exports = { STATIC, SPACE, RADIUS };
```

A rounded element inside a rounded container uses `outer radius − padding`, or the
curves visibly disagree.

## Screens declare a mood, never a colour

Give the app an emotional arc as a few colour keyframes (night to dawn, calm to
celebratory, cool to warm). Each screen declares one number, its position on the arc,
and a `paletteAt(phase)` function blends the keyframes.

```js
const KEYFRAMES = [
  { at: 0.0, top: '#04040A', bottom: '#080814', accent: '#8B7CFF' },
  { at: 0.5, top: '#0D0711', bottom: '#210E24', accent: '#D083E8' },
  { at: 1.0, top: '#1A0C08', bottom: '#3E1503', accent: '#FFC66B' },
];
const PHASE = {
  welcome: 0.0, question: 0.45, magicMoment: 1.0,
  home: 0.7, settings: 0.2, // utility screens stay quiet
};
```

- Adding a screen is never a colour decision.
- Changing the whole mood of the app is one edit.
- Let only part of the screen travel (for example the bottom warms while the top stays
  dark). It stays classy and text stays readable.
- Tailwind holds static chrome only. The moving colours live in a `Screen` component
  that owns the background:

```tsx
/** Screen owns the background. Pass the phase, never a colour. */
export function Screen({ children, phase, animated = false }) { /* … */ }
```

## Typography

- **Two typefaces with jobs.** A display face for anything said *to* the user
  (questions, headlines). A UI face for the app talking about itself (buttons, labels,
  settings). Don't swap them to fit a layout.
- **Avoid the default everyone uses** (Inter is the house style of AI-built apps).
  Pick a face with character; a serif display face stands out in most categories.
- **Define the scale once** and never set a raw font size on a screen:

```ts
export const Type = {
  display: { fontFamily: FONTS.display, fontSize: 46, lineHeight: 50, letterSpacing: -1.2 },
  title:   { fontFamily: FONTS.display, fontSize: 36, lineHeight: 41, letterSpacing: -0.8 },
  body:    { fontFamily: FONTS.ui, fontSize: 17, lineHeight: 26 },
  caption: { fontFamily: FONTS.ui, fontSize: 15, lineHeight: 22 },
  button:  { fontFamily: FONTS.uiSemi, fontSize: 17, letterSpacing: 0.1 },
  eyebrow: { fontFamily: FONTS.uiMedium, fontSize: 11, letterSpacing: 2.4,
             textTransform: 'uppercase' as const },
} as const;
```

Large display text runs optically small and loose: size it up and pull letter-spacing
negative.

## Motion

Nothing moves linearly. Define it once:

```ts
export const Motion = {
  fast: 200, base: 320, slow: 620, cinematic: 1100,
  ease: [0.32, 0.72, 0, 1] as const,              // decelerates hard, no bounce
  spring:     { damping: 18, stiffness: 140, mass: 0.9 },
  springSoft: { damping: 22, stiffness: 90, mass: 1.1 },
} as const;
```

All motion in Reanimated. Haptics on every primary action. Animate only the screens
that earn it; save the big moment for the magic moment.

## Components

- In a small app, put the whole UI kit in `components/ui/index.tsx`. Split a component
  out only when it grows a real life of its own.
- **Fancy backgrounds must fail safe.** `Skia.RuntimeEffect.Make()` returns `null` on
  some devices; always fall back to a plain gradient from the same palette, never to a
  black screen. If static screens freeze an animated background, freeze each at a
  different moment so they don't look like wallpaper.
- **Match controls to the feeling.** Audio meant to feel like a live call shouldn't
  have a scrubber; it turns a person into a file.

## Accessibility is a gate

1. **WCAG AA on every screen:** 4.5:1 for body text, 3:1 for large text. Measure it;
   dark, glowing designs fail exactly where they look best.
2. **Compute contrast correctly:** linearise sRGB before applying
   `0.2126R + 0.7152G + 0.0722B`. The shortcut gives wrong answers on dark backgrounds.
3. When colour kills contrast, keep the hue and darken the luminance.
4. Text opacities are floors, not style. Comment them in the tokens file.
5. Keep a small `scripts/check-contrast` that reads the live tokens, checks every
   screen and exits non-zero on failure. Run it after any colour change.
6. **Never make one input the only way.** Voice-first screens need a visible "Type it
   instead". Autoplaying audio needs a visible way to stop it.
7. Set `accessibilityRole`, `accessibilityLabel` and `accessibilityState` on every icon
   button and toggle.
8. Trial terms on a paywall must be plainly readable (Apple requires it).

## Pitfalls no tool will catch

- **NativeWind drops the function form of `style` on `Pressable`.**
  `style={({ pressed }) => …}` renders with no styles at all. Use a plain style array
  and track pressed state with `onPressIn` / `onPressOut`. Comment why.
- **Reanimated worklets can't call ordinary JS functions** (string parsing, colour
  helpers). Compute values with `useMemo` on the JS side, then only read them in the
  worklet.
- **Absolute positioning ignores SafeAreaView padding.** Position from
  `useSafeAreaInsets().top`.
- **Skia colour uniforms:** pass `[r, g, b, 1]` (vec4), not vec3.
- **`pod install` fails** with "Unicode Normalization not appropriate for ASCII-8BIT":
  run it with `LANG=en_US.UTF-8`.
- **`expo-audio` metering** is −160 to 0 dB, not 0 to 1. Map it before driving visuals.
- **If you test with a simulation, check it against a real screenshot.** A wrong
  simulation hides real bugs.
