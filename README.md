# My OS setup :rocket:

## Change display settings

- Enable fractional settings
- Set to 200% 4k screen, and keep 100% for 1080p

## Change hostname

```
sudo vi /etc/hostname
sudo vi /etc/hosts
sudo reboot
```

## Install Chrome
*https://www.google.com/intl/fr_fr/chrome/*

- Download .deb
- sudo dpkg -i google-chrome-stable_current_amd64.deb
- Set sync on with my profile
- Set Google Chrome use system title bar and borders
- Log in to 1password

## Install Zsh
- sudo apt install zsh
- zsh --version
- Make zsh default shell
- chsh -s $(which zsh)
- Logout to apply update
- Choose to populate with comment .zshrc automatically
- $SHELL --version

## Install ohmyzsh
- sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
- Remove old .zshrc
- rm .zshrc.pre-oh-my-zsh

## Install node version manager n
- curl -L https://git.io/n-install | N_PREFIX=~/.n bash -s -- -y
- Choose version want to use for node ex: n install 12

Note:
> To update n later, run `n-update`.
> To uninstall, run `n-uninstall`.

## Install Rustup

- https://doc.rust-lang.org/book/ch01-01-installation.html
- $ curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
- Add $HOME/.cargo/bin in $PATH

## Install tldr write in Rust

- Install dep
- sudo apt install libssl-dev
- https://tldr.sh/
- cargo install tealdeer
- tldr --version


## Install Alacritty

- Follow manual installation
- https://github.com/alacritty/alacritty/blob/master/INSTALL.md#clone-the-source-code
- Install dev
- apt-get install cmake pkg-config libfreetype6-dev libfontconfig1-dev libxcb-xfixes0-dev python3
- Dont forget NVIDIA lib
- apt-get install libegl1-mesa-dev

- Clone repo on /tmp
- git clone https://github.com/alacritty/alacritty.git
- cd alacritty
- cargo build --release

Term info

- infocmp alacritty
- if nothing appear
- sudo tic -xe alacritty,alacritty-direct extra/alacritty.info


Desktop entry

- sudo cp target/release/alacritty /usr/local/bin
sudo cp target/release/alacritty /usr/local/bin # or anywhere else in $PATH
sudo cp extra/logo/alacritty-term.svg /usr/share/pixmaps/Alacritty.svg
sudo desktop-file-install extra/linux/Alacritty.desktop
sudo update-desktop-database

Manual Page

sudo mkdir -p /usr/local/share/man/man1
gzip -c extra/alacritty.man | sudo tee /usr/local/share/man/man1/alacritty.1.gz > /dev/null


Shell Completion

mkdir -p ${ZDOTDIR:-~}/.zsh_functions
echo 'fpath+=${ZDOTDIR:-~}/.zsh_functions' >> ${ZDOTDIR:-~}/.zshrc

cp extra/completions/_alacritty ${ZDOTDIR:-~}/.zsh_functions/_alacritty

## Make alacritty default terminal

https://frantzroulet.com/blog/other/2018/12/26/how-to-choose-alacritty-as-default-terminal.html

// replace /usr/bin/alacritty with good installation place, show it with which alacritty
sudo update-alternatives --install /usr/bin/x-terminal-emulator x-terminal-emulator /usr/bin/alacritty 50
sudo update-alternatives --config x-terminal-emulator

## install configuration of alacritty

- @TODO add alacritty config
- mv in ~/.alacritty.yml

## Install pure

in /home
git clone https://github.com/sindresorhus/pure.git .pure
add this path $HOME/.pure to fpath
fpath+=$HOME/.pure

and load config in .zshrc

## .zshrc
autoload -U promptinit; promptinit
prompt pure


## Install spotify

flatpak install flathub com.spotify.Client

## Install vscode

https://code.visualstudio.com/
dpkg -i

install Settings sync to pull settings from github gist
// Ctrl P sync dowload settings


## Install alias

- mv .aliases
- add it to .zshrc


## Install the fuck

https://github.com/nvbn/thefuck

sudo apt update
sudo apt install python3-dev python3-pip python3-setuptools
sudo pip3 install thefuck

add in zshrc
eval $(thefuck --alias)

## Intall bat

https://github.com/sharkdp/bat

apt install bat

## Install zsh autosuggestion

https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh

- git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

add pluging in zshrc
plugins=(zsh-autosuggestions)


## Install zsh syntax highligting

https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md

- git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

- plugins=( [plugins...] zsh-syntax-highlighting)
in zshrc

## Install tmux

sudo apt install tmux


## Intall aws-cli

- curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

Add credential in .aws/credentials
and add .aws/confiand add .aws/config

## Install htop

sudo apt install htop

## Add ssh key

ssh-keygen -t rsa -b 4096 -C "artifakt-einz@rastapopoulos"

config file for different keys in .ssh/config

## Install xclip

sudo apt install xclip

## Install tablePlus

https://tableplus.com/blog/2019/10/tableplus-linux-installation.html

-Add TablePlus gpg key
wget -O - -q http://deb.tableplus.com/apt.tableplus.com.gpg.key | sudo apt-key add -

-Add TablePlus repo
sudo add-apt-repository "deb [arch=amd64] https://deb.tableplus.com/debian tableplus main"

-Install
sudo apt update
sudo apt install tableplus

## Install MyCLI

https://github.com/dbcli/mycli

pip install -U mycli

## Install mysql-cli

sudo apt install mysql-client

## Install docker

- sudo apt install docker.io
- sudo apt install docker-compose

## Install yarn

npm i --global yarn


## Git config

git config --global user.name "zagonine"
git config --global user.email "mail@enzogain.com"

## Install Slack

https://slack.com/intl/fr-fr/downloads/instructions/ubuntu

- dpkg -i

## Install php 7.4 for console

sudo apt install php7.4 php7.4-mysql php7.4-xml php7.4-intl php7.4-gd php7.4-curl

## Install of envv command for environment variable for artifakt
- Add in alias, install override prompt pure


## Install gnome tweak tools

sudo apt install gnome-tweaks

## Install gnome extensions

- install chrome extensions
- install user-theme
https://extensions.gnome.org/extension/19/user-themes/
- install caffeine
https://extensions.gnome.org/extension/517/caffeine/
- install panel OSD
https://extensions.gnome.org/extension/708/panel-osd/
- install top panel workspace scroll
https://extensions.gnome.org/extension/701/top-panel-workspace-scroll/
- hide top bar
https://extensions.gnome.org/extension/545/hide-top-bar/


## Install arc-theme

sudo apt install arc-theme
selet it in tweak tool

## Install Arc icons + la capitaine
https://github.com/horst3180/arc-icon-theme
https://github.com/keeferrourke/la-capitaine-icon-theme


mkdir .icons
cd .icons

git clone https://github.com/keeferrourke/la-capitaine-icon-theme.git La-Capitaine

For Arc,
clone in /tmp
git clone https://github.com/horst3180/arc-icon-theme.git
mv /tmp/Arc ~/.icons

update index.theme of Arc line Inherits and add La-Capitaine in first position
Inherits=La-Capitaine,Moka,Adwaita,gnome,hicolor


## Install discord

https://discord.com/
dpkg -i
