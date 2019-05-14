# Confuse Build of `st` 

The [suckless terminal (st)](https://st.suckless.org/) with some additional features added by 
[Luke Smith](mailto:luke@lukesmith.xyz) 
and
[con-f-use](mailto:con-f-use@gmx.net)
that make it literally the best terminal emulator ever.

### My pet peeves with st

Generally I like st and minimalist software and suckless in particular 
(even donated to them and the registered association is right next to 
where some my relatives live). 
However, I still have some pet peeves with st: 

- It wraps lines with actual an actual newline character, not a virtual one. 
The means when you copy output, you copy superfluous newlines. 
  It also means: 
- Your old output doesn't resize as you resize the window. 
- There is now good way to copy a part of the output that is larger than the window, 
  since you can't scroll AND select at the same time (again afaik). 
- Middle click copying is slightly broken 
- I know the FAQ about 
  ("Why doesn't the Del key work in some programs?")[(ttp://git.suckless.org/st/file/FAQ.html] 
  but even if you apply their fixes, 
  the del key breaks all the time during some time into a shell session. 
- If you want tabs, you can use `tabbed`, 
  sure, but that means your terminal now shows up as `tabbed` 
  instead of `st` to various other programs. 
  I know suckless rationlizes tabbed by saying, it's wasteful to re-
  implement tabs for every application separately and that they don't
  want to clutter the binary with them, especially as some users do not
  need tabs. But isn't that what they made shared libraries for?
- The fact that you have to re-compile and reinstall in order to change 
  settings is just dumb. 
  I know it's just one command that you can automise, it's just 
  inefficient. 
- The scrollback value is not in the config file but rather some 
  preprocessor define hidden in a c file (very minor thing but annoyed 
  perfectionist me).
  

## Features

+ **follow urls** by pressing <kbd>Alt</kbd> + <kbd>L</kbd>
+ **copy urls** in the same way with <kbd>Alt</kbd> + <kbd>Y</kbd>
+ **copy the output of commands** with <kbd>Alt</kbd> + <kbd>O</kbd>
* **a desktop file**
* **automatic tabbed detection** to start st in tabbed or non-tabbed mode with the `stt` (suckless-terminal-tabs) executable
+ Compatibility with `Xresources` and `pywal` for dynamic colors. 
  The `Xdefaults` file shows a usage example.
+ Default [gruvbox](https://github.com/morhetz/gruvbox) colors otherwise.
+ Transparency/alpha, which is also adjustable from your `Xresources`.
+ Default font is system "mono" at 16pt, meaning the font will match your system font.
+ Vertcenter
+ Scrollback
+ updated to latest version 0.8.2

## Key Bindings

+ **scrollback** with<kbd>Alt</kbd> + <kbd>↑/↓</kbd> or <kbd>Alt</kbd> + <kbd>pageup/down</kbd> or <kbd>Shift</kbd> while scrolling the mouse
+ OR **vim-bindings**: scroll up/down in history with<kbd>Alt</kbd>+<kbd>K</kbd> and<kbd>Alt</kbd>+<kbd>J</kbd>. Faster with<kbd>Alt</kbd>-<kbd>U</kbd>/<kbd>Alt</kbd>+<kbd>D</kbd>.
+ **zoom/change font size**: same bindings as above, but holding down shift as well.<kbd>Alt</kbd>+<kbd>Home</kbd> returns to default
+ **copy text** with<kbd>Alt</kbd> + <kbd>C</kbd>, **paste** is <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>V</kbd> or <kbd>Shift</kbd>+<kbd>Insert</kbd>

## Installation

```
git clone https://github.com/con-f-use/sl-simpleterminal && cd st && sudo make install
```

Requires:

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

