+++
title = "Tagging, FAIL, regexes"
date = "2009-07-29T19:03:00Z"
tags = ["gsoc", "perl", "perl6"]
+++

I'm currently working on making `grok` index all `X<>` (and maybe `C<>`) tags
in Pod documents. The user will then be able to look them up and see which
docs contain the search term in question.
<!--more-->

Gábor Szabó has already done [something like this](http://perlcabal.org/syn/index_X.html)
for the Perl 6 Synopses. His implementation only looked for formatting codes
using the standard `<>` format, but I just patched it to look for `<< >>`,
`<<< >>>`, and `«»` tags as well. Ideally I would like to use a Pod parser to
get the tags, but it's just using regexes for now. Gábor also asked me to
have `grok` look up the predefined subrules from Synopsis 5, which I think
would be a good addition.

For a while, I've been getting some rare [FAIL reports](http://static.cpantesters.org/distro/G/grok.html)
about `grok` from CPAN testers. It seems to be two problems that always
manifest themselves at the same time. One of them is obviously because the
tester has an old version of Pod::Parser which doesn't understand the
`=encoding` directive, but the other one is more mysterious. I'll have to do
some more digging, as I haven't been able to reproduce it on my machines.

Jonathan Scott Duff pointed me to his unpublished
[introduction](http://feather.perl6.nl/~duff/articles/perl6/p6-regex.pod) to
Perl 6 regexes which I could use as a starting point for a `perlretut` man
page. I haven't got it into a releasable state yet, but it will soon.

