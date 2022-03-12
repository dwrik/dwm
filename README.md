# dwm - dynamic window manager

This is my build of dwm (6.3) from suckless. It contains the following patches applied:

- alpha - for transparency in status bar and border fix
- fullgaps - for gaps in b/w clients and the desktop
- xrdb - loads colors from Xresources (pywal compatible)
- movestack - for changing client's position through the stack

## Keybindings

For keybindings, take a look at the `static Key keys[]` array in the `config.def.h` file. This build uses `Super` (Windows key) as the `MODKEY`.The keybindings are defined using the keysyms defined in the X11 protocol which can be found [here](https://cgit.freedesktop.org/xorg/proto/x11proto/tree/).

This build also has some bindings which uses my own scripts (powermenu, sniping-tool, emojimenu) which can be found in my dotfiles repo.

## Commands

Keybindings are bound to either internal dwm functions or the `spawn` function which takes custom commands to execute along with their arguments.

`spawn` commands can be executed directly by defining them as commands and arguments like so:
```
static const char *locksessioncmd[] = { "loginctl", "lock-session", NULL };
```
dwm also provides an option to execute commands in a shell like environment using the `SCHMD` macro in case shell features such as piping or conditionals are required.
```
SHCMD("amixer set Master 5%+ unmute && pkill -RTMIN+10 dwmblocks")
```

## Requirements

In order to build dwm you need the Xlib header files.

## Installation
Edit config.mk to match your local setup (dwm is installed into the /usr/local namespace by default).

Afterwards enter the following command to build and install dwm (if necessary as root):
```
make clean install
```

## Running dwm

Add the following line to your .xinitrc to start dwm using startx:
```
exec dwm
```
In order to connect dwm to a specific display, make sure that the DISPLAY environment variable is set correctly, e.g.:
```
DISPLAY=foo.bar:1 exec dwm
```
(This will start dwm on display :1 of the host foo.bar.)

In order to display status info in the bar, you can do something like this in your .xinitrc:
```
while xsetroot -name "`date` `uptime | sed 's/.*,//'`"
do
    sleep 1
done &
exec dwm
```
or use a status monitor like dwmblocks (refer to the suckless website for alternatives).

## Configuration

The configuration of dwm is done by creating a custom config.h and (re)compiling the source code.
