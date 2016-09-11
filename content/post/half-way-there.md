+++
title = "Half way there"
date = "2009-07-11T01:54:00Z"
lastmod = "2009-07-11T01:56:00Z"
tags = ["gsoc", "perl", "perl6"]
+++

With Summer of Code's mid-term evaluations coming up, some interesting things
are about to happen to `grok`. I was contacted by Herbert Breunung, author of
[Perl6::Doc](http://search.cpan.org/dist/Perl6-Doc/) (formerly
Perl6::Bible), which is a project that shares some of `grok`'s goals.
<!--more-->

He told me that he doesn't have enough time to maintain his project anymore
and would like some sort of merge to happen. I said I'd look into it. His
project bundles all the Synopses, Apocalypses, Exegeses, and some other Perl 6
documentation, and ships with a `perldoc` wrapper for reading them. What I
would like to do is to move all documentation out of the `grok` distribution
and update/add more to Perl6::Doc while eliminating the `perldoc` wrapper
(in favor of `grok`).

He also brought to my attention the [Perl Table Index](http://www.perlfoundation.org/perl6/index.cgi?perl_table_index),
a sort of Perl 6 glossary. Ahmad Zawawi has [just patched](http://padre.perlide.org/trac/changeset/5994)
his [Padre::Plugin::Perl6](http://search.cpan.org/dist/Padre-Plugin-Perl6/) to
feed this index to `grok`. I will probably port the Perl Table Index to the
Perl6::Doc distribution and make `grok` look things up in it.

I've started writing a Pod::Text subclass as well as amending
Perl6::Perldoc::To::Ansi to conform to a consistent color scheme when using
the default ANSI-colored output.

Something which `grok` should eventually be able to do is recognize arbitrary
Perl 6 syntax (at very fine level of granularity, that is) and tell you what
it means. A first stab at this will be to simply include a table of some
common ones and look those up. Stuff like `my`, `+`, and so on. Doing this
reliably is the original inspiration for the u4x project (Userdocs for
Christmas), of which `grok` is a part.

I hope to make a release of `grok` and Perl6::Doc shortly which will include
all of the above.

