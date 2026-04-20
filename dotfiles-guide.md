# Working with Dotfiles and Stow

GNU Stow is a symlink farm manager. It creates symbolic links from your dotfiles repo into a target directory (`~/.config`), letting you track config files in git while they appear in their normal locations.

## How `.stowrc` Works

The `.stowrc` file in the repo root sets default options so you don't have to pass flags manually:

```
--target=~/.config
--ignore=.stowrc
--ignore=DS_Store
```

This means `stow .` always targets `~/.config`, so each top-level directory in the repo (e.g. `nvim/`, `tmux/`) maps to `~/.config/nvim/`, `~/.config/tmux/`, etc.

## Initial Setup

Check for conflicts before stowing:

```sh
stow -nv . 2>&1 | grep -i "conflict\|existing\|cannot"
```

Back up any conflicting directories:

```sh
cp -r ~/.config/TOOL ~/.config/TOOL.bak
```

Remove the conflicting file so stow can symlink it:

```sh
rm ~/.config/TOOL/config-file
```

Stow everything:

```sh
stow .
```

## Adding a New Config to the Repo

Move the config from `~/.config` into the dotfiles repo:

```sh
mv ~/.config/TOOL ~/code/omerxx-dotfiles/TOOL
```

Restow to create the symlink back:

```sh
stow -R .
```

Commit it to git:

```sh
git add TOOL && git commit -m "Add TOOL config"
```

## Common Commands

| Command | Description |
|---|---|
| `stow -nv .` | Dry-run — simulate without making changes |
| `stow .` | Stow all packages |
| `stow -D PACKAGE` | Unstow a package (remove its symlinks) |
| `stow -R PACKAGE` | Restow a package (remove and re-create symlinks) |

Find what's in `~/.config` but not yet tracked in the repo:

```sh
ls ~/.config/ | grep -vxFf <(ls ~/code/omerxx-dotfiles/)
```

Check which symlinks already point to the dotfiles repo:

```sh
find ~ -type l -lname '*omerxx-dotfiles*'
```

Find broken symlinks (targets no longer exist):

```sh
find ~ -xtype l
```