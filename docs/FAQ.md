# FAQ

**What does one hotkey do?** It switches a profile: window layout, terminal windows, browser tabs, VPN and kube context, in that group of steps, as you defined them. See [Profiles](PROFILES.md).

**Which macOS versions?** macOS 27 or later.

**Does it work without a licence key?** Yes. Everything works and a status line says "Unlicensed". For a free 30-day trial key write to sales@zyvor.dev. See [Licence and trial](LICENSING.md).

**What does it cost?** Prices are not published yet. Contact sales@zyvor.dev.

**Which permissions does it need?** Accessibility for window layout and Automation for Terminal, iTerm2, Safari and Google Chrome. Neither is requested up front, and if you deny one only the affected steps are skipped. See [Permissions](PERMISSIONS.md).

**Can I preview a switch?** Yes: [dry run](DRY-RUN.md), in the editor or with `--dry-run` from a terminal. It moves nothing and prompts for nothing.

**Is it safe to put commands in a profile?** The command is typed into a new terminal window exactly as written, so it runs with your own rights, as if you had typed it. Only keep commands you trust.

**Which URLs does it open?** Only `http` and `https` URLs. Anything else is ignored.

**Where are my profiles?** `~/Library/Application Support/Focus Profiles/Profiles/`, one JSON file each. Set `FOCUS_PROFILES_DIR` to use another folder.

**Which terminals and browsers?** Terminal and iTerm2; Safari and Google Chrome.

**Does it support several displays?** Window rectangles are fractions of the main display's usable area. Other displays are not addressed.

**What does it not do?** It does not use any private Spaces API, and it does not read the contents of your windows, your tabs or your terminal output.

**Are the screenshots real?** They are renders of the app's own SwiftUI views with sample data (an invented project called "Atlas"), produced by the app's `--render-screenshots` flag. They are not captures of a live session, and the dry-run text in these docs is real output.

**Is the source available?** No. This repository holds documentation, the website and downloads. The source code is private.

**Something behaves differently from the docs.** Real window moves and the macOS permission prompts were not exercised on a live desktop before 0.1.0. Please tell sales@zyvor.dev.
