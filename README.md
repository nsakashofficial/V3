# MeetWoYou — Functional Update v3

A source-level update to the existing static MeetWoYou project. Existing Firebase Auth, Firestore and Cloudinary configuration and current page structure are preserved.

## Main entry points
- `index.html` — sign in / sign up
- `dashboard.html` — social feed, stories, profile and creator studio entry
- `messenger.html` — messaging
- `admin.html` — admin console

## Changes in this package
- Dashboard header settings shortcut moved to the profile section; the brand remains centered.
- Added a working emoji picker to the post composer.
- Removed synthetic/random initial view counts for newly created video posts.
- Admin exit now signs out of Firebase before redirecting.
- Monetization policy now persists to `platformSettings/monetization` in Firestore and reloads in the admin console.
- Creator eligibility reads the configured follower threshold (default 5,000).
- Payout requests use a Firestore transaction to avoid a non-atomic balance deduction and payout record; the configured minimum payout is checked.
- Service worker cache bumped to `mw-v12` and app modules added to the shell cache.

## Deployment
Extract the ZIP and upload all archive contents directly to the GitHub Pages repository root. No parent folder is included.

## Important production notes
- Firestore security rules must restrict writes to `platformSettings/monetization` to trusted admins. Client-side email checks alone are not a security boundary.
- Payout requests are recorded as pending; they do not trigger a real bank transfer. A secure server-side payout integration is required for real payments.
- Static JavaScript syntax and ZIP integrity were checked. Live Firebase/Cloudinary end-to-end tests were not possible in this environment, so verify authentication, posting, Messenger, admin actions and monetization after deployment.
