# How to launch Sway without SystemD (runit, void linux)

## First you want to install needed packages. Go to your user account and do:

sudo xbps-install -S sway seatd dbus elogind polkit

## Now you will have to enable seatd


sudo ln -s /etc/sv/seatd /var/service/

### To check if things are working correctly run:

sudo sv status seatd

## Make sure you are in correct groups. Run this command to make sure:

sudo usermod -aG video,input $(whoami)

If youre not in these groups login in to root and add your user to these groups

## Enable and configure dbus

### To enable dbus run: (If not installed install via xbps-install)

sudo ln -s /etc/sv/dbus /var/service/

### Check if its running:
sudo sv status dbus

### Testing
Run this command:
sway
to enter Sway and check if everything is working correctly and its usable. If screen resolution is wrong its okay.
