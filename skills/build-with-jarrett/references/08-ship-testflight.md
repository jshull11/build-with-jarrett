# Stage 8: Ship to TestFlight

TestFlight is Apple's beta channel: you upload a build, Apple processes it, and the
user installs it on their phone through the TestFlight app. Steps 1–5 are one-time.
Only run builds or submissions when the user says to.

## One-time setup

1. **Apple Developer Program** at developer.apple.com: $99/year, approval can take a
   day or two. Start early; it blocks everything else. Install TestFlight on the phone.
2. **Bundle ID** (reverse-DNS, e.g. `com.yourname.appname`). It's permanent, so no
   working titles.
3. **Reserve the App Store name early**: App Store Connect → My Apps → + → New App
   (iOS, the name, the bundle ID, any SKU). Names get taken. The home-screen name
   (`app.json` → `name`) can differ.
4. **EAS**, Expo's cloud build service. It handles signing certificates; accept the
   defaults.

   ```bash
   npm install -g eas-cli
   eas login
   eas init
   ```

5. **`eas.json`** production profile:

   ```json
   {
     "cli": { "appVersionSource": "remote" },
     "build": {
       "production": {
         "autoIncrement": true,
         "env": { "EXPO_PUBLIC_API_URL": "https://..." }
       }
     }
   }
   ```

   And in `app.json`:
   `"ios": { "infoPlist": { "ITSAppUsesNonExemptEncryption": false } }`
   (correct for apps using only standard HTTPS). Without it every build waits on an
   export-compliance question.

## ⚠️ The trap: `.env` never reaches cloud builds

EAS respects `.gitignore`, so the local `.env` isn't uploaded. The build ships with
every `EXPO_PUBLIC_*` value empty and usually crashes at launch, while working fine
locally.

- Public config (API URLs, keys designed to be public): put it in `eas.json` → `env`.
  These values ship inside the app anyway.
- Real secrets: never in the app. They live on the server. If a build-time secret is
  truly needed, use EAS secrets.
- Read the build log: "No environment variables found" means this is about to bite.

## Every build

```bash
eas build --platform ios --profile production
eas submit --platform ios --latest
```

Or download the `.ipa` from the EAS build page and upload it with Apple's free
Transporter app. A build takes about 10–20 minutes.

In App Store Connect → the app → TestFlight:

1. The build shows "Processing" for 5–30 minutes.
2. "Missing Compliance" means the encryption flag above wasn't set; answer "standard
   encryption only" for this build.
3. Internal Testing → + → add the user's Apple ID. Up to 100 internal testers, no
   review. External testers (public link) need a one-time Beta App Review.

Then on the phone: TestFlight → the app → Install.

## Things to remember

- `version` in `app.json` must match the version in App Store Connect.
- TestFlight builds are release builds; anything dev-only is gone. A crash there that
  doesn't happen in the simulator usually means missing config.
- Permission wording, icons and other native settings only change with a new build.
  Get them right before anyone sees the app.
- **App Store screenshots:** keep them simple. Repeat the one sentence, show the phone
  and the core action. A good video and funnel matter more than clever screenshots.
- AI features that send personal data to outside AI services need a clear, permanent
  in-app disclosure and consent, not just a privacy policy line. App Review checks for
  it, and a one-time screen the reviewer never sees doesn't count.

## Costs

- Apple Developer Program: $99/year.
- EAS: the free tier covers early TestFlight builds.
- TestFlight: free.

## Gate

When the app is installed from TestFlight on their phone, celebrate, update the Journey page, give the reel moment ("My app is on TestFlight") and ask whether to move on to the Launch kit.
