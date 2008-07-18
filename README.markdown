sep-offprint
============

`sep-offprint` is a perl script that makes offprints from 
[Stanford Encyclopedia of Philosophy] articles.

[Stanford Encyclopedia of Philosophy]: http://plato.stanford.edu

© 2006-7 John MacFarlane. This script may be freely used and modified.
There are no guarantees or warranties of any kind. If you find a way to
improve it, I would appreciate hearing about it.

Installing sep-offprint
-----------------------

You can download `sep-offprint` [here](http://github.com/jgm/sep-offprint/tarball/master)
or clone the git repository:

    git://github.com/jgm/sep-offprint.git

To use the `sep-offprint` script, you will need Perl and two (free) external
programs:

-   [Ghostscript](http://www.cs.wisc.edu/~ghost/doc/AFPL/get851.htm)
-   [html2ps](http://user.it.uu.se/~jan/html2ps.html) (Download the
    tarball or zip file, extract, and run the `install` script.)

If you are running linux or unix (including Mac OS X), you may
already have Ghostscript. You can check by issuing the command:

    which ps2pdf

If it returns a pathname, then you probably have Ghostscript.

You'll also need the Perl modules in LWP (Library for WWW in Perl).
Your perl installation may already contain LWP; if not, you can
install it using cpan:

    cpan -i LWP

(Accept all the defaults.)

On a \*nix system, you will want to put `sep-offprint` in your path
(e.g. in your `~/bin` directory) and make it executable:

    chmod +x sep-offprint

You can then run it from any directory by typing:

    sep-offprint plato

If this doesn't work, you may have to modify the first line of the
script, which tells it where to find perl. Replace `/usr/bin/perl`
in the first line of the script with the path to perl on your
system. To find this path, type:

    which perl

On Windows systems, follow [these instructions], or just type

    perl sep-offprint plato

to run the script.  (Note that if you use the method of associated file-types,
you will have to rename `sep-offprint` as `sep-offprint.pl`, so Windows will
know that it's a perl script.)

[these instructions]: http://aspn.activestate.com/ASPN/docs/ActivePerl/5.8/faq/Windows/ActivePerl-Winfaq4.html#What_s_the_equivalent_of_the_she

Using sep-offprint
------------------

To make a PDF offprint from the "Frege" article, just type:

    sep-offprint frege

If all goes well, the file `frege.pdf` will be created in your
working directory (so make sure you don't already have a file by
that name, or it will be overwritten).  If you have not put
`sep-offprint` in your path as described above, you will have
to put the `sep-offprint` script in your working directory and type

    perl sep-offprint frege

instead of the command above.

To find the official name of an entry, look at the URL. For
example, the URL for my article on
[logical constants](http://plato.stanford.edu/entries/logical-constants)
is `http://plato.stanford.edu/entries/logical-constants`. The part
after `entries/` is the official name. So, to generate an offprint,
we'd type:

    sep-offprint logical-constants

Or, if you want, use the whole URL:

    sep-offprint http://plato.stanford.edu/entries/logical-constants

If you want to create an offprint from an entry on your local computer
(say, one that you are editing), use a `file://` URL. For example, if
your entry lives in the directory `/home/mmm/entries/truth`, you can use

    sep-offprint file:///home/mmm/entries/truth

to create an offprint from it. (The old `--localpath` option has been
removed, as this is now the preferred way to create offprints from
local entries.)

By default, `sep-offprint` creates PDF offprints with two pages per
side, in landscape mode, using letter size paper and a 14 point
Times font. All of these defaults can be changed using command-line
options. Thus, to create a postscript file instead of a PDF, with
just one page per sheet and A4 paper, type:

    sep-offprint --1up --ps --paper a4 frege

This command will produce a file called `frege.ps` in the working
directory.

To create a PDF with larger print and a sans-serif font, type:

    sep-offprint --size 16pt --font Helvetica frege

Here is a full list of options, with defaults indicated by `*`:

    --1up                  print one page per sheet, portrait orientation
    --2up                  print two pages per sheet, landscape orientation*
    --ps                   produce postscript (PS) output
    --pdf                  produce PDF output*
    --output FILENAME      name of output file (defaults to ENTRYNAME.ps|pdf)
    --font FONT            specify font (Times*, Helvetica, Palatino, Courier)
    --size SIZE            specify font size (10pt, 12pt, 14pt*, 16pt)
    --align ALIGN          specify alignment (left, justified*)
    --paper PAPERSIZE      specify paper size (letter*, legal, a4)
    --linkcolor COLOR      specify color of hyperlinks (black*, gray, blue, ...)
    --help                 this message
    --version              prints version number

Limitations
-----------

Due to limitations in `html2ps`, `sep-offprint` may stumble
on some Unicode characters that render properly in HTML.
The following characters found in some SEP articles 
are not yet properly supported by sep-offprint:

(257) &#257;,
(261) &#261;,
(263) &#263;,
(269) &#269;,
(281) &#281;,
(299) &#299;,
(321) &#321;,
(322) &#322;,
(324) &#324;,
(333) &#333;,
(345) &#345;,
(346) &#346;,
(347) &#347;,
(351) &#351;,
(363) &#363;,
(365) &#365;,
(369) &#369;,
(378) &#378;,
(380) &#380;,
(381) &#381;,
(594) &#594;,
(596) &#596;,
(601) &#601;,
(618) &#618;,
(660) &#660;,
(768) &#768;,
(769) &#769;,
(770) &#770;,
(771) &#771;,
(772) &#772;,
(773) &#773;,
(775) &#775;,
(803) &#803;,
(903) &#903;,
(1087) &#1087;,
(8004) &#8004;,

History
-------

+   2007-08-16 (v1.11)

    Use File::Spec and File::Basename for platform-independent
    manipulation of files and directories.

+   2007-08-16 (v1.1)

    Added --output|o option to specify output filename

+   2007-07-19 (v1.0)

    - Include supplements in the ordered they are linked to.
    - Always put notes at the end.
    - Removed `--localpath` option; use `file:/// URL` instead.

+   2007-03-08 (v0.9)

    Fixed regex for stripping off SEP header (thanks to George Galfalvi).

+   2007-02-22 (v0.8)

    Strip off "(Stanford Encyclopedia of Philosophy)" from
    HTML title (thanks to Uri Nodelman).

+   2007-01-23 (v0.7)

    - Include supplements, if present (thanks to Dan Robins).
    - Removed unnecessary call to lwp-rget (Dan Robins).
    - Added `--linkcolor` option (JM and Dan Robins).
    - Added error checking:  error exit if index.html not found.
    - Fixed `--version` and adjusted `--help` output.

+   2005-05-25 (v0.3)

