+++
title = "Theming the Linux console"
date = "2008-04-29T05:03:00Z"
lastmod = "2008-05-22T01:22:00Z"
tags = ["linux", "perl"]
+++

While messing with my Linux console recently, I stumbled upon the
[console\_codes(4)](http://kerneltrap.org/man/linux/man4/console_codes.4) man
page. Apparently there are Linux-specific escape codes to redefine the color
palette. Awesome! I've always preferred the
["Tango" terminal palette](http://uwstopia.nl/blog/2006/07/tango-terminal)
that recently became the default in `gnome-terminal`. Now I can use it
outside of X.
<!--more-->

Everybody likes screenshots: [before](/console-before.png) and
[after](/console-after.png).

**Update:** Apparently [PuTTY](http://en.wikipedia.org/wiki/PuTTY) supports
these escapes as well.

Using the escape codes to change the palette is quite laborious, so I decided
to write a small program to make it easier to switch between various palettes.
You can find it [here](http://search.cpan.org/dist/App-ConPalette).

There is one problem though. The Linux console doesn't allow you to set the
default foreground/backround colors independently of the color palette, as you
can do in most GUI terminal emulators. In the absence of any ANSI color
espaces, Linux uses the first and last colors of the palette for the
background and foreground (text), respectively. This means that if I were to
reuse the Tango palette verbatim in the Linux console, the background would be
dark grey and the text would be almost white. This makes man pages harder to
read, and I prefer a black background with medium gray text anyway, as is the
default in the Linux console. To solve this, I created a palette called
"tango-dark" with the first color black and the last color medium grey, and
called the unmodified palette "tango-light".

In addition to the `gnome-terminal` palettes (rxvt, tango, xterm), I also
added KDE Konsole's palette, as well as the color palette used by the
[Sinclair Spectrum](http://en.wikipedia.org/wiki/List_of_8-bit_computer_hardware_palettes#ZX_Spectrum),
since it mostly fits the ANSI palette (it has black listed twice, so I
replaced one with a dark grey color, which it was missing).

So, assuming Perl is installed, the program can be installed on most
distributions in the following manner:

    $ cpan -i App::ConPalette

Then do:

    $ conpalette --help

