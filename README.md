# Telegram iOS Pure Chat Builder (11.9.0)

This repository builds an unsigned Telegram iOS IPA in GitHub Actions with a patch that:

- pins upstream Telegram iOS to **11.9.0** commit `fa93715135f8d9e16ca098c9e0c35d7e370af6ff`
- disables Telegram Premium and Stars in client-side configuration
- disables sponsored ads (chat sponsored messages + ad peer search)
- removes Calls tab from the root tab bar
- removes Settings entries for Recent Calls / Premium / Stars / Business / Send Gift
- removes Settings bot-app list (including Wallet entry)
- removes attachment menu Gift and App buttons (keeps core chat attachments)

## What this repo contains

- `patches/0001-lite-trim-heavy-features.patch`: source patch applied on top of upstream Telegram iOS.
- `scripts/apply_mods.sh`: patch apply helper.
- `scripts/slim_ipa.sh`: post-processing helper to reduce final IPA size (extension pruning, locale pruning, binary strip).
- `.github/workflows/build-unsigned-ipa.yml`: CI pipeline that clones upstream Telegram iOS, applies patch, and builds an unsigned IPA.

## How to build

1. Push this repository to GitHub.
2. Open **Actions**.
3. Run workflow: **Build Unsigned Telegram IPA**.
4. Download artifact `Pixiagram-unsigned-ipa-<build_number>`.

## Notes

- Build uses upstream fake codesigning and outputs an unsigned IPA.
- IPA post-processing defaults:
  - keep locales: `Base,en,zh-Hans` (`IPA_KEEP_LOCALES`)
  - remove app extensions by keyword: `Watch,Widget,BroadcastUpload,Share` (`IPA_DROP_PLUGINS`)
- Patch is targeted specifically for commit `fa93715135f8d9e16ca098c9e0c35d7e370af6ff` (11.9.0). If base changes, patch apply may fail.
