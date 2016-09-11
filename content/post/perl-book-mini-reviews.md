+++
title = "Perl book (mini) reviews"
date = "2008-05-04T21:33:00Z"
lastmod = "2008-09-11T23:50:00Z"
tags = ["books", "perl"]
+++

I much prefer reading things in well typeset paperback books than on computer
screens. The subject of Perl is no exception. I've got quite a few Perl books.
Some reviews are in order. I haven't actually written a book review in many
years, so they won't be very "in-depth", though.

Oh, and by the way, this, too, [is a Perl blog](http://use.perl.org/~schwern/journal/36263).
<!--more-->

<style>.book-pic { float: right; padding: 10px; }</style>

## Programming Perl

{{< figure src="/books/progperl.png" alt="Programming Perl" class="book-pic" >}}

_By Larry Wall, Tom Christiansen, and Jon Orwant_

Ah, the Camel book. The latest edition is about 7 years old now, but it has
stood the test of time. If you only read one Perl book, make it this one.
Aside from being a comprehensive and detailed reference on the language, it's
also funny. One of my favorite passages is the start of chapter 10, Packages:

> In this chapter, we get to start having fun, because we get to start
> talking about software design. If we're going to talk about good software
> design, we have to talk about Laziness, Impatience, and Hubris, the basis
> of good software design.

> We've all fallen into the trap of using cut-and-paste when we should have
> defined a higher-level abstraction, if only just a loop or a subroutine.\*

> To be sure, some folks have gone to the opposite extreme of defining
> ever-growing mounds of higher-level abstractions when they should have
> used cut-and-paste.† Generally, though, most of us need to think about
> using more abstraction rather than less.

> Caught somewhere in the middle are the people who have a balanced view of
> how much abstraction is good, but who jump the gun on writing their own
> abstractions when they should be reusing existing code.‡

> ――――――――――

> \* This is a form of False Laziness.

> † This is a form of False Hubris.

> ‡ You guessed it — this is False Impatience. But if you're determined to
> reinvent the wheel, at least try to invent a better one.

The book is written for programmers, so if you've haven't programmed before,
you should probably start with an easier book. I've heard "Learning Perl" is
pretty good.

## The Perl Cookbook

{{< figure src="/books/perlcookbook.png" alt="Perl Cookbook" class="book-pic" >}}

_By Tom Christiansen and Nathan Torkington_

Here is another highly useful book. If you read the Camel book and thought
"What next?", then this book is the answer. It's got 900 pages of recipes for
how to do everything from sorting hashes to writing pre-forking TCP servers.
Each one of the 22 chapters begins with a few pages of very informative
discussion of the problem domain at hand. This book has been extremely useful
to me. It saves you a lot of Googling and looking through various Perl man
pages. I highly recommend it.

## Mastering Regular Expressions

{{< figure src="/books/masteringregex.png" alt="Mastering Regular Expressions" class="book-pic" >}}

_By Jeffrey Friedl_

While not strictly a Perl book, it is about regular expressions, which were
to a large extent popularized by Perl. Or the other way around. Or both. I'm
not sure. But hey, at least the chapter on Perl is the longest one in the
book.

Anyway, the book truly lives up to its title. It describes in detail how
regular expression engines work, how to write effecient expressions, how
programming languages support regexes, and more. Until I read this book, I did
not know that there are two main approaches to writing a regular expression
engine, a DFA (deterministic finite automaton) and an NFA (nondeterministic
finite automaton), or that the fastest way to strip leading and trailing
whitespace is (usually) like so:

{{< highlight perl >}}
s/^\s+//;
s/s+$//;
{{< /highlight >}}

I hadn't actually learned Perl before getting this book. Perl is used in most
of the examples in the book, which is what got me interested in the language.

## Mastering Algorithms with Perl

{{< figure src="/books/masteringalgorithms.png" alt="Mastering Algorithms with Perl" class="book-pic" >}}

_By Jon Orwant, Jarkko Hietaniemi, and John Macdonald_

I'm not a computer scientist. Perhaps that's why I found this book so
interesting. It has working Perl code accompanying all the algorithms that
are explained in the book, as well as discussions of pertinent CPAN modules.
Though I suspect that last part might be a bit outdated, as the book was
written almost a decade ago. If you know Perl and would like a hands-on
introduction to algorithms, this book is great.

## Perl Best Practices

{{< figure src="/books/perlbestpractices.png" alt="Perl Best Practices" class="book-pic" >}}

_By Damian Conway_

I liked this book. I like my code especially clean and readable, and this book
has very good guidelines that can help achieve that. The book is a joy to read
(it has humour!), and it's got very useful appendices at the end with quick
summaries of all the guidelines. Then, if you want to audit your source code
according to some of these (and other) guidelines, you can use the excellent
[Perl::Critic](http://search.cpan.org/dist/Perl-Critic/) module.

## Perl Hacks

{{< figure src="/books/perlhacks.png" alt="Perl Hacks" class="book-pic" >}}

_By `chromatic`, Damian Conway, and Curtis "Ovid" Poe_

This one is sort of like The Perl Cookbook, except it focuses more on the
process of working with Perl rather than specific solutions to various
programmatic problems. As such, it's not really aimed at beginners. It has
many very useful tricks regarding things like customizing your editor for
Perl, working with modules, (ab)using the guts of Perl, and debugging.
There's something in it for everyone.

## Higher-Order Perl

{{< figure src="/books/higherorderperl.png" alt="Higher Order Perl" class="book-pic" >}}

_By Mark Jason Dominus_

_Now_ it's getting interesting. In this book, the author tries to familiarize
the reader with ways of programming most common in purely functional
languages like Lisp and Haskell. That makes it very different from most Perl
books (in a good way). The book is all about "being clever" as the author has
said, so you're bound to learn something from it. I certainly have. The topics
covered include recursion, dispatch tables, currying, and parsing, to name a
few. There are [plans](http://hop.perl.plover.com/#free) to turn the book into
wiki, but I I'm not sure when that'll happen.

## Perl 6 and Parrot Essentials

{{< figure src="/books/perl6andparrot.png" alt="Perl 6 and Parrot Essentials" class="book-pic" >}}

_By Allison Randal, Dan Sugalski, and Leopold Toetsch_

This book is an excellent introduction to Perl 6 and Parrot (the virtual
machine which will run Perl 6), though I've been told that the Parrot bits
are a little dated now. I read it in one sitting, it was that exciting. I
realize that his book is about programming, and that this statement makes me
a total geek. Oh well, there's no looking back, Perl 6 will be awesome! The
first half of the book covers the Perl 6 language, while the second covers
the design of Parrot. I didn't absorb as much as I could have from the second
half as I don't know much about parsing or compilers, but the first half more
than made up for it. I really wish I could use all those nifty featues in my
code right now. In the meantime, [Pugs](http://en.wikipedia.org/wiki/Pugs)
will have to quence the thirst of those like me who are excited about Perl 6.

## Perl 6 Now

{{< figure src="/books/perl6now.png" alt="Perl 6 Now" class="book-pic" >}}

_By Scott Walters_

I didn't get much out of this book. For
one, many things are explained which most Perl users already know, so I
flipped over many pages while reading it. Secondly, many of the Perl 6 ideas
are illustrated with modules that use source filters, which are known to be
unreliable, so you definitely wouldn't use them in production code.

## Catalyst

{{< figure src="/books/catalyst.png" alt="Catalyst" class="book-pic" >}}

_By Jonathan Rockway_

The chapters in this book follow a very _practical_ approach, diving right in
and showing you various common ways of using Catalyst. I haven't written much
using this fine web framework, so there isn't really much more I can say about
the content of the book. I can say something about the _lack_ of content
though. This book is missing an overview of Catalyst, and a better explanation
of how all the parts fits together. Some discussion on the MVC architecture
and how Catalyst implements it would have been nice as well. Seeing as the
book is quite short, there would be plenty of room for these things.

## Perl Medic

{{< figure src="/books/perlmedic.png" alt="Perl Medic" class="book-pic" >}}

_By Peter J. Scott_

I was not disappointed by this book. It delivers what is promised. Having
recently started working on an old codebase, I found the book very useful.
Testing, refactoring, benchmarking, debugging; all these things are well laid
out by the author. It also has a useful chapter on upgrading code written for
older versions on Perl, and discusses how to make use of newer features.

