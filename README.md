# ror

*A run-or-raise application switcher for any X11 desktop*

Based on [jumpapp](https://github.com/mkropat/jumpapp)

The idea is to bind a key for any given application that will:

- launch the application, if it's not already running
- focus the application's window, if it is running

Pressing the key again will cycle to the application's next window, if there's more than one.

In short, **ror** is probably the fastest way for a keyboard-junkie to switch between applications in a modern desktop environment.  Once [installed](#installation), all you have to do is configure the key bindings you want to use:

![Settings Example](http://i.imgur.com/dAj8NDZ.png "On Ubuntu it's under All Settings → Keyboard → Shortcuts")

## Synopsis

    Usage: ror [OPTION]... COMMAND [ARG]...

    Jump to (focus) the first open window for an application, if it's running.
    Otherwise, launch COMMAND (with opitonal ARGs) to start the application.

    Options:
      -r -- cycle through windows in reverse order
      -f -- force COMMAND to launch if process found but no windows found
      -m -- if a single window is already open and in focus - minimize it
      -n -- do not fork into background when launching COMMAND
      -p -- always launch COMMAND when ARGs passed
            (see Argument Passthrough in man page)
      -L -- list matching windows for COMMAND and quit
      -t NAME -- process window has to have NAME as the window title
      -c NAME -- find window using NAME as WM_CLASS (instead of COMMAND)
      -i NAME -- find process using NAME as the command name (instead of COMMAND)
      -w -- only find the applications in the current workspace
      -R -- bring the application to the current workspace when raising
            (the default behaviour is to switch to the workspace that the
            application is currently on)
      -C -- center cursor when raising application

## Installation

    git clone https://github.com/mencargo/ror.git
    cd ror
    sudo cp ror /usr/local/bin

## Argument Passthrough (`-p` option)

Many applications keep track of what windows they have open so that if you run
the command again, it will interact with the existing application window
instead of launching a new instance of the application.

Take Firefox, for example. If you already have a Firefox window open and you
run `firefox https://github.com/`, Firefox won't start a new instance. What it
does is open a new tab in the existing window and browse to the URL you passed.

## A Wrapper Around wmctrl(1)

All the heavy lifting is done by Tomáš Stýblo's powerful
[**wmctrl**](http://tripie.sweb.cz/utils/wmctrl/). You must have it installed to
use **ror**.

**ror** has a good chance to work on [any window manager supported by **wmctrl**](http://tripie.sweb.cz/utils/wmctrl/#about).

## XBindKeys

If your desktop environment doesn't offer a way to bind keys to commands — or if it's too limited — take a look at [XBindKeys](http://www.nongnu.org/xbindkeys/xbindkeys.html).

Example `.xbindkeysrc`:

    "ror firefox"
      control + alt + f

    "ror -r firefox"
      shift + control + alt + f

    "ror -f telegram-desktop"
      control + alt + t
