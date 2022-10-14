# st - simple terminal

`st` is a simple terminal emulator for X which sucks less.

## Changes

The following sections describe the various changes I have added to the st
codebase. The suckless documentation, FAQ, legacy notice, and license for `st`
can be found in the `suckless` directory.

## Build

The config.mk file has had the `PREFIX` variable changed from `/usr/local/` to
`~/.local/`. This allows the st tool to only be installed for my user without 
having to use sudo.

## config.h

The following section describes no patch related changes made to the `config.h`
header file.

### Font

The terminal font has been modified to the following:

```c
static char *font = "Source Code Pro:pixelsize=14:antialias=true:autohint=true";
```

### Constants

A new constant for shortcut keys called `SHIFTMOD` has been added. It is the
or'ing of the `ShiftMask` and `MODKEY` constants.

```c
#define SHIFTMOD (ShiftMask|MODKEY)
```

### Shortcuts

The shortcuts for `clipcopy` and `clippaste` have been modified as follows:
```c
{ ControlMask, XK_y, clipcopy,  {.i =  0} },
{ ControlMask, XK_p, clippaste, {.i =  0} },
```

## Patches

The following section describes applied patches and any further modifications
using those patches.

### st-scrollback

These are the patches applied for scrollback support:
- st-scrollback-20210507-4536f46.diff
- st-scrollback-mouse-20220127-2c5edf2.diff

The following block of code was added to the shortcuts array (`shortcuts[]`) to
allow the use of the scrollback feature.

```c
{ MODKEY,   XK_Up,   kscrollup,   {.i =  1} },
{ MODKEY,   XK_Down, kscrolldown, {.i =  1} },
{ MODKEY,   XK_j,    kscrollup,   {.i =  1} },
{ MODKEY,   XK_k,    kscrolldown, {.i =  1} },
{ SHIFTMOD, XK_J,    kscrollup,   {.i = 40} },
{ SHIFTMOD, XK_K,    kscrolldown, {.i = 40} },
```

`MODKEY` and the up and down arrows can be used to move the scrollback up or
down. To provide a vim-ish experience, `MODKEY` and lowercase `j` move the
scrollback up. `MODKEY` and lowercase `k` move the scrollback down. `SHIFTMOD`
variants for `j` and `k` are added to allow the scrollback to move 40 rows at
a time. Please note that the keys for the `SHIFTMOD` variants are capitol.

The following block of code was added by the patch to allow the mouse to
perform scrollback.

```c
{ ShiftMask, Button4, kscrollup,   {.i = 1} },
{ ShiftMask, Button5, kscrolldown, {.i = 1} },
```
