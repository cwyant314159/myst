# st - simple terminal

`st` is a simple terminal emulator for X which sucks less.

## Changes

The following section describes the various changes I have added to the st
codebase. The suckless documentation, FAQ, legacy notice, and license for `st`
can be found in the `suckless` directory.

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

The following block of code was added to the shortcuts array (`shortcuts[]`) to
allow the use of the scrollback feature.

```c
{ MODKEY, XK_Up,   kscrollup,   {.i = -1} },
{ MODKEY, XK_Down, kscrolldown, {.i = -1} },
{ MODKEY, XK_j,    kscrollup,   {.i = -1} },
{ MODKEY, XK_k,    kscrolldown, {.i = -1} },
```

`MODKEY` and the up and down arrows can be used to move the scrollback up or
down. To provide a vim-ish experience, `MODKEY` and lowercase `j` move the
scrollback up. `MODKEY` and lowercase `k` move the scrollback down.

The following block of code was added by the patch to allow the mouse to
perform scrollback.

```c
{ ShiftMask, Button4, kscrollup,   {.i = 1} },
{ ShiftMask, Button5, kscrolldown, {.i = 1} },
```
