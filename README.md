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

To make a FNT file from an FD text file:
```
python3 mkwinfont.py -fnt -o <outfile.fnt> <file.fd>
```

To make a FON file from one or more FD text files:
```
python3 mkwinfont.py -fon -o <outfile.fon> [-facename <name>] <file1.fd> [<file2.fd> ...]
```
* `-facename <name>` is required if the FD files have different facenames defined within them.  Optional otherwise.

To desconstruct a FNT or single-font FON file to FD text file:
```
python3 dewinfont.py -o <outfile.fb> <filename>
```

To desconstruct a multi-font FON file to multiple FD text files:
```
python3 dewinfont.py -p <prefix> <file.fon>
```
* Files will be named like so: `<prefix>00.fd`

## Other Font Tools

### Bitmap Font Tools

[**fony**](http://hukka.ncn.fi/?fony) - For most work, you'll probably want to use this editor.  It is a fairly good editor with only a few UI annoyances.  It has a few issues that forced me to revert to _mkwinfont_ here and there, but those are rare.  I also had some trouble with saving multi-font FON files as FNT (the FNT file coming out identical to the FON file, which is wrong) and reducing multi-font FON files to a single-font FON file (the result not readable by Windows)... but I can't reliably reproduce those problems either so, go figure, maybe it was me.  Considering that FNT files are resource files for programming and not installable in the OS (also, they cannot contain more than one font like FON files can, which this editor favors features for) it would probably make more sense to handle FNT as another type of import/export instead of a load/save.  The feature to export to grid images is broken (which is fairly disappointing to me) -- or never completed (the latest version is a "work in progress").

[**VSoft's Fontedit**](http://www.vsoft.nl/software/utils/win/fontedit/) - This FNT-only editor still works on the latest Windows versions except for one very important feature: a bug prevents it from saving on the latest Windows.  The source code is provided so it should be an easy fix.  This is not as nice an editor as _fony_ but it has some features _fony_ should absorb like inserting and deleting of columns and rows, and selection editing.

[**PSF Tools**](http://www.seasip.info/Unix/PSF/) - UNIX programs that are useful for converting many bitmap types -- particularly, Linux's PSF console type (but not the PCF X11 type?).  It installed fine in [Babun](http://babun.github.io/)/Cygwin for me.

## See Also

This project was spawned by needs of this other one for creating fonts compatible with [PICO-8](http://www.lexaloffle.com/pico-8.php) programming:

* https://github.com/juanitogan/p8-programming-fonts
