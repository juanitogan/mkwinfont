# mkwinfont/dewinfont

This is an update to Simon Tatham's font utilities found here:
* http://www.chiark.greenend.org.uk/~sgtatham/fonts/

Some additional information on his work can be found here:
* http://michelbytes.blogspot.com/2012/08/how-to-make-fon-bitmap-font-files.html

In brief, `mkwinfont` and `dewinfont` are Python scripts for working with Windows bitmap font file types: FNT and FON.  These scripts read from and write to text files (*.fd) where the character bitmaps are defined with text characters such a `.` and `x`, or `0` and `1` (or any combination of those).

For example, the letter "A":
```
char 65
width 9
.........
.........
.........
...xx....
...xx....
..xxxx...
..x..x...
.xx..xx..
.xx.xxx..
.xxxx.x..
xxx...xx.
xx....xx.
xx....xx.
.........
.........
.........
```

### Syntax

To make a FNT file from an FD source file:
```
python3 mkwinfont.py -fnt -o <outfile.fnt> <file.fd>
```

To make a FON file from one or more FD source files:
```
python3 mkwinfont.py -fon -o <outfile.fon> [-facename <name>] <file1.fd> [<file2.fd> ...]
```
* `-facename <name>` is required if the FD files have different facenames defined within them.  Optional otherwise.

To deconstruct either a FNT file or a single-font FON file to an FD source file:
```
python3 dewinfont.py -o <outfile.fb> <filename>
```

To deconstruct a multi-font FON file to multiple FD source files:
```
python3 dewinfont.py -p <prefix> <file.fon>
```
* Files will be named like so: `<prefix>00.fd`

## Other font tools

### Bitmap font tools

[**fony**](http://hukka.ncn.fi/?fony) - For most work, you'll probably want to use this editor.  It is a fairly good editor with only a few UI annoyances.  It has a few issues that forced me to revert to _mkwinfont_ here and there, but those are rare.  I also had some trouble with saving multi-font FON files as FNT (the FNT file coming out identical to the FON file, which is wrong) and reducing multi-font FON files to a single-font FON file (the result not readable by Windows)... but I can't reliably reproduce those problems either so, go figure, maybe it was me.  Considering that FNT files are resource files for programming and not installable in the OS, and that FNT files cannot contain more than one font like FON files can (which this editor favors features for), it would probably make more sense to handle FNT as another type of import/export instead of a load/save.  The feature to export to grid images is broken (which is fairly disappointing to me)... or was never completed (the latest version I found being a "work in progress").  That's what [ImageMagick](https://imagemagick.org/)'s montage tool is for, I suppose.  Hint:

```shell script
montage \
 t_?.png \
 t_??.png \
 t_???.png \
 -tile 32x -geometry "9x16<+0+0" -background white \
 - \
 | magick - -bordercolor white -border 4x2 \
 t_montage.png
```

[**VSoft's Fontedit**](http://www.vsoft.nl/software/utils/win/fontedit/) - This FNT-only editor still works on the latest Windows versions except for one very important feature: a bug prevents it from saving on the latest Windows.  The source code is provided so it should be an easy fix.  This is not as nice an editor as _fony_ but it has some features _fony_ should absorb, like: inserting and deleting of columns and rows, and selection editing.

[**PSF Tools**](http://www.seasip.info/Unix/PSF/) - A collection of UNIX tools for converting many bitmap font types -- particularly, Linux's PSF console type (but not the PCF X11 type?).  It installed fine in [Babun](http://babun.github.io/)/Cygwin for me.

### Vector font tools

See [my guide](https://namethattech.wordpress.com/2017/03/22/how-to-make-a-snap-to-grid-in-fontforge/) for creating pixelated TrueType fonts in [FontForge](https://fontforge.github.io/).

## See also

This project was spawned by needs of this other one for creating fonts compatible with [PICO-8](http://www.lexaloffle.com/pico-8.php) programming:

* https://github.com/juanitogan/p8-programming-fonts
