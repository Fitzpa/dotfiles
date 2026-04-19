# nvim/

## Purpose
Neovim configuration (LazyVim-style layout).

## Contents
- `init.lua` — Neovim entry config.
- `lazyvim.json`, `lazy-lock.json` — Plugin manager metadata/lock.
- `lua/config/` — Core editor config (options, keymaps, autocmds, lazy bootstrap).
- `lua/plugins/` — Plugin specifications/overrides.
- `stylua.toml` — Lua formatting settings.
- `.neoconf.json` — Local tooling/editor metadata.
- `LICENSE` — License text.
- `.gitignore` — Ignore patterns.

## Current Stow target result
- Files are linked directly under `~/.config` (for example `~/.config/init.lua`, `~/.config/lua/...`).

## Notes
- This can work for Neovim because Neovim commonly reads from `~/.config/nvim/` **not** flat `~/.config`.
- In current setup, this is likely mis-targeted unless additional directory-level symlink strategy is used.
