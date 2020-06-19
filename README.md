# base16-gtk-flatcolor
This is a [Base16](https://github.com/chriskempson/base16) template for [FlatColor](https://github.com/jasperro/FlatColor), a gtk3 theme by jasperro and deviantfero,

## Usage
First download FlatColor theme from jasperro's repo to your .themes folder:
`git clone https://github.com/jasperro/FlatColor ~/.themes`

Before anything, you need to make a few changes in FlatColor so the base16 builder of your choice can inject to it. 

Navigate to `~/.themes/FlatColor/gtk-2.0` and open `gtkrc` with your favorite text editor.

Delete `gtk-color-scheme` and everything inside quotes following it (so keep gtk-auto-mnemonics), and replace with:
```
# %%base16_template: gtk-flatcolor##gtk-2 %%
# %%base16_template_end%%
```

Now move on to `.~/.themes/FlatColor/gtk-3.0`, and open `gtk.css`.

Delete all in lines in section `/* Default color scheme */`, and replace with:
```
/* %%base16_template: gtk-flatcolor##gtk-3 %%
/* %%base16_template_end%%
*/
```
(The comments look weird, blame CSS, but they will work nicely after injection)

Do the same as above, but with `.~/.themes/FlatColor/gtk-3.20`'s `gtk.css`.

Now using your injector (if you don't have one, check out [InspectorMustache's](https://github.com/InspectorMustache/base16-builder-python), it includes steps on how to use it as well), inject to those 3 files (using the correct subtemplate) you edited (plus any other you use with Base16's templates) and voila! Now your gtk theme matches your chosen Base16 scheme.

*Tip*: Most gtk apps only update when restarted, but you can use `gsettings` or `xsettingsd` to change to some theme, and back to FlatColor so all applications re-theme without restart (Thanks jasperro for the [workaround](https://github.com/deviantfero/wpgtk/issues/112))

First of all, create a dummy theme as a symlink to FlatColor (so your theme doesn't flash when changing):
```
ln -Ts ~/.themes/FlatColor ~/.themes/dummy
```

Here's two ways to do it:
#### [Xsettingsd](https://github.com/derat/xsettingsd)
After [installing](https://github.com/derat/xsettingsd/wiki/Installation) it, edit your `~/.xsettings` so it has the theme set:
```
Net/ThemeName "dummy"
```
Now just running `xsettings` should reload the theme! You can background the process, or make a systemd service to reload it more easily (check out my dotfiles if you want an example).

#### Gsettings (requires gnome packages)
Use this command to reload:
```
gsettings set org.gnome.desktop.interface gtk-theme dummy && gsettings set org.gnome.desktop.interface gtk-theme FlatColor
```

If nothing happens, make sure `/usr/lib/gsd-xsettings` is running. You do need some gnome packages installed, though.
