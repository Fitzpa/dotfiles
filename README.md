# Dotfiles Overview

This repository is organized as **GNU Stow packages**. Each top-level directory is a package that can be symlinked into your machine.

## How setup currently works

### `.stowrc`

Current options:

- `--target=~/.config`
  - Stow writes symlinks into `~/.config`.
- `--ignore=.stowrc`
  - Prevents Stow from trying to link the Stow config itself.
- `--ignore=DS_Store`
  - Ignores macOS metadata files.
- `--ignore=atuin/*`
  - Ignores everything inside `atuin/`.

### `setup.sh`

`setup.sh` currently runs:

```bash
stow .
```

Because `.stowrc` sets `--target=~/.config`, this attempts to link package contents into `~/.config`.

## Top-level directories and what they do

- `aerospace/` — AeroSpace window manager config.
- `atuin/` — Atuin shell history config.
- `gh-dash/` — GitHub dashboard (`gh-dash`) config.
- `ghostty/` — Ghostty terminal config + shader assets.
- `hammerspoon/` — Hammerspoon automation scripts and local Spoons.
- `karabiner/` — Karabiner-Elements key remapping config.
- `kindavim/` — KindaVim macOS preference plist.
- `nix/` — Nix daemon/client config.
- `nix-darwin/` — Nix-Darwin flake and Home Manager config.
- `nushell/` — Nushell environment and shell config.
- `nvim/` — Neovim distribution/configuration.
- `opencode/` — OpenCode tool configuration, agents, and skills.
- `sketchybar/` — SketchyBar status bar config and helper plugin code.
- `skhd/` — skhd hotkey config and AppleScripts.
- `ssh/` — SSH client config.
- `starship/` — Starship prompt config.
- `television/` — Television launcher config and cable sources.
- `tmux/` — tmux configuration and helper scripts.
- `wezterm/` — WezTerm terminal config.
- `zellij/` — Zellij terminal multiplexer config and themes.
- `zshrc/` — Zsh shell startup file.

## Potentially unused or mis-targeted in the current setup

Because target is `~/.config`, files link into that folder directly (for example, `ghostty/config` => `~/.config/config`). Some tools expect different locations. Notable suspects:

- `atuin/` is explicitly ignored by `.stowrc` and will not be linked.
- `ghostty/config` likely needs to be under `~/.config/ghostty/config`, not `~/.config/config`.
- `ssh/ssh-config` likely needs to be `~/.ssh/config` (or include file), not `~/.config/ssh-config`.
- `zshrc/.zshrc` likely needs to be `~/.zshrc`, not `~/.config/.zshrc`.
- `karabiner/karabiner.json` and `kindavim/*.plist` usually live in app-specific macOS paths, not `~/.config`.
- `nix/nix.conf` is commonly `/etc/nix/nix.conf` or `~/.config/nix/nix.conf`; current target would be `~/.config/nix.conf`.
- `sketchybar/`, `skhd/`, `hammerspoon/` often expect app-specific paths and may require explicit launch arguments or extra symlinks.

See each directory README for deeper detail.
