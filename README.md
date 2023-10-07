# ripright(1) - CD ripper

ripright-0.11, 2015-12-08

```
ripright  [-d] [-a] [-r] [-s] [-w] [-c device] [-o format] [outpath]
```



<a name="description"></a>

# Description

RigRight is a minimal CD ripper with few options.  It can run as a daemon and
will automatically start ripping any CD found in the drive after which the disc
will be ejected.  Ripping is always to FLAC lossless audio format with tags taken
from the MusicBrainz lookup service and cover art from Amazon where possible.
If a disc is unknown to MusicBrainz, the CD will be ejected without ripping.

In case a disc is unknown, MusicBrainz Picard can be used to send the CD ToC to
the MusicBrainz database.  The MusicBrainz website can then be used to find or
add details of a CD, after which the CD can be ripped using RipRight.


<a name="options"></a>

# Options


* **-d**, **--daemon**  
  Run in daemon mode.  Ripright will detach from the terminal and direct output
  to the syslog.
* **-a**, **--rip-to-all**  
  Normally exactly 1 result is required from Musicbrainz, otherwise the CD will
  be refused and ejected.  With this option, the CD will be ripped and tagged to
  multiple files, once as each result from Musicbrainz.  Each rip is output under
  a directory named Ambiguous/&lt;mb-release-id&gt;/ where the the Musicbrainz
  release Id is used to identify each possible release.
* **-w**, **--w32-filenames**  
  Covert characters that are illegal on Windows filesystems to UTF-8 alternatives.
  If accessing files over Samba, this prevents name mangling which can lose the
  file extension.  Mapped characters are ***, ?**, **"** and **|**
  which are replaced by **ӿ**, **ʔ**, **¨** and **ǀ** respectively.
* **-s**, **--allow-skips**  
  Normally ripping attempts to make a perfect copy of a CD by using all data
  verification and correction features of the cdparanoia library.  With this
  option, each bad sectors will be skipped after 20 failed attempts to read the
  data.  Without this option, ripping of scratched or damaged CDs may take a very
  long time and possibly may not complete.
* **-r**, **--require-art**  
  Refuse to rip a CD if the cover art cannot be retrieved.  The correct ASIN must
  be added to the MusicBrainz database for art to be fetched from Amazon.
* **-f &lt;file&gt;**, --folder-art &lt;file&gt;  
  Save cover art (if available) to &lt;file&gt;, relative to the output directory.
  The art file will be converted to the format specified by the filename e.g.
  -f folder.jpg or -f folder.gif or -f folder.png
* **-c**, **--cd-device**  
  Path to the CD-ROM device to use.  This defaults to /dev/cdrom if not otherwise
  specified.
* **-o**, **--output-file**  
  Set the format used to produce output filenames and paths.  This should be a
  string containing the following special tokens:
  
    %N = Track number (TRACKNUMBER)
    %A = Track artist (ARTIST)
    %a = Track artist sort name (ARTISTSORT)
    %B = Album artist (ALBUMARTIST)
    %b = Album artist sort name (ALBUMARTISTSORT)
    %C = Track artist if present, else album artist
    %c = Track artist sort name if present, else album artist sort name
    %D = Album/CD name (ALBUM)
    %T = Track name (TITLE)
    %Y = Release type (MUSICBRAINZ_TYPE)
    %% = A single percent sign
  
  The release type is one of Albums, Audiobooks, Compilations, EPs,
  Interviews, Live, Remixes, Singles, Soundtracks, Spokenword and Other.
  
  Slashes and colons in the '%' output fields are converted to UTF-8
  equivalents to avoid creating subdirectories or causing problems
  with Windows shares mounted via Samba.  Slashes and colons given in
  the format string will be literally preserved.
  

<a name="copyright"></a>

# Copyright

RipRight, Copyright (C) 2013-2015 Michael C McTernan,
                                  mike@mcternan.uk  
Eject routines, Copyright (c) 1994-2005 Jeff Tranter
                                        tranter@pobox.com

This program is free software; you can redistribute it and/or modify it under
the terms of the GNU General Public License as published by the Free Software
Foundation; either version 2 of the License, or (at your option) any later version.


<a name="see-also"></a>

# See Also

riparrange(1)

http://www.mcternan.co.uk/ripright/  
http://www.musicbrainz.org/
