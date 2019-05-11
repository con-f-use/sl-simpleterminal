# Confuse Build of `st` 

The [suckless terminal (st)](https://st.suckless.org/) with some additional features added by [Luke Smith](mailto:luke@lukesmith.xyz) and a `.desktop`-file that make it literally the best terminal emulator ever.

## Unique features (using dmenu)

+ **follow urls** by pressing <kbd>Alt</kbd> + <kbd>L</kbd>
+ **copy urls** in the same way with <kbd>Alt</kbd> + <kbd>Y</kbd>
+ **copy the output of commands** with <kbd>Alt</kbd> + <kbd>O</kbd>
+ **a desktop file**

## Key Bindings

+ **scrollback** with<kbd>Alt</kbd> + <kbd>↑/↓</kbd> or <kbd>Alt</kbd> + <kbd>pageup/down</kbd> or <kbd>Shift</kbd> while scrolling the mouse
+ OR **vim-bindings**: scroll up/down in history with<kbd>Alt</kbd>+<kbd>K</kbd> and<kbd>Alt</kbd>+<kbd>J</kbd>. Faster with<kbd>Alt</kbd>-<kbd>U</kbd>/<kbd>Alt</kbd>+<kbd>D</kbd>.
+ **zoom/change font size**: same bindings as above, but holding down shift as well.<kbd>Alt</kbd>+<kbd>Home</kbd> returns to default
+ **copy text** with<kbd>Alt</kbd> + <kbd>C</kbd>, **paste** is <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>V</kbd> or <kbd>Shift</kbd>+<kbd>Insert</kbd>

## Pretty stuff

+ Compatibility with `Xresources` and `pywal` for dynamic colors. The `Xdefaults` file shows a usage example.
+ Default [gruvbox](https://github.com/morhetz/gruvbox) colors otherwise.
+ Transparency/alpha, which is also adjustable from your `Xresources`.
+ Default font is system "mono" at 16pt, meaning the font will match your system font.

## Other st patches

+ Vertcenter
+ Scrollback
+ updated to latest version 0.8.2

## Installation

```
git clone https://github.com/con-f-use/simpleterminal && cd st && sudo make install
```

### Requirements

* `make` 
* `fontconfig` is used for getting your system monospace font
*  `libX11` and `libXft` 

Be sure to have a composite manager (`xcompmgr`, `compton`, etc.) running if you want transparency.

On OpenBSD, be sure to edit `config.mk` first and remove `-lrt` from the `$LIBS` before compiling.

## How to configure dynamically with Xresources

For many key variables, this build of `st` will look for X settings set in either `~/.Xdefaults` or `~/.Xresources`. You must run `xrdb` on one of these files to load the settings.

For example, you can define your desired fonts, transparency or colors:

```
*.font:	Liberation Mono:pixelsize=12:antialias=true:autohint=true;
*.alpha: 0.9
*.color0: #111
...
```

The `alpha` value (for transparency) goes from `0` (transparent) to `1` (opaque).

### Colors

To be clear about the color settings:

- This build will use gruvbox colors by default and as a fallback.
- If there are Xresources colors defined, those will take priority.
- But if `wal` has run in your session, its colors will take priority.

Note that when you run `wal`, it will negate the transparency of existing windows, but new windows will continue with the previously defined transparency.
