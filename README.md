# Dotfiles

Personal [chezmoi](https://www.chezmoi.io/) setup for macOS and Ubuntu 26.04 (minimal also supports Ubuntu 24.04).

## Install

```sh
sh -c "$(curl -fsLS https://get.chezmoi.io)" -- -b "$HOME/.local/bin" init --apply --use-builtin-git=true https://github.com/georg3k/dotfiles.git
```

Personal/corporate: place your **age** private key at `~/.config/chezmoi/age-key.txt`. Minimal/config need no key. Append `--prompt --promptChoice profile=minimal` (or `profile=config`) to select a key-free profile.

## Profiles

- **personal** (default) — macOS/Ubuntu: dev tools + desktop apps
- **corporate** — macOS: personal profile with corporate tooling
- **minimal** — Ubuntu 24.04/26.04: work tools and configuration, with package/system setup
- **config** — rootless, key-free Git/shell/editor/tmux configuration for installed tools; no downloads, installs or system changes

## What's managed

- **Shell/env:** zsh (Oh My Zsh, autosuggestions, syntax highlighting), tmux, Git, SSH
- **Dev:** GCC, Clang/LLVM, CMake, Ninja, Go, Python, LSP servers; VS Code, Vim/Neovim; Podman, Kubernetes, Terraform/Terragrunt; Java runtimes
- **Desktop:** media, docs, notes, messaging, VPN apps; iTerm (macOS) or Ptyxis (Ubuntu); Fira Code font, Rosé Pine Main/Dawn themes

## Post-deploy steps

- **Steam** (desktop profiles, amd64 only): sign in; on Linux enable Steam Play/Proton via Settings → Compatibility
- **Accounts:** sign into apps, set up VPNs, sync, hardware permissions
- **Secrets:** enable Bitwarden's SSH agent; add your public key to GitHub
- **Firefox:** enable Sync; apply Rosé Pine themes with automaticDark for light/dark switching
- **iTerm:** restart iTerm after apply; select Fira Code; import presets from `~/.local/share/themes/rose-pine-iterm` (Main for dark, Dawn for light)
- **Obsidian:** per vault, select Rosé Pine, "Adapt to system", Fira Code (staged files in `~/.local/share/themes/rose-pine-obsidian`). CLI is bundled: enable Settings → General → Command line interface (requires installer 1.12.7+); chezmoi registers the bundled executable outside minimal mode. Keep Obsidian open while using CLI commands.
- **Telegram (macOS):** install the pre-created [Rosé Pine Dawn](https://t.me/addtheme/t92mgwdG0XiynBSL) and [Rosé Pine](https://t.me/addtheme/m3iEr0CcgyZWEHbf) themes; use Dawn for daytime and Rosé Pine for Auto-Night → System Based.
- **Telegram (Linux):** import theme from `~/.local/share/themes/rose-pine-telegram`
- **Anki:** install ReColor (`688199788`), restart, re-apply chezmoi, select **Rosepine** in ReColor → Configuration → Themes; set Anki to follow system theme
- **OBS:** Appearance → Rose Pine → Main/Dawn
- **LibreOffice:** Application Colors → Rosé Pine Main/Dawn
- **Corporate VS Code:** open projects with `code --profile Corporate PATH`

## Manual exceptions

- DaVinci Resolve (Linux): [vendor installer](https://www.blackmagicdesign.com/event/davinciresolvedownload), x86 only
- **Stremio (Linux):** official Flathub app, Ubuntu amd64 personal mode only. Updates: `flatpak update --user`.
- ChatGPT/Telemost (Linux): use web apps
- Remote desktop: Windows App or FreeRDP (macOS), Remmina (Linux)
- Some vendor apps unavailable on ARM64

## Editing private fragments

```sh
chezmoi cd
chezmoi edit-encrypted .private/NAME.age
chezmoi diff && chezmoi apply
```

