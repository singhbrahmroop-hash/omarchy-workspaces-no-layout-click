# Workspaces (no layout click)

An [Omarchy](https://omarchy.org/) bar widget for people who want workspace
layouts changed **only by keyboard**.

Recent Omarchy updates made the active workspace button in the top bar clickable:
clicking it cycles that workspace through tiling → scrolling → floating. One
accidental click can change your whole workspace layout.

This plugin is a clone of Omarchy's stock `omarchy.workspaces` widget with one
small change: clicking the **active** workspace no longer cycles its layout.
Clicking the *other* workspace numbers still switches workspaces.

## Controls after installing

| Action | Result |
| --- | --- |
| Click active workspace number/glyph | Nothing |
| Click another workspace number | Switch to that workspace |
| `Super + L` | Cycle layout forward |
| `Super + Alt + L` | Cycle layout backward |
| `Super + T` | Toggle a single window floating/tiling (unchanged) |

## Install

```bash
omarchy plugin add https://github.com/singhbrahmroop-hash/omarchy-workspaces-no-layout-click.git --enable --yes
```

If you already cloned the stock widget (`omarchy plugin clone omarchy.workspaces`),
remove/disable that clone first so the bar doesn't have two workspaces widgets.

You can also install manually: copy this folder to
`~/.config/omarchy/plugins/io.github.singhbrahmroop-hash.workspaces-no-layout-click/`
and enable it with:

```bash
omarchy plugin enable io.github.singhbrahmroop-hash.workspaces-no-layout-click --section left
```

## Remove / go back to stock

```bash
omarchy plugin remove io.github.singhbrahmroop-hash.workspaces-no-layout-click --yes
omarchy plugin clone omarchy.workspaces   # restores the stock clickable widget
```

Removing the plugin does not touch your saved workspace layouts or keybindings.

## Dependencies

None beyond Omarchy/Quickshell itself. No extra packages, services, or network
access are used.

## What changed

Against Omarchy 4.5.0's `shell/plugins/bar/widgets/Workspaces.qml`:

```diff
-        onPressed: function() {
-          if (shown) root.cycleLayout()
-          else root.focusWorkspace(modelData)
-        }
+        // Clicking the active workspace no longer cycles its layout; use
+        // Super + L (or Super + Alt + L) for that.
+        onPressed: function() {
+          if (!shown) root.focusWorkspace(modelData)
+        }
```

Everything else is the upstream file unchanged, so layout glyphs, workspace
switching, wheel scrolling, and multi-monitor behaviour stay the same.

## Why not just use a setting?

There isn't a shipped setting for this in Omarchy 4.5.0. Upstream proposals that
do the same job are still open:

- [PR #15993 – Add an off switch for the bar's click cycles](https://github.com/omacom/omarchy/pull/15993)
- [PR #18082 – Add config-lock guards for bar, workspaces, and dock](https://github.com/omacom/omarchy/pull/18082)
- [PR #16629 – Let the workspace layout cycle choose which layouts it holds](https://github.com/omacom/omarchy/pull/16629)
- [PR #17959 – Make the workspace layout cycle configurable](https://github.com/omacom/omarchy/pull/17959)

When one of those lands, this plugin can be retired in favour of the official
setting.

## License

MIT. This is a modified copy of Omarchy's `Workspaces.qml`, which is
Copyright (c) David Heinemeier Hansson. See [LICENSE](LICENSE).
