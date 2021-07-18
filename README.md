# ror *`run-or-raise` application switcher for X11*

The fastest way for a keyboard-junkie to switch between applications in a modern desktop environment.

Bind a key to launch any given application if it's not already running or raise the application's window if it is.

Pressing the key again will cycle to the application's next window, if there's more than one.

All you have to do is configure the key bindings you want to use.

## Install
### With git
```
git clone https://github.com/mencargo/ror.git
cd ror
sudo cp ror /usr/local/bin
```
### Without git
```
curl https://raw.githubusercontent.com/mencargo/ror/master/ror -o ror.sh
chmod +x ror.sh
sudo cp ror.sh /usr/local/bin/ror
```

## Synopsis
```
Usage: ror [OPTION]... COMMAND [ARG]...

Raise (focus) the first open window for an application, if it's running.
Otherwise, launch COMMAND (with opitonal ARGs) to start the application.

Options:
  -r -- cycle through windows in reverse order
  -f -- force COMMAND to launch if process found but no windows found
  -m -- if a single window is already open and in focus - minimize it
  -n -- do not fork into background when launching COMMAND
  -p -- always launch COMMAND when ARGs passed
  -L -- list matching windows for COMMAND and quit
  -t NAME -- process window has to have NAME as the window title
  -c NAME -- find window using NAME as WM_CLASS (instead of COMMAND)
  -i NAME -- find process using NAME as the command name (instead of COMMAND)
  -w -- only find the applications in the current workspace
  -R -- bring the application to the current workspace when raising
        (the default behaviour is to switch to the workspace that the
        application is currently on)
```

## Argument Passthrough (`-p` option)

Many applications keep track of what windows they have open so that if you run
the command again, it will interact with the existing application window
instead of launching a new instance of the application.

Take Firefox, for example. If you already have a Firefox window open and you
run `firefox https://github.com/`, Firefox won't start a new instance. What it
does is open a new tab in the existing window and browse to the URL you passed.


## XBindKeys

If your desktop environment doesn't offer a way to bind keys to commands (or if it's too limited) take a look at [XBindKeys](http://www.nongnu.org/xbindkeys/xbindkeys.html).

Example `.xbindkeysrc`:
```
"ror firefox"
  control + alt + f

"ror -r firefox"
  shift + control + alt + f

"ror -f telegram-desktop"
  control + alt + t
```


## Requirements

Extremly basic, relies on `bash`, `wmctrl`, `xprop`, `xdotool` and `pgrep`. Already in most devices with X11.

This script was based on [jumpapp](https://github.com/mkropat/jumpapp)
