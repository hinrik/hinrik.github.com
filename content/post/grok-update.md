+++
title = "grok update"
date = "2009-06-26T05:54:00Z"
lastmod = "2009-07-01T19:28:00Z"
tags = ["gsoc", "perl", "perl6"]
+++

Some things have kept me very busy lately and I'm a bit behind on my GSoC
schedule. I'm starting to catch up now, though.
<!--more-->

First of all, as of version 0.05, you can now easily install `grok` from the
command line on most operating systems like so:

    $ cpanp -i App::Grok

It can handle Pod 5 files now (via Pod::Text) as well (which most of the
Perl 6 Synopses are written in). The ANSI-colored output looks a bit different
than the Pod 6 output because Pod::Text is very conservative in its use of
colors. I'll probably make them more similar later to keep it consistent.

When called interactively, `grok` now uses your system's pager to view the
output by default.

It will now treat an argument as a Pod 6 file to read if said argument doesn't
match a known documentation target. As for the targets, the only known ones so
far are the synopses (which are bundled with `grok` for now), so you can do
things like:

    $ grok s02
    $ grok s32-rules
