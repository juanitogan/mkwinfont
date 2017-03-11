# mkwinfont/dewinfont

This is an update to Simon Tatham's font utilities found here:
* http://www.chiark.greenend.org.uk/~sgtatham/fonts/

More information on his work can be found here:
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

## Other Font Tools

### Bitmap Font Tools

[**fony**](http://hukka.ncn.fi/?fony) - For most work, you'll probably want to use this editor.  It is a fairly good editor with only a few UI annoyances.  Note: it reads but doesn't write genuine FNT files -- instead, it creates a FON file with a *.fnt extention.  This, however, won't be an issue for most.  It has a few other bugs that forced me to revert to _mkwinfont_ here and there, but those are also rare.  The feature to export to grid images also appears to be broken (which is fairly disappointing to me).

[**VSoft's Fontedit**](http://www.vsoft.nl/software/utils/win/fontedit/) - This FNT-only editor still works on the latest Windows versions except for one very important feature -- a bug prevents it from saving on the latest Windows.  The source code is provided so it should be an easy fix.  This is not as nice an editor as _fony_ but it has some features _fony_ should absorb like inserting and deleting of columns and rows, and selection editing.

[**PSF Tools**](http://www.seasip.info/Unix/PSF/) - UNIX programs that are useful for converting many bitmap types -- particularly, Linux's PSF console type (but not the PCF X11 type?).  It installed fine in [Babun](http://babun.github.io/)/Cygwin for me.

