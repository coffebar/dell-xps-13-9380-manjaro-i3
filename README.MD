# xps 13 9380 manjaro i3

## Here's my setup
![2021_09_03](https://user-images.githubusercontent.com/3100053/131967232-c4f539ab-12ed-48f6-9e23-8721744fb68f.png)

## Things i do after installing Manjaro (i3wm)

Note: avoid kernel version 5.10.59, use 5.13.11 or try newer one. Otherwise, there may be serious graphics problems when booting the system. You can use manjaro-settings-manager to install kernels.

I prefer to install additional software:

```bash
sudo pacman -S \
arc-gtk-theme deepin-icon-theme-manjaro \
adobe-source-code-pro-fonts keepassxc \
alacritty firefox rofi pulseaudio git i3-gaps \
lxappearance xdotool xautomation wmctrl wget curl \
vlc gimp virtualbox vim barrier neovim dropbox \
flameshot fzf rsync xclip xmodmap numlockx \
xxkb telegram-desktop xfce4-taskmanager \
thunar-volman thunar-archive-plugin \
nodejs neofetch ttf-dejavu libreoffice \
file-roller bat baobab pavucontrol \
simplescreenrecorder imagemagick \
xsecurelock xbindkeys goaccess
```

more from AUR:

```jsx
sudo pamac install \
dell-command-configure \
docker \
arch-linux-2d-wallpapers \
pix \
autorandr \
google-chrome \
ttf-ms-fonts \
polybar-git \
ttf-font-awesome-4

sudo usermod -aG docker $USER
sudo systemctl enable autorandr.service
```

+pip3:

```bash
pip install autotiling neovim pynvim ueberzug
```

+follow manuals:

[https://wiki.archlinux.org/title/ECryptfs#Encrypting_a_home_directory](https://wiki.archlinux.org/title/ECryptfs#Encrypting_a_home_directory)

[https://github.com/bulletmark/libinput-gestures](https://github.com/bulletmark/libinput-gestures)

[https://github.com/junegunn/vim-plug](https://github.com/junegunn/vim-plug)

[https://ohmyz.sh/#install](https://ohmyz.sh/#install)

Fix time:

```jsx
systemctl enable --now systemd-timesyncd.service
timedatectl set-ntp true
```

Change default shell to zsh:

```bash
sudo chsh -s $(which zsh)
```

Disable services i don't need:

```bash
sudo systemctl disable avahi-daemon.service
sudo systemctl disable cups.service
sudo systemctl disable ModemManager.service
sudo systemctl disable lvm2-monitor.service
sudo systemctl disable bluetooth.service
sudo bluetooth off
# enable TRIM
sudo systemctl enable fstrim.timer
```

Laptop battery life can be prolonged by limiting the charge level to 80%

```bash
sudo /opt/dell/dcc/cctk --PrimaryBattChargeCfg=Custom:60-80
# default is PrimaryBattChargeCfg=PrimAcUse
```

Edit file /etc/lightdm/lightdm.conf 

```bash
[LightDM]
...
# this should be enabled to avoid "Lightdm failed to start" error
logind-check-graphical=true
```

Camera can be disabled from BIOS option by using "Dell Command | Configure":

```bash
sudo /opt/dell/dcc/cctk --Camera=Disabled

# for security reason we can remove dell-command-configure until don't need it
sudo pamac remove dell-command-configure
```

Enable firewall

```bash
sudo systemctl enable ufw
```

swap:

create a file /etc/sysctl.d/100-swap.conf

> vm.swappiness=10

and follow [https://wiki.manjaro.org/index.php/Swap#Using_a_Swapfile](https://wiki.manjaro.org/index.php/Swap#Using_a_Swapfile) to create a swap file.


Login screen background can be changed in /etc/lightdm/slick-greeter.conf

![Arch5.jpg](https://64.media.tumblr.com/2d53e8f1486b6bb22e74f8e80073be4b/694a6580a1372c75-7d/s1280x1920/b16ea4d525f26004e90331d12e1a72341b1954e7.jpg)

```
background=/usr/share/backgrounds/arch-linux-2d/Arch5.jpg
```

Install syncthing:

```
sudo pacman -S syncthing
sudo ufw allow syncthing
systemctl enable --user syncthing.service
systemctl start --user syncthing.service
firefox http://127.0.0.1:8384/
```
