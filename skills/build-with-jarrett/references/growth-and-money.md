# Growth and money

## The first-session order that works

1. Splash: the one sentence and one button.
2. One or two setup questions, plus a permission that now makes sense
   ("What time do you wake up?" → notification prompt).
3. The magic moment.
4. The paywall, if there is one.
5. **A second magic moment built to share**, for example a membership card with the
   user's name, a member number and a small celebration, with a clear share button.
6. Any permission that defines the habit (camera, location, Screen Time), right after
   the user has felt why it matters.

## Permissions

- Ask in the first session. A "no" can only be reversed in Settings, and most people
  never do it.
- Never show the system prompt cold. A designed screen first, in the app's voice,
  makes the reason obvious; then the prompt.
- If the app needs quiet, time or headphones, offer "Now or later?" Later means a
  reminder at a better time. The person isn't lost; they're scheduled.
- Write the permission text in `app.json` as carefully as any other copy. It only
  changes with a new build.

## Make the action that keeps people sure to happen

Find the early action that predicts a user comes back (a dating app knows a
first-day match does). Then design so every new user does it: good defaults, a
reminder, the right timing. **Do the honest version only.** Never fake matches,
messages, users or activity.

## Sharing

- People share what gives them **status** or makes them look **normal**, never what
  makes them look weird or lame.
- People do what they see others doing. A shared moment (a yearly recap, a start date
  everyone joins on, a challenge) makes sharing feel normal.
- Keep the share asset **simple and personal**: the user's own photo (blurred works
  well) behind one line of text, a small logo, and a link. Not an over-designed poster.
- Never ask people to share something private. Find the part that's safe to show (a
  goal, a streak, a result).
- One-to-one invites count. Not everything needs to go on a Story.

## Viral loops

A viral loop is when one user's action brings in the next user, who does the same.

- **Tight:** the friend does exactly what the sharer did. Keep the chain short.
- **Required:** the strongest loops make sharing how you unlock value. Two-person
  features that only work once the second person joins are the hardest share gate.
- **Variable reward:** people come back for what they can't predict (how many replies,
  which result).
- **Half-gated:** show part of the result on a web page with "download to see the
  rest" right there, as long as it doesn't annoy people.
- **Measure it:** before product-market fit, the main number is share rate. Bring in
  1,000 users, count how many share, and iterate until each download brings another.
- Loops are the strongest growth engine but don't work for every app. If the product
  is private by nature, plan for content to do most of the work.

## Before launch

- **Founding memberships:** sell early access with a member number and a referral
  leaderboard where invites move people up toward rewards you can give. Real product,
  honest copy.
- **Apple Wallet:** a membership card added to Wallet stays on the phone for good.
  Few apps use it.

## Getting the first users

- **Aim for 1,000 users in one day.** That usually comes from one video that hits on
  TikTok, Reels or Shorts. Ideally those people know each other.
- **Post volume on every channel:** TikTok, Reels, Shorts, Reddit. Faceless slideshows
  work ("me after 30 days of X"). Lead with the pain; pain sells better than vitamins.
- The same volume is how AI assistants come to recommend your app.
- Find a trend that's just about to go mainstream. Niches work (an app only for
  vegans, only for one hobby).
- The US pays most. Some regions are cheaper places to get downloads. Translate early.
- Instead of paying many creators, consider one creator as a co-founder with equity
  who runs content.

## Money

- People will pay up front after a good onboarding with a real magic moment.
- **Hard or soft paywall:** a hard paywall stops free users from sharing. Rule of
  thumb: if the app grows by sharing, keep a free tier; if it grows through ads and
  content, a hard paywall right after the magic moment is fine.
- **Weekly, monthly or annual:** weekly works for impulse, social and fun apps; annual
  first is common for paid-ad apps. Test.
- **Apple takes 30%** (15% for small developers in the Small Business Program). In
  return: no chargebacks, refunds handled, less legal risk.
- **Web checkout** keeps more and pays sooner. Where the rules allow it, split
  traffic between web and Apple paywalls (a 50/50 test is fine), since some people drop
  off on the web. Send paid ads to the web funnel.
- Use a subscription tool (for example RevenueCat, with a paywall-testing tool) so
  price and paywall tests never need an App Store review.
- Main costs: marketing, team, and AI usage if the app calls models or makes images.
  Put per-user limits on expensive calls from day one.
- Trial terms in plain, readable type on the paywall. Unreadable small print is a dark
  pattern and Apple rejects it.

## Keep improving

- Iterate the first session and the share flow, not the feature list.
- Hide what people don't use; delete it if nobody misses it.
- After share rate: day 2, day 7 and day 30 return rates, and how many pay.
