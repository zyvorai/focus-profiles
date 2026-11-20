# Permissions explained

Focus Profiles asks macOS for two permissions, and only when a profile first needs them. The Welcome window explains them and links to the System Settings panes, but **requests nothing up front**.

| Permission | Used for | When macOS asks |
| --- | --- | --- |
| **Accessibility** | Moving and resizing other apps' windows (window layout) | The first time you switch a profile that places windows |
| **Automation** (Apple events) | Telling Terminal, iTerm2, Safari or Google Chrome to open a window or tabs | Once per target app, the first time a profile uses it |

VPN and kube context need **no permission**: the VPN uses the services you already set up in System Settings (`scutil --nc`), and the kube context runs `kubectl config use-context`, so `kubectl` must be installed.

## What Focus Profiles does with them

- **Accessibility** is used to set the position and size of other apps' windows through the Accessibility API (no private Spaces API). The app's own onboarding states that it does not read window contents, record the screen or watch your keystrokes.
- **Automation** is used to open a terminal window or browser tabs. It never reads your tabs or terminal output.
- The only entitlement the app carries is `com.apple.security.automation.apple-events`.

## If you say no

Nothing breaks. A step whose permission is missing is **skipped and reported**, and the rest of the profile still runs. After a switch, the menu shows a line such as `Switched to "Atlas": 5 done, 1 skipped, 0 failed` and a **See what was skipped…** item. A [dry run](DRY-RUN.md) shows the same skips in advance.

You can change your mind later in System Settings > Privacy & Security > Accessibility or > Automation. **Settings…** in the app has buttons that open both panes and shows whether Accessibility is granted.

## Not tested yet

Real window moves and the macOS permission prompts were not exercised on a live desktop before the 0.1.0 release. Planning, dry runs, skipping when a permission is denied, and the safety rules are covered by the app's own self-tests (`--selftest`), which run against a recording stand-in for the system. If a prompt or a window move behaves differently from this page, please tell **sales@zyvor.dev**.
