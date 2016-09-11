+++
title = "Grok refactor"
date = "2009-07-24T13:30:00Z"
lastmod = "2009-07-29T18:29:00Z"
tags = ["gsoc", "perl", "perl6"]
+++

As the title suggests, I reorganized the `grok` a bit, in addition to adding a
few new features.
<!--more-->

The code is now more modular, and much easier to maintain. I added support for
looking up individual functions/methods from all the chapters of Synopsis 32.
In other news, Perl6::Doc 0.42 is just out, which includes first drafts of
`perlintro` and `perlsyn` documents, which `grok` will now find.

This brings the total number of things known to `grok` up by almost a hundred:

    $ grok -i|wc -l
    613
