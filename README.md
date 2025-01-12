# Ubuntu Start

### Table of contents

- [Update packages](#update-packages)
- [ZSH](#install-and-set-zsh-as-default-shell)
- [Essentials](#install-essential-packages)
- [NodeJS and NPM](#install-latest-version-of-nodejs-and-npm)
- [Neovim](#install-latest-version-of-neovim-using-the-appimage)
- [FZF](#install-fzf)
- [Pure prompt](#install-pure-prompt)
- [Dotfiles](#dotfiles)

### Update packages

```sh
sudo apt update && sudo apt upgrade -y && sudo apt dist-upgrade
```

### Install and set zsh as default shell

```sh
sudo apt install zsh
chsh -s $(which zsh)
```

### Install essential packages

```sh
sudo apt install tmux stow git vim net-tools apt-transport-https ca-certificates openvpn unzip bat curl wget python3-pip python3-venv zsh-syntax-highlighting zsh-autosuggestions
```

### Install latest version of NodeJS and NPM

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

Run these commands before using `nvm`:
```sh
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
```

Now install latest version of node (in this case 23):
```sh
nvm install 23
```

Check versions:
```sh
node -v
npm -v
```

### Install latest version of Neovim using the appimage

Download the appimage:
```sh
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim.appimage
```

Make it executable:
```sh
chmod u+x nvim.appimage
```

Run:
```sh
./nvim.appimage
```
Move the appimage to `/usr/bin/nvim`.  

If the appimage doesn't execute (probably because FUSE is note installed), then run it using `--appimage-extract` flag:
```sh
./nvim.appimage --appimage-extract
```

Move the squashfs-root directory to root (`/`) and add a symlink as shown:
```sh
sudo mv squashfs-root /
sudo ln -s /squashfs-root/AppRun /usr/bin/nvim
```

Now you can use the `nvim` command to run neovim.

### Install FZF
```sh
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
~/.fzf/install
```

### Install Pure prompt
```sh
npm install --global pure-prompt
```

### Dotfiles

Clone the repo:
```sh
git clone https://github.com/dasShounak/dotfiles.git
```

Setup github ssh:
```sh
ssh-keygen -t ed25519 -C "your@email.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

Add the public key to your GitHub account
```sh
cat ~/.ssh/id_ed25519.pub
git clone git@github.com:dasShounak/dotfiles.git
```

Go inside the repo:
```sh
cd dotfiles
```

Delete these two files (or run `stow -n .` and it will show which files already exist. Remove those files):
```sh
rm ~/.profile
rm ~/.zshrc
```

Run stow:
```sh
stow .
```

---

All done!
