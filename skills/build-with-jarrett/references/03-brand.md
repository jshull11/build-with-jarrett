# Stage 3: Name, icon and brand

Give the app an identity before designing screens. The result is the **Brand page**,
and its palette and fonts are used by every page and screen after this.

## Name

1. Suggest **five names**, then narrow to three favourites with the user. Good names are
   short, easy to say out loud, easy to spell after hearing them, and hint at the
   feeling or the one sentence. Avoid names that need explaining.
2. For each finalist, the user should check before falling in love with it:
   - **App Store:** search the name in the App Store app. A different app with the same
     or a near-identical name is a problem. The real test is reserving it in App Store
     Connect (stage 8), which they can do early if they already have a developer account.
   - **Instagram / TikTok handle** availability, if they'll post about it.
   - **Domain**, if they want a website (optional).
   Tell them these checks are theirs to do; you can't verify availability yourself
   unless you have a tool for it.
3. The App Store name and the name under the icon on the home screen can differ
   slightly ("Bloom: Daily Gratitude" vs "Bloom").

## Palette

- Four to six named colours: background, surface, text, muted text, one accent, and an
  optional second accent. Pick deliberately for the feeling, not from defaults.
- Decide light, dark or both. Pure white and pure black rarely look premium; use a warm
  or cool off-white and a near-black.
- **Avoid the overused AI looks** unless the user asks for one: cream with a terracotta
  accent, near-black with one neon pop, a purple-to-blue gradient on white.
- Check contrast: body text at least 4.5:1 on its background, large text 3:1.

## Type

- Two typefaces with jobs: a **display** face for anything said to the user (headlines,
  questions) and a **UI** face for buttons, labels and settings. Both from Google Fonts,
  so they work on the pages and in the app (`@expo-google-fonts/*`).
- Avoid the default every AI-built app uses (Inter). A face with character is the
  cheapest way to stand out.

## Icon

- Three icon concepts, each described in one line and drawn on the Brand page as a
  rounded-square tile (SVG or CSS: simple shapes, the accent colour, no fine detail; it
  has to read at 60px).
- Note: the final icon file is a 1024×1024 PNG without transparency. If the user wants
  to commission or generate a polished one, the chosen concept is the brief.

## Mood

Three to five words and a short line on how the app should feel in the hand (motion,
sound, haptics). Example: "Calm, warm, slow. Motion settles like breath. Soft haptic on
every save."

## The Brand page

Built from the shell, **now in the app's own colours and fonts**:

1. The name, set huge in the display face, with the one sentence under it.
2. The three name finalists with the chosen one marked, and the checks still to do.
3. The palette as large swatches with names and hex values, plus a contrast note.
4. The type pairing shown at real sizes (a headline, a body line, a button).
5. The three icon concepts as tiles, with the chosen one marked.
6. The mood line.
7. A mini "screen preview": a phone frame with the splash screen in the new brand.
8. Reel card: the name reveal.
9. Footer with the brand mark.

Save the palette and fonts into `.buildwithjarrett/progress.json` → `brand`.

## Gate

Approve, or change something? Colour and name changes are cheap now and expensive later.

## Reel moment

The name and icon reveal. See [reel-kit](reel-kit.md).
