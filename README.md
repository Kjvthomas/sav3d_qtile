#+TITLE: Qtile Config
#+PROPERTY: header-args :tangle config.py

* About This Config
#+CAPTION: Qtile Scrot
#+ATTR_HTML: :alt Qtile Scrot :title Qtile Scrot :align left
[[https://i.redd.it/o7y95c4glfl71.png]]

* Features of Qtile
- Simple, small and extensible. It's easy to write your own layouts, widgets and commands.
- Configured in Python.
- Command shell that allows all aspects of Qtile to be managed and inspected.
- Complete remote scriptability - write scripts to set up workspaces, manipulate windows, update status bar widgets and more.
- Qtile's remote scriptability makes it one of the most thoroughly unit-tested window managers around.

* Imports
These are python modules that must be imported for this config.

#+BEGIN_SRC python
# -*- coding: utf-8 -*-
import os
import re
import socket
import subprocess
from libqtile import qtile
from libqtile.config import Click, Drag, Group, KeyChord, Key, Match, Screen
from libqtile.command import lazy
from libqtile import layout, bar, widget, hook
from libqtile.lazy import lazy
from typing import List  # noqa: F401
#+END_SRC

* Variables
Just some variables I am setting to make my life easier.

#+BEGIN_SRC python
mod = "mod4"              # Sets mod key to SUPER
myTerm = "kitty"      # My terminal of choice
myBrowser = "librewolf" # My terminal of choice
myDmenu = "dmenu_run -c -bw 2 -l 20 -g 4 -p 'Run'" #dmenu
myEditor = "atom" #atom
myFile = "pcmanfm" #pcmanfm
myGFX = "gimp" #gimp
mySVG = "inkscape"
myOffice = "libreoffice"
myLogOut = "arcolinux-logout"
myWallpaper = "dwall -s earth"
myStats = "urxvt -T 'bpytop' -e bpytop"
myMath = "galculator"
myUpdate = "pamac-manager"
myCloud = "/home/sav3d/Applications/Nextcloud-3.3.1-x86_64_332d890d59fed28c70f0e58f2a1b04f3.AppImage"
#+END_SRC

* Keybindings
These are the keybindings for qtile.

| A FEW IMPORTANT KEYBINDINGS | ASSOCIATED ACTION                                                        |
|-----------------------------+--------------------------------------------------------------------------|
| MODKEY + RETURN             | opens killy terminal                                                     |
| MODKEY + SHIFT + RETURN     | opens pcmanfm                                                            |
| MODKEY + TAB                | rotates through the available layouts                                    |
| MODKEY + q                  | closes window with focus                                                 |
| MODKEY + SHIFT + r          | restarts qtile                                                           |
| MODKEY + 1-9                | switch focus to workspace (1-9)                                          |
| MODKEY + SHIFT + 1-9        | send focused window to workspace (1-9)                                   |
| MODKEY + SHIFT + j          | lazy layout shuffle_down (rotates the windows in the stack)              |
| MODKEY + SHIFT + k          | lazy layout shuffle_up (rotates the windows in the stack)                |
| MODKEY + h                  | bpytop                                                                   |
| MODKEY + r                  | reloads dwall                                                            |
| MODKEY + g                  | opens gimp.                                                              |
| MODKEY + i                  | opens inkscape.                                                          |
| MODKEY + c                  | opens galculator                                                         |
| MODKEY + n                  | opens my appimage nextcloud                                              |
| MODKEY + x                  | arcolinux-logout.                                                        |
| MODKEY + e                  | opens atom                                                               |
| MODKEY + w                  | librewolf                                                                |
| MODKEY + d                  | dmenu.                                                                   |
| MODKEY + u                  | ulauncher                                                                |
| MODKEY + o                  | libreoffice                                                              |


* Startup applications
The applications that should autostart every time qtile is started.
#+BEGIN_SRC startup
## run (only once) processes which spawn with different name
if (command -v gnome-keyring-daemon && ! pgrep gnome-keyring-d); then
    gnome-keyring-daemon --daemonize --login &
fi
if (command -v start-pulseaudio-x11 && ! pgrep pulseaudio); then
    start-pulseaudio-x11 &
fi
#if (command -v /usr/lib/mate-polkit/polkit-mate-authentication-agent-1 && ! pgrep polkit-mate-aut) ; then
    #/usr/lib/mate-polkit/polkit-mate-authentication-agent-1 &
#fi
if (command -v  xfce4-power-manager && ! pgrep xfce4-power-man) ; then
    xfce4-power-manager &
fi
# System-config-printer-applet is not installed in minimal edition
if (command -v system-config-printer-applet && ! pgrep applet.py ); then
  system-config-printer-applet &
fi
xfsettingsd &
run nm-applet &
picom &
light-locker &
compton --shadow-exclude '!focused' &
xcape -e 'Super_L=Super_L|Control_L|Escape' &
#run thunar --daemon &
/usr/lib/polkit-gnome/polkit-gnome-authentication-agent-1 &
pa-applet &
volumeicon &
pamac-tray &
conky &
dwall -s earth &
numlockx on &
# blueman-applet and msm_notifier are not installed in minimal edition
blueman-applet &
msm_notifier &
torguard &
/home/sav3d/Applications/Nextcloud-3.3.1-x86_64_332d890d59fed28c70f0e58f2a1b04f3.AppImage &
#+END_SRC