+++
title = "More docs added"
date = "2009-08-17T23:52:00Z"
lastmod = "2009-08-17T23:54:00Z"
tags = ["gsoc", "perl", "perl6"]
+++

I've added Jonathan Scott Duff's introduction to Perl 6 regexes to Perl6-Doc
as `perlreintro`. In addition I put in a first draft of a `perlobjintro`.
Neither of these correspond to names from the set of Perl 5 man pages, which
is fitting since they are not directly based on them. So, Perl6-Doc now has
4 man pages, the aforementioned two as well as `perlintro` and `perlsyn`. I'll
be carefully adding to and polishing these in the near future. I'm hesitant to
start on man pages relating to modules, IO, laziness/iterators, and other very
important features, as the specs (and implementation) for those are still
shifting heavily from month to month.
<!--more-->

I've been thinking about using the Perl Table Index as initial source material
for the magical syntax recognition feature, the implementation of which has
remained elusive for a while. The current implementation is just a proof-of-
concept with only a few terms as of yet. However, Damian Conway just published
a significant update to Synopsis 26 on Perl documentation, focused on tying
docs to code, so it might be time to figure out some Pod-ish source format for
the terms to be stored in. Writing Pod is a breeze, so it should be easy to
contribute new terms.

`grok` also needs more love. I'm not as happy as I'd like to be with some of
its implementation details, most notably how it picks out functions from
Synopses 29 and 32, using simple regexes (to be fair, this is exactly what
good ol' `perldoc -f` does). It should parse the Pod and pick out parts of the
document tree instead, I think. There are also still a few visual differences
between textual output of Pod 5 and Pod 6 that I have to address. Pod 5
textual output is pleasingly indented (gradually depending on the current
heading level), which makes it very easy to follow, while Pod 6 is not.

As a sidenote, I believe I've found what was causing intermittent FAIL reports
from CPAN testers. Some machines had a pretty old version of Pod::Simple which
didn't take well to subclassing. Another failure was caused by an old
Pod::Parser (deprecated, but relied on by Pod::Xhtml) version which didn't
recognize `=encoding` directives. The relevant distributions now depend on
newer versions of those troublesome modules.
