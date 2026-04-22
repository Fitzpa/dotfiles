# aerospace/

## Purpose
Configuration for the AeroSpace tiling window manager.

## Contents
- `aerospace.toml` — Main AeroSpace configuration.

## Current Stow target result
- `~/.config/aerospace.toml`

## Configuration walkthrough (`aerospace.toml`)

This file configures startup hooks, window behavior, layout defaults, gaps, keybindings, modes, and workspace/monitor mapping.

### 1) Startup + workspace change hooks

- `after-startup-command = ['exec-and-forget sketchybar']`
  - Starts SketchyBar after AeroSpace starts.
- `exec-on-workspace-change = [...]`
  - Runs on workspace switch:
    - Triggers a SketchyBar event (`aerospace_workspace_change`) with focused workspace info.
    - Runs `borders` to set active/inactive border colors and width.

How to use:
- Keep this if you use SketchyBar/borders integration.
- Remove or replace commands if you use different status bar/border tools.

### 2) Startup behavior

- `start-at-login = false`
  - AeroSpace is not auto-started at macOS login.

How to use:
- Set to `true` if you want AeroSpace to launch automatically.

### 3) Normalization behavior

- `enable-normalization-flatten-containers = true`
- `enable-normalization-opposite-orientation-for-nested-containers = true`

What it does:
- Keeps layout trees cleaner and more predictable.
- Avoids nested containers with same orientation when possible.

How to use:
- Keep enabled for i3-like behavior and simpler tiling trees.

### 4) Layout defaults

- `accordion-padding = 300`
  - Large side padding when using accordion layout.
- `default-root-container-layout = 'tiles'`
  - New root containers start in tiled mode.
- `default-root-container-orientation = 'auto'`
  - Chooses horizontal on wide monitors, vertical on tall monitors.

How to use:
- Reduce `accordion-padding` if accordion feels too sparse.
- Change layout/orientation defaults if you prefer fixed behavior.

### 5) Focus behavior

- `on-focused-monitor-changed = ['move-mouse monitor-lazy-center']`
  - Mouse cursor moves toward center of focused monitor when monitor focus changes.

How to use:
- Remove this if you do not want pointer warping.

### 6) macOS hidden app behavior

- `automatically-unhide-macos-hidden-apps = false`
  - AeroSpace will not auto-unhide apps hidden via Cmd+H.

How to use:
- Set `true` if you want hidden apps to auto-unhide when focused.

### 7) Window detection rules (`[[on-window-detected]]`)

Apps matched by name substring are set to floating:
- `telegram`
- `finder`
- `safari`
- `dicord` (likely typo; see below)
- `mail`
- `trello`
- `quicktime`
- `discord`

What it does:
- These windows open in floating layout instead of tiling.

How to use:
- Add/remove rules based on apps you prefer to float.
- There is both `dicord` and `discord`; `dicord` appears to be a typo and can likely be removed.

### 8) Keyboard mapping preset

- `[key-mapping]`
- `preset = 'qwerty'`

What it does:
- Uses QWERTY key interpretation.

How to use:
- Change to `dvorak` if needed.

### 9) Gaps configuration (`[gaps]`)

- `inner.horizontal = [{ monitor.main = 40 }, 10]`
- `outer.left/right = [{ monitor.main = 350 }, 20]`
- `outer.top = [{ monitor.main = 100 }, 10]`
- `outer.bottom = [{ monitor.main = 100 }, 10]`

What it does:
- Uses bigger margins on the `main` monitor (likely primary display).
- Falls back to smaller defaults on other monitors.

How to use:
- Tune these values per monitor for your display geometry.
- `inner.vertical` is currently commented out.

### 10) Main keybindings (`[mode.main.binding]`)

#### Window/layout control
- `alt-ctrl-shift-f` → fullscreen
- `alt-ctrl-f` → toggle floating/tiling
- `alt-slash` → cycle tile layouts (tiles horizontal vertical)
- `alt-comma` → cycle accordion layouts

#### Join containers
- `alt-shift-left/down/up/right` → `join-with` direction

#### Focus movement (vim-style)
- `alt-h/j/k/l` → focus left/down/up/right

#### Window movement
- `alt-shift-h/j/k/l` → move window left/down/up/right

#### Resize
- `alt-shift-minus` → resize -50
- `alt-shift-equal` → resize +50

#### Workspaces
- `alt-1..4` → switch workspace 1..4
- `alt-shift-1..4` → move window to workspace 1..4 and follow focus
- `alt-tab` → toggle previous workspace
- `alt-shift-tab` → move workspace to next monitor (wrap)

#### Mode switching
- `alt-shift-semicolon` → enter `service` mode
- `alt-shift-enter` → enter `apps` mode

#### App launchers
- `alt-o` → Obsidian
- `alt-b` → Brain.fm
- `alt-s` → Slack
- `alt-q` → QuickTime Player
- `alt-w` → WezTerm
- `alt-f` → Finder
- `alt-e` → Final Cut Pro
- `alt-z` → Zen
- `alt-t` Telegram launcher exists but is commented out.

How to use:
- This is a modal, keyboard-driven workflow:
  - Navigate/focus with `alt + h/j/k/l`
  - Move with `alt + shift + h/j/k/l`
  - Switch workspaces with `alt + number`

### 11) Service mode (`[mode.service.binding]`)

- `esc` → reload config, return to main mode
- `r` → flatten workspace tree, return to main mode
- `f` → toggle floating/tiling, return to main mode
- `backspace` → close all windows but current, return to main mode

How to use:
- Enter using `alt-shift-semicolon`, run one maintenance action, auto-return to main mode.

### 12) Apps mode (`[mode.apps.binding]`)

- `alt-w` → launch WezTerm, then return to main mode

How to use:
- Enter using `alt-shift-enter`.
- Add more app shortcuts here to keep launch commands grouped.

### 13) Workspace-to-monitor mapping (`[workspace-to-monitor-force-assignment]`)

- Workspace `1` → monitors matching `^Built-in.*$`
- Workspace `2` → monitors matching `^DELL U.*$`
- Workspace `3` → monitors matching `^DELL S.*$`
- Workspace 4+ examples are commented out.

What it does:
- Pins workspaces to specific monitors by monitor-name regex.

How to use:
- Run AeroSpace monitor-list command (or check display names) and adjust regex patterns to your hardware names.

## Practical usage pattern

1. Use `alt-1..4` to jump between workspaces mapped to specific monitors.
2. Use `alt-h/j/k/l` and `alt-shift-h/j/k/l` for fast keyboard-only focus/move.
3. Keep communication/media apps floating via `on-window-detected`.
4. Trigger service actions via `alt-shift-semicolon` when layout cleanup is needed.

## Notes
- The README describes the current state of `aerospace.toml`.
- AeroSpace command reference: https://nikitabobko.github.io/AeroSpace/commands
