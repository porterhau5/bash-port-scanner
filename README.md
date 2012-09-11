bash-port-scanner
=================

Port scanner in bash (TCP)

Usage
-----

First, source the functions:
. scanner

scan <host> <port, ports, port-range>

Example: scan google.com 78-82

Output
------
<pre>
user@host:~/bash-port/scanner$ . scanner
user@host:~/bash-port/scanner$ scan 78-82 google.com
78/tcp closed
79/tcp closed
80/tcp open
81/tcp closed
82/tcp closed
user@host:~/bash-port-scanner$ scan 25,80,443 google.com
25/tcp closed
80/tcp open
443/tcp open
</pre>

Background
----------
Original concept found here: http://www.catonmat.net/blog/tcp-port-scanner-in-bash/

I made a couple tweaks in the formatting. I plan to abstract it a little further to incorporate UDP.
