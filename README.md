# dotfiles

Personal configuration files for macOS (Ghostty, Neovim, Zsh).

## Structure

```
.
├── ghostty
│   ├── config          # Ghostty terminal config (theme, font, opacity, shell integration)
│   └── welcome.txt      # Banner shown on interactive shell start
├── nvim
│   ├── init.lua
│   ├── lazy-lock.json
│   ├── lazyvim.json
│   ├── LICENSE
│   ├── lua
│   │   ├── config
│   │   │   ├── autocmds.lua
│   │   │   ├── keymaps.lua
│   │   │   ├── lazy.lua
│   │   │   └── options.lua
│   │   └── plugins
│   │       └── example.lua
│   ├── README.md
│   └── stylua.toml      # LazyVim-based Neovim config
└── zsh
    ├── aliases.zsh       # Custom shell aliases
    ├── secrets.zsh        # API keys/tokens (gitignored — never committed)
    └── zshrc             # Main zsh config, sourced via symlink
```

## Setup

**This repo does nothing on its own.** Each config only takes effect once it's symlinked into the location the corresponding app actually reads from. Symlinking — not copying — is what makes this whole setup work: edit a file here, and the change is live immediately wherever it's linked, with one source of truth tracked in git.

Create the symlinks:

```bash
ln -s ~/.dotfiles/zsh/zshrc ~/.zshrc
ln -s ~/.dotfiles/ghostty ~/.config/ghostty
ln -s ~/.dotfiles/nvim ~/.config/nvim
```

Verify they took:

```bash
ls -la ~/.zshrc ~/.config/ghostty ~/.config/nvim
```

Each should show as a symlink (`->`) pointing back into `~/.dotfiles`.

## Secrets

`zsh/secrets.zsh` holds API keys and tokens as `export` statements. It is listed in `.gitignore` and must be recreated manually on any new machine — it is never committed to the repo.

```bash
touch ~/.dotfiles/zsh/secrets.zsh
chmod 600 ~/.dotfiles/zsh/secrets.zsh
```

`zshrc` sources it conditionally, so a missing `secrets.zsh` on a fresh clone won't break the shell:

```bash
[ -f ~/.dotfiles/zsh/secrets.zsh ] && source ~/.dotfiles/zsh/secrets.zsh
```
