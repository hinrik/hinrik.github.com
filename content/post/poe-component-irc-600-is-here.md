+++
title = "POE::Component::IRC 6.00 is here"
date = "2009-03-05T03:03:00Z"
tags = ["irc", "perl"]
+++

[POE::Component::IRC](http://search.cpan.org/dist/POE-Component-IRC) version
6.00 has just been released on CPAN. I've neglected to blog about PoCo::IRC
since I started contributing to it, but since a new major release has been
rolled out[1], now would be a good time. Also, as it turns out, next May will
be the tenth anniversary of the project's first release.
<!--more-->

For the uninitiated, POE::Component::IRC is an event-driven IRC client library
built on top of POE. People mostly use it to write bots. Some have made that
even easier by creating a simpler interface suited to that task (see
Bot::BasicBot).

I became involved in the project about 14 months ago, fixing bugs and adding
features. There've been about 50 releases during that time, so there's
something for everybody. Following is a list of the most prominent ones.

### Important squashed bugs

  * Quite a few DCC-related bugs have been fixed, error handling and diagnostics have been improved.
  * A bug causing the NickReclaim plugin to only try to reclaim the nick once has been fixed.
  * POE::Component::IRC::State was reacting incorrectly to some WHO replies sent by IRC servers that veered from the RFCs, causing it to hold inconsistent information. This has been fixed.
  * When raw messages were enabled, the raw line was not provided with CTCP-related events. Fixed.
  * POE::Component::IRC::State would issue more WHO commands than necessary when another user would join more than one of the component's channels. No more.

### New major features

  * POE::Component::IRC::Common, which provides many helper functions, now has functions for identifying and stripping color/formatting from IRC messages. It also defines IRC color constants for use in messages.
  * We now handle FreeNode's IDENTIFY-MSG capability, which means that can you always know whether a user had identified with NickServ when s/he wrote a particular message.
  * Sending and receiving files with spaces in them over DCC is now supported.
  * All DCC-related events now provide the IP address of the peer.
  * DCC resume support has been implemented.
  * The BotTraffic plugin now send an event for every CTCP ACTION issued by the client.
  * We now guard against sending IRC protocol messages that are too long and might get us booted off the server.
  * The Connector plugin (takes care of maintaining the connection to the IRC server) now supports cycling through a list of servers when reconnecting.
  * The CTCP plugin can now respond to CTCP SOURCE requests for you.
  * POE::Component::IRC::State and can now track the away status of users for you.
  * POE::Component::IRC::State now keeps track of a channel's creation time.
  * Added NICKSERV, SERVLIST, and SQUERY commands.
  * Plugins can now respond to custom events which have not been explicitly defined by POE::Component::IRC.

### New plugins

I wrote 5 additional core plugins:

  * First of all, the **Logger** plugin. It logs channel/private/dcc chat activity to files on disk like normal IRC clients do.
  * Then there's **AutoJoin**, which takes care of keeping you on your favorite channels, whatever happens.
  * **NickServID** deals with identifying your user to NickServ.
  * A **CycleEmpty** plugin which reclaims ops on channels that become empty.
  * **BotCommand**, which allows you to register commands that your bot handles, and get back an appropriate event when one is issued.

### Testing

The test suite has been reorganized, many tests improved and more added. The
test coverage (as reported by Devel::Cover) has increased from 40% (version
5.48) to 61% (version 6.00).

### Refactoring

Much refactoring was done. The coding and indenting style has also been made
consistent across the project, and many spotty coding practices have been
eliminated (thanks, Perl::Critic).

POE::Filter::CTCP was merged with POE::Filter::IRC:Compat, and the former was
removed. DCC support has been moved into its own plugin, and the plugin system
itself has been ripped out in favor of POE::Component::Pluggable (which is
based on the aforementioned plugin system).

Using the project's current Perl::Critic parameters, version 6.00 has zero
policy violations in 11,791 lines of code, compared to version 5.48's 242
violations in 10,634 lines of code. The average
[McCabe](http://en.wikipedia.org/wiki/Cyclomatic_complexity) score of
subroutines also dropped from 4.21 to 3.45.

### Documentation

Last but not least, the Pod docs have been improved. Errors have been fixed,
much more formatting and linking has been added for easier reading and
browsing, consistency has been improved, and many sections have been expanded.

I also added a
[cookbook](http://search.cpan.org/perldoc?POE::Component::IRC::Cookbook) with
a few recipes showing off some of the things one can do with
POE::Component::IRC.

### Credits

Thanks to all the users who provided feedback, bug reports and patches. You
helped make this happen. I also couldn't have done many of these things
without the help of Chris 'BinGOs' Williams, the senior maintainer of
POE::Component::IRC.

Now go write some IRC bots (or clients)!

_Notes:_

1. It's actually quite an insignificant release. Historically,
POE::Component::IRC versions have always passed the whole-number boundaries
naturally as part of a regular "bump the version number up by 0.02 for the
next release" process.

