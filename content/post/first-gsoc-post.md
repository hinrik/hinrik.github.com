+++
title = "First GSoC post"
date = "2009-05-27T17:25:00Z"
lastmod = "2009-05-31T22:15:00Z"
tags = ["gsoc", "perl", "perl6"]
+++

I officially started on my Google Summer of Code project (project details
[here](http://nix.is/gsoc/)) last weekend.

I've been tasked with writing a `perldoc` equivalent for Perl 6. I've decided
to write it in Perl 5 for now, since it's already got Perl6::Perldoc, which
is a fast and feature-complete parser for the Perl 6 version of Pod (see
[specification](http://perlcabal.org/syn/S26.html)), as well as lots of other
useful CPAN modules which I won't have to rewrite in Perl 6 (yet).
<!--more-->

The program will be called `grok`
([repository](http://github.com/hinrik/grok)). So far it's just a barebones
command-line reader for Pod 6, but I did create an ANSI-colored terminal
renderer for Perl6::Perldoc. It might be too colorful for some people's
taste currently, so maybe I'll tone it down a little. I think Ruby's `ri`
documentation reader is the only such tool which colors the output, and I
thought it was a nice enough feature (one of many!) to copy. I've also been
looking at `pydoc` and `javadoc` in search of interesting features to
implement.

The plan is to make it more modern and extensive than `perldoc`. One
interesting thing I might end up doing is making use of STD (the standard
Perl 6 grammar) to parse arbitrary syntax, so you could do stuff like `grok
'[*]'` and the program would tease the expression apart and show you
documentation for both the `[]` and the `*` operators.

Some portion of the project also includes writing new documentation for Perl
6. I haven't written any yet, but I bet it will be fun. Before doing so, we
first have to figure out how to organize the the docs. Since Perl 6 is a
specification, it's not as obvious as with Perl 5, where the docs are included
(sometimes inline) with the implementation.
