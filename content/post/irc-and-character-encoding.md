+++
title = "IRC and character encoding"
date = "2008-05-01T01:44:00Z"
tags = ["irc", "perl"]
+++

A while ago, I wrote an IRC logger for
[POE::Component::IRC](http://search.cpan.org/dist/POE-Component-IRC/), which
is an IRC client module for Perl. The main challenge I faced was the issue of
character encodings. Since IRC is ripe with clients that use different
encodings, messages must be reliably decoded before they are written to a
file.
<!--more-->

You see, [RFC 1459](http://www.faqs.org/rfcs/rfc1459.html), the standards
document describing the IRC protocol, does not regulate the use of character
encodings:

    2.2 Character codes

    No specific character set is specified. The protocol is based on a
    set of codes which are composed of eight (8) bits, making up an
    octet. Each message may be composed of any number of these octets;
    however, some octet values are used for control codes which act as
    message delimiters.

    Regardless of being an 8-bit protocol, the delimiters and keywords
    are such that protocol is mostly usable from USASCII terminal and a
    telnet connection.

ASCII uses the first 7 bits. So, from the looks of it, you should only be able
to rely on the first seven bits representing an ASCII character, the
interpretation of the last bit being anyone's guess. That's bad.

For most of IRC's history, the most popular IRC client has been mIRC. Until
recently, mIRC decoded incoming messages using the ANSI code page that was
currently being used on the user's Windows system. This meant that whenever
mIRC users wanted to communicate using anything other than ASCII characters,
they'd better be using the same code page. In later versions, mIRC decodes
incoming messages as UTF-8 if they look UTF-8 encoded, or code page 1252 (used
by most Westerners). As for _how_ it does this, I cannot know since mIRC is
closed-source.

The open-source client irssi handles the situation similarly. It uses GLib's
[g_utf8_validate()](http://library.gnome.org/devel/glib/2.16/glib-Unicode-Manipulation.html#g-utf8-validate)
function to check if the incoming message is UTF-8 encoded, otherwise it falls
back to CP1252 by default. As for XChat, it uses the same GLib function, but
if it determines that the message is not UTF-8, XChat decodes the message in a
rather novel way. Here is an excerpt from its
[`src/common/text.c`](http://xchat.cvs.sourceforge.net/xchat/xchat2/src/common/text.c?view=markup):

{{< highlight c >}}
/* converts a CP1252/ISO-8859-1(5) hybrid to UTF-8                           */
/* Features: 1. It never fails, all 00-FF chars are converted to valid UTF-8 */
/*           2. Uses CP1252 in the range 80-9f because ISO doesn't have any- */
/*              thing useful in this range and it helps us receive from mIRC */
/*           3. The five undefined chars in CP1252 80-9f are replaced with   */
/*              ISO-8859-15 control codes.                                   */
/*           4. Handles 0xa4 as a Euro symbol ala ISO-8859-15.               */
/*           5. Uses ISO-8859-1 (which matches CP1252) for everything else.  */
/*           6. This routine measured 3x faster than g_convert :)            */
{{< /highlight >}}

How would I handle this in Perl? I don't want to depend on GLib, and I don't
want to write any C code (requiring the user to have a C compiler). At first I
tried using [Encode::Detect](http://search.cpan.org/dist/Encode-Detect/), but
there are two problems with it. It's an extra dependency, and more
importantly, it works heuristically, deciding which character set is being
used based on the number of occurences of each character code. As such, it's
only reliable when large amounts of data are involved. Like a whole web page,
for example, which is what the code was written for. Then I learned of
[Encode::Guess](http://perldoc.perl.org/Encode/Guess.html), which is included
with Perl as of version 5.6.0. The following decodes `$line` as UTF-8 if
Encode::Guess is sure that it's UTF-8. Otherwise it decodes it as CP1252.

{{< highlight perl >}}
use Encode qw(decode);
use Encode::Guess;

my $utf8 = guess_encoding($line, 'utf8');
$line = ref $utf8 ? decode('utf8', $line) : decode('cp1252', $line);
{{< /highlight >}}

So far this method has worked flawlessly for me on channels with mixed
encodings. However, I don't know exactly how Encode::Guess works, so I'm not
as confident in this method as I could be. Any feedback on this issue would be
quite welcome.

