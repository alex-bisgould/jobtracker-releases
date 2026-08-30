# Job Tracker — releases & download site

Public **release feed + download page** for [Job Tracker](https://alex-bisgould.github.io/jobtracker-releases/),
a local-first job-search CRM for macOS. The app's source lives in a separate private repo
(`alex-bisgould/job-tracker`); this repo holds only the published builds and the GitHub Pages site.

**Download:** https://alex-bisgould.github.io/jobtracker-releases/
**What's new:** https://alex-bisgould.github.io/jobtracker-releases/whats-new.html

## How the pieces fit

- **Releases** are published here by the private repo's `jtship` flow
  (electron-builder `--publish always`, Developer-ID signed + notarized, Team `27S6M97XT4`).
- **Installed apps auto-update** from this repo via electron-updater: they poll
  `latest-mac.yml` on the latest release (every 6h + a manual *Check for Updates…* menu item).
- **The Pages site** (this repo's `index.html`, served from `main`) needs no per-release
  update: the download button targets `releases/latest/download/…` and the version badge +
  what's-new list read the GitHub releases API at page load.

## Load-bearing asset names (do not rename)

| Asset | Role |
|---|---|
| `Job-Tracker-mac-arm64.dmg` | Stable-name installer — the download button's permanent target |
| `Job-Tracker-<version>-arm64-mac.zip` | What electron-updater actually installs from |
| `latest-mac.yml` | The auto-update manifest (version + sha512 + file list) |
| `*.blockmap` | Delta-update helpers |

A release missing the `.zip` or `latest-mac.yml` will not auto-update anyone; the `.dmg` is
for first-time installs. All three are uploaded together by the publish flow.

## Invite links

The download page is **invite-aware**: `/?code=<CODE>&type=<referral|household|link>&name=<inviter>`
shows a personalized banner, a `jobtracker://join?code=…` deep link for people who already have
the app, and carries the code through first-run setup. The `code` is re-verified in-app; `type`
and `name` are display hints only.

## Requirements & data

- Apple Silicon Mac (M1 or later), macOS 12+.
- Signed & notarized; first launch needs no right-click dance on current macOS.
- **Local-first:** app data lives in `~/Library/Application Support/JobTracker` on the user's
  Mac. Nothing is uploaded by default. [Privacy](https://alex-bisgould.github.io/jobtracker-releases/privacy.html) ·
  [Terms](https://alex-bisgould.github.io/jobtracker-releases/terms.html)

## Version notes

Versions `5.60.1` and `5.60.9` were claimed in the in-app changelog but never published as
GitHub releases (no binaries exist for them); their changes shipped inside the next published
version. The what's-new page reads this repo's releases, so those two numbers simply don't
appear here — that's expected.
