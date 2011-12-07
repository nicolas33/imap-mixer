
Overall approach
================

Notice that you may intervert both IMAP client and server at your convinience.

Overview::

   +----------------------------+-------+------------------+ 
   |                            |------>|                  | 
   |       Test suites          |       |   IMAP client    | 
   |                            |<------|                  | 
   +-------+-----+--------------+       |                  |
   | other | API | command line |       |                  |
   +-------+-----+--------------+-------+------------------+
       ^      ^       ^                      ^       ^
    (a)|      |  (b)  |                      |       |
       |      +---+---+                      |       |
       |          |                          |       |
     [STOMP PROTOCOL]                        |       |
       |          |                          |       |
       v          v                          |       |
    +------------------+                     |       |
    |                  |          (c)(f)     |       |
    |    imap-mixer    |<--------------------+       |
    |  (proxy server)  |                             |
    |                  |                             |
    +------------------+                             |
          |      ^                                   |
       (d)|      |                                   |
          |   (e)|                                   |
          v      |                                   |
    +------------------+                             |
    |                  |                   (i)       |
    |   IMAP server    |<----------------------------+
    |     backend      |
    |                  |
    +------------------+



STEP 1
------

The test suites dynamically configure the imap-mixer proxy by using the STOMP
protocol (a & b).

To make this work easy, the STOMP protocol is hided by the provided API and
command line. Though, you're not supposed to use them. You might write your own
STOMP implementation. If a API is missing for the language you'd like, please
send your implementation to the project.


STEP 2
------

The IMAP client does his work as IMAP client zealot (c).

STEP 3
------

The proxy blindly relay the messages to the IMAP server.

STEP 4
------

The proxy receives the messages from the IMAP server. Here, 4 scenaries might
happen:
- the answer is stay as is;
- the answer is ignored;
- the answer is dynamically changed (by a matching trigger);
- the answer is superseded by a predefined static answer.

The first two cases are easy. The latters are explained in the dedicated section
of this documentation.

STEP 5
------

The answer is sent back to the IMAP client.

STEP 6
------

The test suites ask the imap-mixer proxy for raw results, IMAP server states
(e.g.: did the server received a new mail?), statistics, etc.

