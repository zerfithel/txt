# How to launch Sway without SystemD (runit, void linux)

## First you want to install needed packages. Go to your user account and do:

sudo xbps-install -S sway seatd dbus elogind polkit

## Now you will have to enable seatd


$ sudo ln -s /etc/sv/seatd /var/service/

### To check if things are working correctly run:

$ sudo sv status seatd

## Make sure you are in correct groups. Run this command to make sure:

$ sudo usermod -aG video,input $(whoami)

If youre not in these groups login in to root and add your user to these groups

## Enable and configure dbus

### To enable dbus run: (If not installed install via xbps-install)

$ sudo ln -s /etc/sv/dbus /var/service/

### Check if its running:
$ sudo sv status dbus

### Testing
Generate Sway config:

$ sudo cp -r /etc/sway /home/yourusername/.config/sway

Run this command to test Sway:
sway
to enter Sway and check if everything is working correctly and its usable. If screen resolution is wrong its okay.

## If it didnt work install your GPU drivers

Intel:
$ sudo xbps-install xf86-video-intel
AMDGPU:
$ sudo xbps-install xf86-video-amdgpu
NVIDIA: (Only Nouveau will work on Wayland)
$ sudo xbps-install xf86-video-nouveau

Configure bash:
$ export XDG_RUNTIME_DIR=/run/user/$(id -u)
$ export WAYLAND_DISPLAY=wayland-1
$ export XDG_SRSSION_TYPE=wayland
(Also add this lines to .bashrc but without export and reboot)

$ sudo reboot

Make sure /run/user/$(id -u) exists and perms are configured correctly
To do that, run (RUN AS A USER, NOT ROOT)
$ sudo ls -h /run/user/$(id -u)
If it doesnt exist create it:
$ sudo mkdir -p /run/user/$(id -u)
$ sudo chmod 700 /run/user/$(id -u)
# OPTIONAL

## Login window

$ sudo xbps-install greetd
$ sudo ln -s /etc/sv/greetd /var/service/
$ sudo sv status greetd

## Screenshot tool, clipboard for Neovim/Vim, and essential tools

# Nice tools to have installed:

$ sudo xbps-install btop htop parted gparted xmirror grim mako xwayland neovim cowsay git base-devel cfdisk fdisk
