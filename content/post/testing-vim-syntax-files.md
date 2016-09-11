+++
title = "Testing vim syntax files"
date = "2009-09-01T13:13:00Z"
lastmod = "2009-09-01T13:15:00Z"
tags = ["perl", "perl6", "vim"]
+++

Yesterday, Andy Lester opened an [issue](http://github.com/petdance/vim-perl/issues#issue/15)
for vim-perl on github about adding an automated test suite. I've thought
about doing something like this before, so last night got busy with
prototyping a test harness.
<!--more-->

What I've got so far (in [my fork](https://github.com/hinrik/vim-perl/tree))
is a test file that uses Text::VimColor to generate HTML and compare it
against a reference HTML document to determine if the syntax file is doing its
job. If a reference file can't be found, it will create it and skip that
test. Here's what it looks like:

    $ make test
    prove -rv t
    t/01_highlighting.t .. 
    ok 1 - Correct output for t_source/perl/basic.t
    ok 2 # skip Created t_source/perl/advanced.t.html
    ok 3 - Correct output for t_source/perl6/basic.t
    1..3
    ok
    All tests successful.

In case of failure, it will use Test::Differences to show you what's wrong,
and write the incorrect output to disk for you to inspect:

    $ vim syntax/perl6.vim # make a bad change
    $ make test
    prove -rv t
    t/01_highlighting.t .. 
    ok 1 - Correct output for t_source/perl/basic.t
    ok 2 - Correct output for t_source/perl/advanced.t
    not ok 3 - Correct output for t_source/perl6/basic.t

    #   Failed test 'Correct output for t_source/perl6/basic.t'
    #   at t/01_highlighting.t line 77.
    #
    «output from Test::Differences showing the offending lines»
    # You can inspect the incorrect output at t_source/perl6/basic.t_fail.html
    1..3
    # Looks like you failed 1 test of 3.
    Dubious, test returned 1 (wstat 256, 0x100)
    Failed 1/3 subtests

The only big downside to this is that `01_highlighting.t` tests all the source
files in one go. You currently can't tell it to only test one specific file.
