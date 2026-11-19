# Profiles: JSON reference

A profile is one plain JSON file. Edit it in the app (menu bar icon > **Edit Profiles…**) or by hand.

- Folder: `~/Library/Application Support/Focus Profiles/Profiles/` (override with the `FOCUS_PROFILES_DIR` environment variable).
- One file per profile, named `<name>-<first 8 characters of id>.json`.
- Every field except `name` is optional, with exceptions noted below. After editing by hand, choose **Reload from Disk** in **Settings…**.
- A file that does not parse is reported in the editor and never overwritten or deleted.

## Example

```json
{
  "schema": 1,
  "name": "Project Atlas",
  "symbol": "briefcase",
  "shortcut": { "keyCode": 18, "modifiers": 6400 },
  "windows": [
    { "bundleID": "com.apple.Terminal", "x": 0,   "y": 0, "width": 0.5, "height": 1 },
    { "bundleID": "com.apple.Safari",   "x": 0.5, "y": 0, "width": 0.5, "height": 1 }
  ],
  "terminals": [ { "app": "terminal", "directory": "~/code/atlas", "command": "git status" } ],
  "browsers":  [ { "app": "safari", "urls": ["https://example.com/board"] } ],
  "vpn": { "service": "Corp VPN", "connect": true },
  "kubeContext": "atlas-staging"
}
```

The same file is in [example-profile.json](example-profile.json).

## Fields

| Field | Type | Meaning |
| --- | --- | --- |
| `schema` | number | File format version. Currently `1`. |
| `id` | UUID string | Identifies the profile (active marker, hotkey). If missing, a new id is made each time the file is read, so add one if you want the active marker to survive a restart. Two files with the same id: the second is ignored and reported. |
| `name` | string, **required** | Shown in the menu and editor. |
| `symbol` | string | An SF Symbol name for the menu entry. Default `scope`. |
| `shortcut` | object | A global hotkey: `keyCode` and `modifiers`, both required. |
| `windows` | array | Window placements, see below. |
| `terminals` | array | Terminal windows to open. |
| `browsers` | array | Browser tabs to open. |
| `vpn` | object | VPN service to connect or disconnect. |
| `kubeContext` | string | Kube context to switch to. |

### `shortcut`

`keyCode` is a macOS virtual key code (for example `18` is the 1 key, `19` is 2, `20` is 3, `21` is 4). `modifiers` is the sum of Carbon modifier masks: Command `256`, Shift `512`, Option `2048`, Control `4096`. So `6400` is Control + Option + Command. The editor sets both for you. Use at least one modifier so the key keeps working in other apps.

### `windows[]`

| Field | Default | Meaning |
| --- | --- | --- |
| `bundleID` | required | The app, for example `com.apple.Terminal`. |
| `x`, `y` | `0` | Top-left corner as a fraction (0 to 1) of the main display's usable area (below the menu bar, above the Dock). `y` counts from the top. |
| `width`, `height` | `1` | Size as a fraction of the same area. |
| `launchIfNeeded` | `true` | Launch the app if it is not running. |

Values outside 0 to 1 are clamped. A window smaller than 100 points in either direction is reported as skipped ("window size is too small"). The editor offers presets (full, halves, two-thirds, third, quarters) and **Capture Frontmost Window**, which waits 3 seconds so you can bring the window to the front. Window placement needs [Accessibility](PERMISSIONS.md).

### `terminals[]`

| Field | Default | Meaning |
| --- | --- | --- |
| `app` | `terminal` | `terminal` or `iterm2`. |
| `directory` | empty | Working folder (`~` is expanded). |
| `command` | empty | A command to run. |

A new terminal window is opened, then `cd '<directory>' && <command>` is typed into it. **The command is typed exactly as written.** Keep only commands you trust in a profile. Needs [Automation](PERMISSIONS.md) for the terminal app.

### `browsers[]`

| Field | Default | Meaning |
| --- | --- | --- |
| `app` | `safari` | `safari` or `chrome` (Google Chrome). |
| `urls` | empty | Pages to open as new tabs. |

**Only `http` and `https` URLs with a host are opened.** Anything else (for example `file:` or `javascript:`) is ignored and named in the result. Needs [Automation](PERMISSIONS.md) for the browser.

### `vpn`

| Field | Meaning |
| --- | --- |
| `service` | The name of a VPN service from System Settings. List them with `scutil --nc list`. |
| `connect` | `true` to connect, `false` to disconnect. |

Both fields are required when `vpn` is present. A service name that starts with a dash is rejected.

### `kubeContext`

Runs `kubectl config use-context <context>`. `kubectl` must be installed. A context name that starts with a dash is rejected.

## Order of steps

A switch runs: VPN, kube context, terminals, browser tabs, then window layout (the apps are open by then).
