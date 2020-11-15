# My OS setup :rocket:
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

- Place [config_files/.alacritty.yml](.alacritty.yml) in `$HOME`

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

- Add in [config_files/.aliases](.aliases) in `$HOME`
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

ssh-keygen -t rsa -b 4096 -C "name@hostname"

## Install xclip
*https://github.com/astrand/xclip*

sudo apt install xclip

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

## Install gnome extensions

https://extensions.gnome.org/extension/19/user-themes/
https://extensions.gnome.org/extension/517/caffeine/
https://extensions.gnome.org/extension/708/panel-osd/
https://extensions.gnome.org/extension/701/top-panel-workspace-scroll/
https://extensions.gnome.org/extension/545/hide-top-bar/

## Install arc-theme
*https://github.com/horst3180/arc-theme*

```
sudo apt install arc-theme
```
- select it in tweak tool

## Install Arc icons + la capitaine
https://github.com/horst3180/arc-icon-theme
https://github.com/keeferrourke/la-capitaine-icon-theme

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
