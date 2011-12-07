.. -*- coding: utf-8 -*-

.. _mailing list: http://lists.alioth.debian.org/mailman/listinfo/offlineimap-project
.. _github: git://github.com/nicolas33/imap-mixer.git
.. _IMAPMIXER: https://github.com/nicolas33/imap-mixer

======
README
======

.. contents::
.. sectnum::


Description
===========

`IMAPMIXER`_ is a tool to make testing of any IMAP client/server easy. Also,
it's a very good tool to analyse an IMAP session or study the IMAP protocol.

As you might test both a client and a server (with respectively a server and
client as backend) we use another terminology:
- the IMAP client/server you want to test is called the *zealot*;
- the IMAP client/server backend is called the *guardian*.


Official repository is at `github`_.

`IMAPMIXER`_ is written with two kind of user targets in mind:
- users and developers wanting to deploy `IMAPMIXER`_ themselves;
- maintainer(s) of your IMAP client/server already provide this tool for you.


Design overview
===============

`IMAPMIXER`_ is an IMAP proxy which means it does *not* rely on any IMAP
client/server.  Although you are free to use any IMAP backend you like be aware
that embedded (fake) ones are provided.

You can interact with `IMAPMIXER`_ in 3 ways from a test suites (called
mandatory agent):
- the API from your prefered language (recommended);
- the command-line (usefull for shell scripts but slow);
- the local unix socket with STOMP protocol of your own.

Brief overview::

            +-------------+ +------------+
            | test suites | |   zealot   |
            +-------------+ +------------+
                |    ^         |
                |    |         |
                v    |         |
            +------------+     |
            | imap-mixer |     | (direct connection)
            +------------+     |
                |    ^         |
                |    |         |
                v    |         |
            +-------------+    |
            |   guardian  |<---+
            +-------------+


Since you're using IMAP, you should be able to directly create a external IMAP
link (usefull if you intend to squeeze behind the proxy).

For more background, check out the dedicated documentation.


Method of Operation
===================


Documentation
=============


Reporting bugs and contributions
================================

Bugs
----

Bugs, issues and contributions should be reported to the `mailing list`_.
**Please, don't use the github features (messages, pull requests, etc) at all.
It would most likely be discarded or ignored.**

