# Dry run

A dry run prints what a switch **would** do, including what it would skip because a permission is missing. It **moves nothing, launches nothing and prompts for nothing.**

## In the editor

Press **Dry Run** (⌘R) at the bottom of a profile. The result appears below the profile, one row per step.

## From a terminal

```
/Applications/FocusProfiles.app/Contents/MacOS/FocusProfiles --dry-run [profile name|all] [--profiles-dir DIR]
```

With no name, or `all`, every profile is shown. Exit status is 2 when no profile is found or the name does not match.

## Real output

This is the real output of the 0.1.0 build for the example profile in [example-profile.json](example-profile.json) (the home folder is shortened to `/Users/you`; the screen size comes from the Mac that ran it):

```
Dry run for "Project Atlas": would do 6, would skip 0
  [would do] Connect VPN "Corp VPN"
  [would do] Use kube context "atlas-staging"
  [would do] Open Terminal window (in /Users/you/code/atlas, run `git status`)
  [would do] Open 1 tab in Safari: https://example.com/board
  [would do] Place Terminal at 0,30 size 960x1050
  [would do] Place Safari at 960,30 size 960x1050
```

And for a profile with a bad URL and a bad VPN name, showing the safety rules:

```
Dry run for "Docs only": would do 1, would skip 1
  [would skip] Connect VPN "-bad": VPN service name must not start with a dash
  [would do] Open 1 tab in Google Chrome: https://example.com/docs (ignoring 1 invalid: file:///etc/passwd)
```

When Accessibility or an Automation permission is missing, the affected lines read `[would skip] ...` with the reason, for example `Automation for iTerm2 is not allowed (System Settings > Privacy & Security > Automation)`.

After a real switch the same lines read `[done]`, `[skipped]` or `[failed]`.
