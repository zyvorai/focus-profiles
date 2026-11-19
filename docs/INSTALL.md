# Install

## Requirements

- macOS 27 or later (the app's `LSMinimumSystemVersion` is 27.0)
- Terminal, iTerm2, Safari or Google Chrome only if a profile uses them
- `kubectl` only if a profile switches a kube context

## Download and verify

1. Download `FocusProfiles-0.1.0.dmg` and `FocusProfiles-0.1.0.dmg.sha256` from the [release page](https://github.com/zyvorai/focus-profiles/releases/tag/v0.1.0).
2. Optional: verify the checksum.

   ```
   cd ~/Downloads
   shasum -a 256 -c FocusProfiles-0.1.0.dmg.sha256
   ```

3. Open the DMG and drag **FocusProfiles** to **Applications**.

The app is signed with a Developer ID and notarized by Apple, so it opens without a Gatekeeper warning.

## First launch

Focus Profiles is a menu-bar app: it has no Dock icon. After you open it:

- A **Welcome** window explains the two macOS permissions it may ask for. Nothing is requested there; see [Permissions](PERMISSIONS.md).
- A menu-bar item appears. Its menu lists your profiles, **Edit Profiles…**, **Settings…**, **Licence…**, **About** and **Quit**.
- A first profile, "Example: side by side" (Terminal on the left half, Safari on the right half), is created if you have none.

Next: [profiles](PROFILES.md), then [dry run](DRY-RUN.md) to preview a switch.

## Licence key (optional)

The app works without a key. For a free 30-day trial key write to **sales@zyvor.dev**, then choose **Licence…** in the menu, paste the key and press **Verify and Save**. See [Licence and trial](LICENSING.md).

## Uninstall

Quit the app, delete `FocusProfiles.app`, and, if you want to remove your profiles too, delete `~/Library/Application Support/Focus Profiles/`.
