# st - simple terminal

st is a simple terminal emulator for X which sucks less.

## Changes

The following section describes the various changes I have added to the st codebase.

### Build Changes

The config.mk file has had the `PREFIX` variable changed from `/usr/local/` to
`~/.local/`. This allows the st tool to only be installed for my user.

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

