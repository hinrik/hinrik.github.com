+++
title = "grok 0.09 is out"
date = "2009-07-01T19:33:00Z"
lastmod = "2009-07-01T19:36:00Z"
tags = ["gsoc", "perl", "perl6"]
+++

The code is starting to take a more stable form. I've prepended an underscore
to all private/internal subroutines and documented the rest. Perl authors
wishing to use `grok`'s functionality will now have an easier time doing so.
<!--more-->

I've also added various author tests to the distribution to help keep the code
in shape (or at least remind me when it's not), notably Test::Pod,
Test::Pod::Coverage, and Test::Perl::Critic.

Since my last blog post, `grok` has gained a few features. It can print the
name of the target file (like `perldoc -l`), print an index of known
documentation files, output xhtml, and detect whether the target file has Pod
5 or Pod 6 in it. It's also got some Win32 fixes and more informative error
messages.

Pretty soon I will start bringing in some more docs to bundle with it.
Tutorials and such. I will also most likely implement function documentation
lookup (like `perldoc -f`) in grok.

