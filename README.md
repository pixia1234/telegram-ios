# Telegram iOS Lite Builder (Aggressive Trim)

This repository builds an unsigned Telegram iOS IPA in GitHub Actions with a patch that:

- disables Telegram Premium and Stars related features in the client
- disables sponsored ads in chat and ad peer search
- removes Contacts and Calls tabs from the root tab bar (chat + settings only)
- disables story upload pipeline by default
- removes gift / todo / attach-menu app buttons from chat attachment UI
- pins upstream Telegram iOS source to commit `63a37c5becb646a3c2400e01d91d78faf4799a2e` for reproducible patching

## What this repo contains

- `patches/0001-lite-trim-heavy-features.patch`: source patch applied on top of upstream Telegram iOS.
- `scripts/apply_mods.sh`: patch apply helper.
- `.github/workflows/build-unsigned-ipa.yml`: CI pipeline that clones upstream Telegram iOS, applies patch, and builds an unsigned IPA.

## How to build

1. Push this repository to GitHub.
2. Open **Actions**.
3. Run workflow: **Build Unsigned Telegram IPA**.
4. Download artifact `Telegram-unsigned-ipa-<build_number>`.

## Notes

- Build uses upstream fake codesigning and outputs an unsigned IPA.
- If upstream source changes significantly, patch apply may fail. Update `patches/0001-lite-trim-heavy-features.patch` accordingly.
- Story upload and todo editing can be re-enabled via app config keys `lite_enable_stories=true` and `lite_enable_todo=true`.
