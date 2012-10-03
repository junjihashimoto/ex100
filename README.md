ex100
=====

patch of ex100 wireless keyboard for linux

Install:
 type following commands.
 >cp -r etc lib /

How to customize keybinding.
 check "https://wiki.archlinux.org/index.php/Map_scancodes_to_keycodes"
 
 Following comments are snippet of the url.

 
 Using udev

First, you need to create a keymap file that udev will recognise. Some examples can be found in /lib/udev/keymaps/, and you should use one of these if it works for your keyboard model. Otherwise, you need to create one yourself. The format of each line in a keymap is '<scancode> <keycode>'. You can work out <scancode> (looks like 0xXX) using

# /lib/udev/keymap -i input/eventX

and pressing the relevant keys. Replace input/eventX with your keyboard device, which can be found by running

$ /lib/udev/findkeyboards

The choices for <keycode> are listed as KEY_<KEYCODE> in /usr/include/linux/input.h, but you need to change these to lower case and remove the KEY_ prefix (for example, KEY_PROG3 corresponds to prog3). A sorted list is available here.

Once you have a keymap, you need to tell udev to use it. This can be done with a udev rule. Here is a simple example:

SUBSYSTEM=="input", ATTRS{name}=="AT Translated Set 2 keyboard", RUN+="/lib/udev/keymap input/$name /path/to/keymap"

If you place the keymap file in /lib/udev/keymaps, you can omit the full path. Now the keymap will be active the next time you restart. You can run the following command to activate it immediately:

# /lib/udev/keymap input/eventX /path/to/keymap

