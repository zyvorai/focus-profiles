# Changelog

## v0.1.0 - 2026-11-20

First release of Focus Profiles for Mac, notarized, with a 30-day trial. Requires macOS 27 or later.

### Added
- One hotkey per profile switches your setup: window layout (Accessibility API), Terminal or iTerm2 windows, Safari or Google Chrome tabs (Automation), a VPN service (`scutil --nc`) and a kube context (`kubectl config use-context`).
- Plain JSON profiles, one file per profile, in `~/Library/Application Support/Focus Profiles/Profiles/`.
- A profile editor with layout presets and capture of the frontmost window, and a Dry Run button.
- `FocusProfiles --dry-run [profile name|all]`: prints what a switch would do and changes nothing.
- A step that lacks a permission is skipped and reported; the rest of the profile still runs.
- Only `http` and `https` URLs are opened. Terminal commands are typed exactly as written.

### Not tested
Real window moves and the macOS permission prompts were not exercised on a live desktop before release. Planning, dry runs, permission skipping, the safety rules and licence checks are covered by the app's `--selftest`.

Free 30-day trial key: sales@zyvor.dev. The app works without a key and shows an Unlicensed status line.
