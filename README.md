# colemak-se
_The Colemak keyboard layout adapted for the Swedish language._

## Layout
![illustration of colemak-se layout](./assets/illustrations/layout.png)

The Colemak layout was originally created by Shai Coleman in 2006 as an ergonomic and modern keyboard layout, bringing together the comfort of Dvorak while retaining a lot of QWERTY familiarity. It employs a home row centric design placing frequently used keys under the strongest fingers. While the original layout is optimised for the English language, its Germanic roots also make it suitable for use when writing Swedish.

#### Project Scope
* Colemak-SE aims to bring a Swedish language adaption of Colemak to all modern operating systems. 
* The base layout targets 102-key keyboards, as these are the far most widely used in Sweden. 
* Colemak-SE makes as few key changes as possible in order to ease the often brutal learning process.

#### ÅÄÖ-placement
Colemak-SE does not provide full `ÅÄÖ` parity with QWERTY. `Ö` has been moved up a row to where `P` is on QWERTY, to make room for the default Colemak placement of `O`.

#### `⇪ Caps Lock` replacements
The original Colemak layout remaps `⇪ Caps Lock` to `← Backspace`. I personaly find this choice rather contentious and largely unhelpful when compared to more common replacements like `esc` and `ctrl`. As such, `⇪ Caps Lock` is left unchanged in order to make it easier for the end user to change it to their preference. macOS supports this by default (System preferences → Keyboard → Modifiers Keys...), with more advanced replacements made possible through the excellent [Karabiner](https://karabiner-elements.pqrs.org/). Windows requires [Microsoft PowerToys](https://docs.microsoft.com/en-us/windows/powertoys/) and Linux users will probably want to look into xkb.

## Installation

### Linux
The Linux implementation of Colemak-SE aims to mirror the [English Colemak website](https://colemak.com/Unix). There are a few diffient ways to do it, all with thier neuances.

##### xmodmap
`xmodmap` is a utility for modifying keymaps in `Xorg`. It modifies the layout temporarily and does not require root access.

1. Download the `xmodmap release`.
2. Open a terminal window and navigate to the file.
3. Run the shell command:
```bash
$ setxkbmap se && xmodmap xmodmap.colemak-se && xset -r 66
```

If you want to restore QWERTY, run the following:
```bash
$ setxkbmap se && xset -r 66
```

#### xkb
xmodmap is best used as a to temporary test the layout, as changes applied to it don't last over sessions. A more permanent way is to use Xorgs xkb.

1. Download the `xkb release`.
2. Open a terminal window and navigate to the file.
3. Copy the file to the place where xkb saves keymaps (might be diffirent depending on you version):
```bash
$ sudo cp colemak-se /usr/share/X11/xkb/symbols
```
4. Make sure everthing works:
```bash
$ setxkbmap -v colemak-se && xset r 66
```
If something is acting up, you can switch back to qwerty with: `setxkbmap se; xset -r 66`
5. To make the changes permanent, you need to add them to your xorg.conf.  Again, this might be different depending on your installation. Many modern distributions use the convention of a `/usr/share/X11/xorg.conf.d`, separating the diffirent parts of the config. I like to keep my layout configuration in the file `00-keyboard.conf`.
```conf
Section "InputClass"
        Identifier "system-keyboard"
        MatchIsKeyboard "on"
        Option "XkbLayout" "colemak-se"
        Option "XkbRules" "xorg"
        Option "XkbSymbols" "pc+colemak-se+inet(evdev)"
        Option "XkbModel" "pc104"
        Option "CoreKeyboard"
EndSection
```
You might need to do some configuration on your own, depending on what type of keyboard you are using.

### macOS
To install the layout, simply put the `colemak-se.bundle` in the folder `/Library/Keyboard Layouts`. This will install the layout on a system level, which is usually what you want. If you prefer to have the layout on a user level, place it in the user library instead `~/Library/Keyboard Layouts`.

To install via the terminal:
```bash
$ curl https://github.com/motform/colemak-se/releases/download/1.0/colemak-se.bundle.zip -o colemak-se.bundle.zip
$ unzip colemak-se.bundle.zip && rm colemak-se.bundle.zip
$ mv colemak-se.bundle /Library/Keyboard\ Layouts
```

If you feel uncomfortable using the terminal, a [`.dmg`](https://github.com/motform/colemak-se/releases/download/1.0/colemak-se.dmg) disk image is provided for easy GUI based installation. Just mount the disk image and follow the instructions on screen. 

A system restart is required for the layout to show up in the 'Input Sources' panel, which is accessable though: `System Preferences/Keyboard/Input Sources`. To add a new layout, press the `+`. This takes you to a list of input sources, if your installation went well, Colemak-SE should show up as a layoutoption in the `Swedish` submenu add the layout, and start using Colemak-SE!

### Windows
Download the [compressed folder](https://github.com/motform/colemak-se/releases/download/1.0/windows-colemak-se.zip) and run setup.exe.

## Learning Colemak
For resources on how to learn Colemak, see the [official Colemak website](https://colemak.com/Learn#Tips_for_learning). 

In the [extras](./extras/reference-sheet-A4_colemak-se.pdf) folder, you can find print out pdf:s for easy reference.

## Issues
* The macOS implementation only has `.incs` for 'dark mode'. I have made icons for light mode for personal use, but I can't find any documentation on how to make a dynamic `.incs`, givme me an @ if you know how!

## Attributions
* macOS keyboard layout created using [Ukelele.](https://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=Ukelele) 
* Original Colemak-SE developed in collaboration with [Jakobaa](https://github.com/jakobaa).
* All illustrations are set in [Input](http://input.fontbureau.com) by [DJR](https://djr.com). Free for private use and amazing for code!

## Licence
Original Colemak layout license is provided as is. For more information, se the [Colemak Website](https://colemak.com/License). All the files in this repo are licensed under GPL-3.0, see [LICENSE.](./LICENSE)
