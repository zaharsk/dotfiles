## Personal dotfiles for macOS

### First time setup
#### Install brew
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

#### Prepare chezmoi
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
chezmoi edit ~/.Brewfile
```
```bash
chezmoi diff
```
```bash
chezmoi apply
```
#### Install brew bundle
```bash
brew bundle list --global --all
```
```bash
brew bundle --global --jobs auto
```

### SSH
#### Add ssh-key
```bash
mkdir -p ~/.ssh

cp ~/Documents/_ssh/id_ed25519 ~/.ssh/
cp ~/Documents/_ssh/id_ed25519.pub ~/.ssh/

chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub

ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

#### Add ssh agent config
```bash
touch ~/.ssh/config
```

```config
Host *
    AddKeysToAgent yes
    UseKeychain yes
    IdentityFile ~/.ssh/id_ed25519
```