bash-port-scanner
=================

Port scanner in bash (TCP)

Usage
-----

First, source the functions:
<pre>. scanner</pre>

Execute the scan with the following syntax:
<pre>scan &lt;host&gt; &lt;port, ports, port-range&gt;</pre>

Example: 
<pre>scan google.com 78-82</pre>

Output
------
<pre>
user@host:~/bash-port-scanner$ . scanner
user@host:~/bash-port-scanner$ scan google.com 78-82
78/tcp closed
79/tcp closed
80/tcp open
81/tcp closed
82/tcp closed
user@host:~/bash-port-scanner$ scan google.com 25,80,443
25/tcp closed
80/tcp open
443/tcp open
</pre>

Background
----------
Original concept found here: http://www.catonmat.net/blog/tcp-port-scanner-in-bash/

I made a couple tweaks in the formatting. I plan to abstract it a little further to incorporate UDP.
