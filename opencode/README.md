# opencode/

## Purpose
Configuration and prompt assets for OpenCode tooling.

## Contents
- `opencode.json` — Main OpenCode config.
- `tui.json` — TUI-specific settings.
- `agent/` — Agent personas and role prompts.
- `command/` — Command prompt templates.
- `skills/ship/SKILL.md` — Custom skill definition.

## Current Stow target result
- `~/.config/opencode.json`
- `~/.config/tui.json`
- `~/.config/agent/...`
- `~/.config/command/...`
- `~/.config/skills/...`

## Usage status
- Might be valid if OpenCode is configured to read from these exact paths.
- If OpenCode expects `~/.config/opencode/...`, this is mis-targeted.
