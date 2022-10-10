# st - simple terminal

st is a simple terminal emulator for X which sucks less.

## Changes

The following section describes the various changes I have added to the st
codebase.

### Build Changes

The config.mk file has had the `PREFIX` variable changed from `/usr/local/` to
`~/.local/`. This allows the st tool to only be installed for my user.

### Patches

The following section describes applied patches and any further modifications
using those patches.

#### st-scrollback

These are the patches applied for scrollback support:
- st-scrollback-20210507-4536f46.diff
- st-scrollback-mouse-20220127-2c5edf2.diff

The following block of code was added to the shortcuts array to allow the use
of the scrollback feature.

```c
{ MODKEY,               XK_Up,          kscrollup,      {.i = -1} },
{ MODKEY,               XK_Down,        kscrolldown,    {.i = -1} },
{ MODKEY,               XK_j,           kscrollup,      {.i = -1} },
{ MODKEY,               XK_k,           kscrolldown,    {.i = -1} },
{ MODKEY,               XK_J,           kscrollup,      {.i = -40} },
{ MODKEY,               XK_K,           kscrolldown,    {.i = -40} },
```

`MODKEY` and the up and down arrows can be used to move the scrollback up or
down. To provide a vim-ish experience, `MODKEY` and lowercase `j` move the
scrollback up. `MODKEY` and lowercase `k` move the scrollback down. Captial `J`
and `K` move the scrollback 40 rows in their respective direction.

## Requirements

In order to build st you need the Xlib header files.

## Installation

Edit config.mk to match your local setup (st is installed into
the /usr/local namespace by default).

Afterwards enter the following command to build and install st (if
necessary as root):

    make clean install

## Running st

If you did not install st with make clean install, you must compile
the st terminfo entry with the following command:

    tic -sx st.info

See the man page for additional details.

## Credits

Based on Aurélien APTEL <aurelien dot aptel at gmail dot com> bt source code.

