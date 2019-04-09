# Instructions
This is the instructions of all setups that I made for i3 on Ubuntu 18.4.

## Touchpad Click and Scroll
When add i3 to a notebook, the "tap click" won't work anymore.
In order to make tap click work again, it's necessary to create a x11 conf.

1. Create the folder and config file:
```
sudo mkdir -p /etc/X11/xorg.conf.d
sudo touch /etc/X11/xorg.conf.d/90-touchpad.conf
```
2. Add configuration
```
Section "InputClass"
        Identifier "touchpad"
        MatchIsTouchpad "on"
        Driver "libinput"
        Option "Tapping" "on"
	Option "NaturalScrolling" "On"
EndSection
```
*the configuration `Option "NaturalScrolling" "On"` is to reverse scroll direction using 2 fingers on the touchpad.*

## Brightness
For brightness control I'm using "light", which is a package for ArchLinux but, it is fairly easy to make and install on other distributions.
Here it how install on Ubuntu:

* If not already installed, install automake and autoconf
```
sudo apt-get update
sudo apt-get install automake autoconf
```

* Clone and install
```
git clone git clone https://github.com/haikarainen/light.git
cd light
./autogen.sh
./configure && make
sudo make install
```
* Add the following line on `~/.i3/conf`
```
# Screen brightness controls with notification
bindsym XF86MonBrightnessUp exec "light -A 5; notify-send 'brightness up'"
bindsym XF86MonBrightnessDown exec "light -U 5; notify-send 'brightness down'"
```

## Audio
For sound I'm using `pavucontrol`. It's good because it can be used on a GUI or via multimidia keys.

* Install
```
sudo apt-get install pavucontrol
```

* Add the following lines to `~/.i3/conf`
```
bindsym XF86AudioRaiseVolume exec --no-startup-id pactl -- set-sink-volume 0 +5% #increase sound volume
bindsym XF86AudioLowerVolume exec --no-startup-id pactl -- set-sink-volume 0 -5% #decrease sound volume
bindsym XF86AudioMute exec --no-startup-id pactl set-sink-mute 0 toggle # mute sound

# Media player controls
bindsym XF86AudioPlay exec playerctl play
bindsym XF86AudioPause exec playerctl pause
bindsym XF86AudioNext exec playerctl next
bindsym XF86AudioPrev exec playerctl previous
```

## Network
TBD
