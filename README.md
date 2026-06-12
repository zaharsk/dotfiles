# Personal dotfiles for macOS

## First time setup
### Install brew
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
```bash
echo >> "/Users/${USER}/.zprofile"
echo 'eval "$(/opt/homebrew/bin/brew shellenv zsh)"' >> "/Users/${USER}/.zprofile"
eval "$(/opt/homebrew/bin/brew shellenv zsh)"
```
```bash
brew bundle dump --global --force
```

### Prepare chezmoi
```bash
brew install chezmoi
```
```bash
chezmoi init
```
```bash
chezmoi add ~/.Brewfile
```
```bash
chezmoi edit --watch ~/.Brewfile
```
### Install brew bundle
```bash
brew bundle list --global --all
```
```bash
brew bundle --global --jobs auto
```

## SSH
### Add ssh-key
```bash
mkdir -p ~/.ssh

cp ~/Documents/_ssh/id_ed25519 ~/.ssh/
cp ~/Documents/_ssh/id_ed25519.pub ~/.ssh/

chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub

ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

### Add ssh agent config
```bash
touch ~/.ssh/config
```
```bash
chezmoi add ~/.ssh/config
```
```bash
chezmoi edit --watch ~/.ssh/config
```

```config
Host *
    AddKeysToAgent yes
    UseKeychain yes
    IdentityFile ~/.ssh/id_ed25519
```

## Environment variables
```bash
mkdir -p ~/.config/shell && touch ~/.config/shell/env
```
```bash
chezmoi add ~/.config/shell/env
```
```bash
chezmoi edit --watch ~/.config/shell/env
```
```ini
export EDITOR="nvim"
export VISUAL="code --wait"

export GITHUB_USERNAME="zaharsk"
export GITHUB_NAME="Zakhar Skorokhodov"
export GITHUB_EMAIL="zaharsk@gmail.com"
```
```bash
chezmoi add ~/.zprofile
```
```bash
chezmoi edit --watch ~/.zprofile
```
```bash
# Load user env, aliases and functions
for file in ~/.config/shell/*; do
    [[ -f "$file" ]] && source "$file"
done
```

> [!WARNING]
> Restart you terminal app here

```bash
chezmoi cd
```
```bash
git add . 
```
```bash
git commit -m "chore: Initial commit"
```
```bash
remote add origin git@github.com:$GITHUB_USERNAME/dotfiles.git
```
```bash
git branch -M main
```
```bash
git push -u origin main
```
```bash
exit
```

## Alacritty
```bash
mkdir -p ~/.config/alacritty/ && touch ~/.config/alacritty/alacritty.toml
```
```bash
chezmoi add ~/.config/alacritty/alacritty.toml
```
```bash
chezmoi edit --watch ~/.config/alacritty/alacritty.toml
```
```toml
[general]
live_config_reload = true

[window]
padding = { x = 4, y = 4 }
dynamic_padding = true
opacity = 0.5
blur = true

[font]
normal = { family = "JetBrainsMono Nerd Font Mono", style = "Regular" }
bold = { family = "JetBrainsMono Nerd Font Mono", style = "Bold" }
italic = { family = "JetBrainsMono Nerd Font Mono", style = "Italic" }
bold_italic = { family = "JetBrainsMono Nerd Font Mono", style = "Bold Italic" }
size = 12.0
```
> [!NOTE]
> Disable `live_config_reload` after all experiments
