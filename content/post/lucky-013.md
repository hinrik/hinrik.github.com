+++
title = "Lucky 0.13"
date = "2009-07-16T06:42:00Z"
lastmod = "2009-07-22T18:01:00Z"
tags = ["gsoc", "perl", "perl6"]
+++

I just uploaded `grok` 0.13 to PAUSE. It has the things I mentioned in my last
post, plus some bug fixes.

`grok` can look up quite a few things now (527 including documents such as
Synopses), but many of the answers it provides lack thoroughness. According to
my project schedule, it's time to start writing new documentation. That means
I can focus on making these answers better.
<!--more-->

I should also write/update a tutorial pretty soon, though I'm not exactly sure
where I'll start. I could update the
[`perlintro`](http://svn.pugscode.org/pugs/docs/Perl6/Tutorial/perlintro.pod6)
in the Pugs repository and add it to Perl6::Doc, or I could use the [Perl 6
part](http://svn.pugscode.org/pugs/docs/tutorial/) of the book _Perl 6 and
Parrot Essentials_ which was donated to the Perl Foundation by O'Reilly. That
one is a bit longer, so I might just use it for a more detailed introduction
(something like Perl 5's `perlsyn`).

P.S. Since I've got the Pod 5 ANSI-color renderer mostly working now, users of
Perl 5's `perldoc` who like colors might want to install Pod::Text::Ansi
and put the following in their `~/.bashrc` (or equivalent):

{{< highlight sh >}}
export PERLDOC="-MPod::Text::Ansi"
{{< /highlight >}}
