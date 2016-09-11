+++
title = "perl6.vim gets more love"
date = "2015-03-01T20:30:00Z"
lastmod = "2015-03-03T22:40:00Z"
tags = ["vim", "perl6"]
+++

tl;dr: Some tuits came my way, so Vim's syntax highlighting of Perl 6 is
much better and faster now. Try it!
<!--more-->

> \<timotimo\> hoelzro: i just skimmed the perl6 vim syntax and ... oh crap

> \<timotimo\> there's just no way i could even make a dent in that thing

> \* psch usually turns off highlighting in vim because it's so slow :/

> \<sorear\> perl 6 is not really syntax-highlightable

So...yeah, perl6.vim is a bit of a beast.

### Recent history of perl6.vim

Sometime in 2008 or so, I got interested in Perl 6, and I really wanted it
to be nicely higlighted in my editor (Vim) as I learned. As it turned out,
there was already a Vim syntax file for it, in the
[Pugs SVN](http://svn.openfoundry.org/pugs/util/perl6.vim) repository. This
was mostly the work of `lpalmer++` and `moritz++`. It worked decently, but
as I learned about more nooks and crannies of Perl 6 (there sure are enough
of them) I started finding the limitations of the highlighting to be
frustrating.

I wanted to make it better, so I started learning all about Vim's
regexes and syntax highlighting support. I began hacking on `perl6.vim`,
and soon enough it grew to be the largest Vim syntax file in existence.
Perl 6 is hard enough to parse already. Having to do so with Vim patterns,
doubly so. I made some progress but eventually the performance of the
highlighting suffered as it grew to support ever more complicated syntax.

In 2009, `alester++` created the vim-perl repository on Github to consolidat
Perl support for Vim. `perl6.vim` gained a new home shortly thereafter
when he imported it from the Pugs repo. Around the same I discovered
[Text::VimColor](https://metacpan.org/pod/Text::VimColor) and used it to
create a test harness for the syntax highlighting of `perl.vim` and
`perl6.vim`. I fixed a few Perl 5 highlighting bugs and added some tests
for them, but I never got around to doing the same for Perl 6.

Since then, a few contributors (`hoelzro++` et al) have continued to fix
bugs in `perl6.vim`. In the meantime, Perl 6 has also evolved, and some
of the assumptions `perl6.vim` has made are no longer valid.

A few weeks ago I went to FOSDEM 2015, where Larry announced that this
Christmas would be The One™. That rekindled my interest in `perl6.vim`,
and I'd like to share with you some of the progress I've made with it.

### Performance

Vim 7.4 ships with a [profiler](http://vimhelp.appspot.com/syntax.txt.html#%3Asyntime)
for its syntax highlighting. I used it to identify a lot of inefficient
patterns in the syntax file. I tried to reduce the use of zero-width
assertions (lookarounds) and to make more use of
[`nextgroup`](http://vimhelp.appspot.com/syntax.txt.html#%3Asyn-nextgroup)
instead when possible. I also optimized many patterns to reject matches as
soon as possible. As a result, Vim now needs to attempt much fewer matches,
and the ones it does attempt are taking less time to do their work.
Editing most Perl 6 files feels pretty snappy now, even
[STD.pm6](https://github.com/perl6/std/blob/master/STD.pm6).

### Identifiers

In `ftplugin/perl6.vim`, I added the apostrophe and high-bit alphabetical
characters (`æóð...`) to the list of characters vim recognizes in keywords
([`iskeyword`](http://vimhelp.appspot.com/options.txt.html#%27iskeyword%27))
This allows all valid Perl 6 identifiers to be used in Vim commands that
depend on matching keywords.

I also cleaned up the highlighting of Perl 6 idenfifiers, in particular
adding support for the high-bit characters and better support for dashes,
so these are now highlighted correctly in sub/package/variable/etc names.

### Multiline comments

These have been updated to recognize the new <code>#&#x60;</code> prefix,
and to be allowed at the beginning of a line. Previously, multiline comments
with stacked delimiters (`««`, `<<`, `<<<`, etc) were not highlighted by
default. Some profiling showed that doing so does not have a noticable
performance impact, so I changed it to always highlight them.

### Heredocs

I added highlighting of heredocs with `qto`, `qqto`, `q:to`, `qq:to`,
`q:heredoc`, and `qq:heredoc`, for most commonly used delimiters.

### Setting functions and methods

> \* TimToady wishes all these highlighters wouldn't treat setting functions and methods as reserved words; they're just functions and methods`

> \<moritz\> TimToady: agreed

> \* flussence wishes perl6.vim didn't highlight Test.pm functions as reserved words either...

By popular request, I removed highlighting of builtin functions and
methods. This makes sense since there's no way to avoid highlighting
user-defined methods that happen to share the name of a builtin one.

### Metaoperators

Highlighting these is one of the trickiest jobs of the syntax file. Yet
it's one of the most crucial because if you let e.g. a stray `R<` or
`[/` go unhighlighted, they will screw up the highlighting of the rest
of the file by starting a string where there isn't one.

I managed to make great improvements to the highlighting of reduce
(`[+]`), hyper (`»+«`), post-hyper (`@foo».bar`), reverse/cross/sequence/zip
(`Rdiv`, `R<`, etc), and set operators (`(<)`, `(>=)`). All the spec tests
for metaoperators I have looked at are now highlighted without issues.

### Strings and patterns

Another part of the language that presents a challenge is `/foo/`,
`<bar>`, `<<baz>>`, and `«quux»`. Determining when these are not actually
numeric division, less-than, or a hyperoperators is tricky. These things
are now matched much more accurately. I also added support for the `qqx`
and `qqw` operators.

### Grammars

Grammars are a whole other language in their own right, and this is where
there is still the most room for improvement (of both performance and
accuracy) in the syntax file. I still don't know grammars well enough,
but I've fixed all the highlighting issues I've found. STD.pm6 in its
entirety is now highlighted properly, although Vim can still get confused
occasionally until you scroll a bit or tell it to redraw the screen.

### Pod

The biggest change here is that I added highlighting of indented Pod
blocks. As part of the indentifier improvements mentioned above, Pod
block names containing hyphens or high-bit alphabetical chars are now
correctly highlighted.

### Folding

I added rudimentary support for syntax-based folding (disabled by default).

### Miscellaneous

* I improved highlighting of numbers and version literals
* Fixed a few issues where interpolated things weren't highlighted as such
* Made big improvements to highlighting of transliteration  (`tr///`,
  `tr{}{}`, etc) operators
* Added highlighting of bare/anonymous sigils in more places
* Highlighted the Unicode set operators (`∈`, `≽`, et al)
* Certain keywords (like `die`, `state`, etc) are no longer highlighted where
  they shouldn't be, e.g. as method calls (`$foo.state`)

### Testing

Of course, I added tests for every improvement and bugfix listed above, so
at least the highlighting should not be getting *worse* from now on.

### \_\_END\_\_

All open [vim-perl](https://github.com/vim-perl/vim-perl) Github issues
relating to Perl 6 highlighting bugs have been resolved. If you discover
any more problems, please open new issues.

I tried patching [perl6/doc](https://github.com/perl6/doc) to add an option
to use Text::VimColor to highlight code blocks in the documentation. While
it does result in richer and more accurate highlighting than the default
pygments-based highlighter, it is painfully slow to generate. This is because
Text::VimColor (and [`2html.vim`](http://ftp.vim.org/vim/runtime/syntax/2html.vim),
on which it is based) extracts Vim's highlighting by calling the
[`synID()`](http://vimhelp.appspot.com/eval.txt.html#synID%28%29) function
at every character position in the file, which is very slow. So while it may
only take Vim a few dozen milliseconds to highlight an entire file,
extracting the highlighting state into something usable by an external
tool takes several *seconds*. I wonder how difficult it would be to patch Vim
(or NeoVim) to export an entire file's highlighting in a more efficient
manner...

To close, here is a sample of some meaningless code that used to get
`perl6.vim` confused but just looks nice now:

<link rel="stylesheet" type="text/css" href="/css/vim_syntax.css">

<div class="vimcolor"><pre><span class="synKeyword">class</span> Johnny's::Super-Cool::Module<span class="synOperator">;</span>

<span class="synSpecial">my</span> <span class="synIdentifier">$cööl-páttérn</span> <span class="synComment">#`[why hello there]</span> <span class="synOperator">=</span> <span class="synDelimiter">/</span><span class="synString">foo</span><span class="synSpecialChar">+</span><span class="synDelimiter">/</span><span class="synOperator">;</span>
<span class="synKeyword">sub</span> infix<span class="synOperator">:</span><span class="synDelimiter">«</span><span class="synString">foo</span><span class="synDelimiter">»</span> { }

<span class="synKeyword">sub</span> foo-bar (<span class="synType">Int</span> <span class="synIdentifier">$a</span> <span class="synPreCondit">where</span> <span class="synOperator">*</span> <span class="synOperator">&gt;</span> <span class="synNumber">3</span><span class="synOperator">,</span> <span class="synIdentifier">@bar</span><span class="synOperator">,</span> <span class="synType">Str</span> <span class="synIdentifier">$b</span> <span class="synOperator">=</span> <span class="synDelimiter">'</span><span class="synString">foo</span><span class="synDelimiter">'</span>) {
    <span class="synSpecial">my</span> <span class="synIdentifier">$document</span> <span class="synOperator">=</span> <span class="synDelimiter">qto/END/</span><span class="synString">;</span>
<span class="synString">        you there</span>
<span class="synDelimiter">    END</span>

    <span class="synSpecial">my</span> <span class="synIdentifier">$document</span> <span class="synOperator">=</span> <span class="synDelimiter">qq</span><span class="synOperator">:</span><span class="synString">heredoc</span><span class="synDelimiter">/END/</span><span class="synString">;</span>
<span class="synString">        and </span><span class="synIdentifier">$b</span>
<span class="synDelimiter">    END</span>

    <span class="synSpecial">my</span> <span class="synIdentifier">$result</span> <span class="synOperator">=</span> <span class="synDelimiter">qqx/</span><span class="synString">ls -l bla</span><span class="synDelimiter">/</span><span class="synOperator">;</span>
    <span class="synSpecial">my</span> <span class="synIdentifier">@bla</span> <span class="synOperator">=</span> <span class="synOperator">[+]</span> <span class="synIdentifier">@bar</span><span class="synOperator">;</span>
    <span class="synSpecial">my</span> <span class="synIdentifier">@list</span> <span class="synOperator">=</span> <span class="synIdentifier">@bla</span> <span class="synOperator">Z,</span> <span class="synIdentifier">@bar</span><span class="synOperator">;</span>
    say <span class="synDelimiter">&quot;</span><span class="synString">yes</span><span class="synDelimiter">&quot;</span> <span class="synConditional">if</span> <span class="synIdentifier">$set1</span> <span class="synOperator">(&lt;)</span> <span class="synIdentifier">$set2</span><span class="synOperator">;</span>

    <span class="synStatement">=for</span> <span class="synType">Pro-tip</span>
<span class="synComment">    Pay careful attention to the following code</span>

    <span class="synConditional">if</span> <span class="synIdentifier">$a</span> <span class="synOperator">!&lt;</span> <span class="synNumber">4</span> {
        <span class="synIdentifier">@bar</span><span class="synOperator">».</span>bla<span class="synOperator">:</span> <span class="synDelimiter">&quot;</span><span class="synString">this </span><span class="synIdentifier">&amp;nice-func</span>()<span class="synString"> thing</span><span class="synDelimiter">&quot;</span><span class="synOperator">;</span>
    }
    <span class="synSpecial">my</span> <span class="synIdentifier">$bin</span> <span class="synOperator">=</span> <span class="synNumber">-0</span><span class="synSpecial">b</span><span class="synNumber">01010</span><span class="synOperator">;</span>

    (<span class="synNumber">1</span><span class="synOperator">,</span><span class="synNumber">2</span>)[<span class="synOperator">*/</span><span class="synNumber">2</span>]<span class="synOperator">;</span>
    say <span class="synIdentifier">$@foo</span><span class="synOperator">.</span>perl<span class="synOperator">;</span>
    <span class="synDelimiter">m</span><span class="synOperator">:</span><span class="synString">s</span><span class="synDelimiter">/</span><span class="synString">foo</span><span class="synDelimiter">/</span><span class="synIdentifier">$bar</span><span class="synOperator">/;</span>
}

<span class="synKeyword">sub</span> foo (<span class="synType">Int</span><span class="synOperator">:</span><span class="synString">D</span> <span class="synIdentifier">$bla</span>) <span class="synPreCondit">is</span> <span class="synTag">cached</span> { }
</pre>
</div>
