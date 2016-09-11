+++
title = "On to the man pages"
date = "2009-07-22T18:31:00Z"
tags = ["gsoc", "perl", "perl6"]
+++

This week I've been working on the `perlintro` document found in the pugs
repository, as well as porting Perl 5's `perlsyn`. These are the most "basic"
man pages about the language, and should be ported first (especially since
many of the more specific bits in Perl 6 are still in flux).
<!--more-->

As for `perlintro`, I can see a few more-than-trivial things that need
changing. For one thing, the introduction to regular expressions is very
casual, but Perl 6's regex/grammar support has seen a major overhaul. Simply
translating the examples to the Perl 6 equivalent seems to just make them
longer, which gives the wrong impression. Focusing less on quick-and-dirty
examples and more on the big picture might help the newcomer here, as grammars
are integral to Perl 6, not just some special strings with weird syntax as
they were in ol' Perl 5.

A lot of special cases and "warts" have been replaced with new, exciting
concepts that show up again and again in Perl (laziness, autothreading, all
blocks are closures, everything is an object) that need to be touched upon.
You could say that in Perl 6, the harmony / idiosyncrasy ratio has been
lowered, and that's a very **good** thing. Some of these can be saved for
`perlsyn`, but nonetheless, they need to be introduced well.

In other news, I noticed that [perldoc.perl.org](http://perldoc.perl.org) has
seen a facelift. I wonder if the software behind it might be used to power a
Perl 6 doc site sometime in the future.

