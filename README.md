# My Pop!_OS setup :rocket:
*Pop!_OS 20.10*

## Change display settings

- Enable fractional settings
- Set scale to 200% for the 4k monitor, and keep 100% for 1080p

## Change hostname

```
sudo vi /etc/hostname
sudo vi /etc/hosts
sudo reboot
```

## Install Chrome
*https://www.google.com/intl/fr_fr/chrome/*

- Download `.deb` and `sudo dpgk -i [...]`
- Set Google Chrome to use system title bar and borders
- Setup my account for syncing and login to password manager

## Install Zsh and setup to be default shell
*https://www.zsh.org/*

```
sudo apt install zsh
zsh --version
chsh -s $(which zsh)
```
- Logout to apply change of default shell
- Choose option to empty .zshrc as ohmyzsh will replace it
- Check installation okay with `$SHELL --version`

## Install ohmyzsh
*https://github.com/ohmyzsh/ohmyzsh/*

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
- Remove backup install made of previous zsh config`rm .zshrc.pro-oh-my-zsh`

Note:
- [.zshrc](config_files/.zshrc)

## Install node version manager: "n"
*https://github.com/tj/n*

```
curl -L https://git.io/n-install | N_PREFIX=~/.n bash -s -- -y
```

Note:
> To update n later, run `n-update`.  
> To uninstall, run `n-uninstall`.

## Install Rustup
*https://rustup.rs/*

```
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```
- Add `$HOME/.cargo/bin` in `$PATH`

## Install tldr write in Rust
*https://tldr.sh/*

- Install needed dependency `sudo apt install libssl-dev`
```
cargo install tealdeer
tldr --version
```
- Setup with ohmyzsh
  - If you’re using oh-my-zsh, create a directory for custom plugins (if it doesn’t exist):

    `mkdir -p $ZSH_CUSTOM/plugins/tldr`

  - Create a symbolic link to the zsh completion script:

    `ln -s bin/completion/zsh/_tldr $ZSH_CUSTOM/plugins/tldr/_tldr`

  - Add tldr to your oh-my-zsh plugins. Edit your ~/.zshrc file and add it to the plugins section:

    `plugins=(git tmux tldr)`

## Install Alacritty
*https://github.com/alacritty/alacritty/blob/master/INSTALL.md#clone-the-source-code*

### Manual installation
- Install dependencies
```
apt-get install cmake pkg-config libfreetype6-dev libfontconfig1-dev libxcb-xfixes0-dev python3
# Dont forget NVIDIA lib
apt-get install libegl1-mesa-dev
```

- Clone and build in `/tmp`
```
git clone https://github.com/alacritty/alacritty.git
cd alacritty
cargo build --release
```

- Terminfo
```
infocmp alacritty
# if not present run below 
sudo tic -xe alacritty,alacritty-direct extra/alacritty.info
```

- Desktop entry
```
sudo cp target/release/alacritty /usr/local/bin
sudo cp target/release/alacritty /usr/local/bin # or anywhere else in $PATH
sudo cp extra/logo/alacritty-term.svg /usr/share/pixmaps/Alacritty.svg
sudo desktop-file-install extra/linux/Alacritty.desktop
sudo update-desktop-database
```

- Manual Page
```
sudo mkdir -p /usr/local/share/man/man1
gzip -c extra/alacritty.man | sudo tee /usr/local/share/man/man1/alacritty.1.gz > /dev/null
```

- Shell Completions
```
mkdir -p ${ZDOTDIR:-~}/.zsh_functions
echo 'fpath+=${ZDOTDIR:-~}/.zsh_functions' >> ${ZDOTDIR:-~}/.zshrc
cp extra/completions/_alacritty ${ZDOTDIR:-~}/.zsh_functions/_alacritty
```

## Make alacritty default terminal
*https://frantzroulet.com/blog/other/2018/12/26/how-to-choose-alacritty-as-default-terminal.html*

```
sudo update-alternatives --install /usr/bin/x-terminal-emulator x-terminal-emulator $(which alacritty) 50
sudo update-alternatives --config x-terminal-emulator
```

## Install configuration of alacritty

- Place [.alacritty.yml](config_files/.alacritty.yml) in `$HOME`

## Install pure
*https://github.com/sindresorhus/pure*

```
cd $HOME
git clone https://github.com/sindresorhus/pure.git .pure
```
- add path $HOME/.pure to fpath `fpath+=$HOME/.pure`
- add code below in `.zshrc`
```
autoload -U promptinit; promptinit
prompt pure
```

## Install spotify
*https://flathub.org/apps/details/com.spotify.Client*

flatpak install flathub com.spotify.Client

## Install vscode
*https://code.visualstudio.com/*

- Download `.deb` and `sudo dpgk -i [...]`
- Turn on sync and replace local config with uploaded one

## Install alias

- Add in [.aliases](config_files/.aliases) in `$HOME`
- Include it in `.zshrc` with `source $HOME/.aliases`

## Install the fuck
*https://github.com/nvbn/thefuck*

```
sudo apt update
sudo apt install python3-dev python3-pip python3-setuptools
sudo pip3 install thefuck
```

.zshrc
```
eval $(thefuck --alias)
```

## Intall bat
*https://github.com/sharkdp/bat*

```
sudo apt install bat
```

## Install zsh autosuggestion
*https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh*

```
- git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

.zshrc
```
plugins=([...] zsh-autosuggestions)
```


## Install zsh syntax highligting
*https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md*

```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

.zshrc
```
plugins=([...] zsh-syntax-highlighting)
```

## Install tmux
*https://github.com/tmux/tmux*

```
sudo apt install tmux
```

## Install tpm (Tmux Plugin Manager)
*https://github.com/tmux-plugins/tpm*

```
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```
- Add at the end of `.tmux.conf` `run '~/.tmux/plugins/tpm/tpm'`

## Install tpm Dracula/tmux
*https://github.com/dracula/tmux*

Add in `.tmux.conf`
```
set -g @plugin 'dracula/tmux'
set -g @dracula-show-battery false
set -g @dracula-show-network false
set -g @dracula-show-location false
set -g @dracula-show-fahrenheit false
set -g @dracula-border-contrast true
set -g @dracula-cpu-usage true
set -g @dracula-ram-usage true
set -g @dracula-gpu-usage true
set -g @dracula-military-time true
set -g @dracula-show-timezone false
set -g @dracula-show-weather false
```

## .tmux.conf

Current `.tmux.conf` [here](config_files/.tmux.conf)

## Tmux template for artifakt

See [.tmux_artifakt_template](config_files/.tmux_artifakt_template)

## Install vim
*https://github.com/vim/vim*

```
sudo apt install vim
```

## Install vim theme dracula
*https://github.com/dracula/vim*

```
mkdir -p ~/.vim/pack/themes/start
cd ~/.vim/pack/themes/start
git clone https://github.com/dracula/vim.git dracula
```

Add this `~/.vimrc`
```
packadd! dracula
syntax enable
let g:dracula_colorterm = 0 " without that, background is grey (https://github.com/dracula/vim/issues/96)
colorscheme dracula
```

## .vimrc

Current `.vimrc` [here](config_files/.vimrc)

## Intall aws-cli
*https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html#cliv2-linux-install*

```
cd /tmp
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

- Add credential in .aws/credentials and .aws/config

## Install htop
*https://htop.dev/*

```
sudo apt install htop
```

## Generate ssh keys

```
ssh-keygen -t rsa -b 4096 -C "name@hostname"
```

## Install xclip
*https://github.com/astrand/xclip*

```
sudo apt install xclip
```

## Install tablePlus
*https://tableplus.com/blog/2019/10/tableplus-linux-installation.html*

```
wget -O - -q http://deb.tableplus.com/apt.tableplus.com.gpg.key | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://deb.tableplus.com/debian tableplus main"
sudo apt update
sudo apt install tableplus
```

## Install MyCLI
*https://github.com/dbcli/mycli*

```
pip install -U mycli
```

## Install mysql-cli
*https://dev.mysql.com/doc/refman/8.0/en/programs-client.html*

```
sudo apt install mysql-client
```

## Install docker
*https://docs.docker.com/engine/install/ubuntu/*

```
sudo apt install docker.io
sudo apt install docker-compose
```

## Install yarn
*https://yarnpkg.com/*

```
npm i --global yarn
```


## Git config

```
git config --global user.name "zagonine"
git config --global user.email "mail@enzogain.com"
```

## Install Slack
*https://slack.com/intl/fr-fr/downloads/instructions/ubuntu*

- Download `.deb` and `sudo dpgk -i [...]`

## Install php 7.4 for console

```
sudo apt install php7.4 php7.4-mysql php7.4-xml php7.4-intl php7.4-gd php7.4-curl
```

## Install of envv command for environment variable for artifakt
- Add in alias command `envv`
- Install override prompt pure to display current environment variables

## Install gnome tweak tools

```
sudo apt install gnome-tweaks
```
> Note: install gnome-extensions in browser if not already added

## Install gnome extensions

- https://extensions.gnome.org/extension/19/user-themes/
- https://extensions.gnome.org/extension/517/caffeine/
- https://extensions.gnome.org/extension/708/panel-osd/
- https://extensions.gnome.org/extension/701/top-panel-workspace-scroll/
- https://extensions.gnome.org/extension/545/hide-top-bar/

## Install arc-theme
*https://github.com/horst3180/arc-theme*

```
sudo apt install arc-theme
```
- select it in tweak tool

## Install Arc icons + la capitaine
*https://github.com/horst3180/arc-icon-theme*
*https://github.com/keeferrourke/la-capitaine-icon-theme*

```
mkdir .icons
cd .icons
git clone https://github.com/keeferrourke/la-capitaine-icon-theme.git La-Capitaine
cd /tmp
git clone https://github.com/horst3180/arc-icon-theme.git
mv /tmp/arc-icon-theme/Arc ~/.icons
```
- update `index.theme` of to include La-Capitaine in first position inherit
```
Inherits=La-Capitaine,Moka,Adwaita,gnome,hicolor
```
- select Arc icons in tweak tools

## Install discord
*https://discord.com/*

- Download `.deb` and `sudo dpgk -i [...]`

## Compose key
*All default compose is here: `/usr/share/X11/locale/en_US.UTF-8/Compose`*

- Enable compose key on `Alt-Rigth` in gnome settings
- Copy [.XCompose](config_files/.XCompose) file in `$HOME`

## Play/Previous/Next shortcut for Spotify 
*Those shorcuts will trigger action only on Spotify! If want to be globally just set it in `Settings > Keyboard > Keyboard Shortcuts > Sound and Media`)*

- In `Settings > Keyboard > Keyboard Shortcuts > Custom Shortcuts`
- Add following
```
# Super+8
dbus-send --print-reply --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.PlayPause

# Super+7 
dbus-send --print-reply --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.Previous

# Super+9
dbus-send --print-reply --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.Next
```

## Set shortcut for volume

- In `Settings > Keyboard > Keyboard Shortcuts > Sound and Media`

- Volume down on `Super+-`
- Volume up on `Super+=`
- Volume mute/unmute on `Super+0`

## Install httpie
*https://httpie.io/*

```
sudo apt install httpie
```

## Remove anoying shortcut: <Super>P
*https://askubuntu.com/questions/68463/how-to-disable-global-super-p-shortcut#:~:text=Install%20the%20dconf%2Dtools%20package,Uncheck%20the%20active%20checkbox.*

- Get value of `gsettings get org.gnome.mutter.keybindings switch-monitor`
- In my case it returns `['<Super>p', 'XF86Display']`
- Add set empty array to remove the shortcut
- `gsettings set org.gnome.mutter.keybindings switch-monitor "[]"`

## Install PulseAudio Volume Control
*https://freedesktop.org/software/pulseaudio/pavucontrol/*  

Control output sound of each application

```
sudo apt install pavucontrol
```


## Remove general `Ctrl+Shift+e` shortcut
*https://github.com/microsoft/vscode/issues/48480#issuecomment-414464079*

If we keep this shortcut, we are not able to use this one for open "Explorer" in VSCode  

```
ibus-setup
```

Go to > Emoji > Remove "Emoji annotation" shortcut (it should be set to the unwanted shortcut Ctrl+Shift+e)
