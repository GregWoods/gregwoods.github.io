---
id: 259
title: Attempting to use Wireshark to debug WebSockets traffic
date: 2012-01-09T17:41:57+00:00

layout: single

guid: http://gregwoods.co.uk/?p=259
permalink: /2012/01/attempting-to-use-wireshark-to-debug-websockets-traffic/
categories:
  - Programming
---
I've been attempting to get some WebSockets code to work using SuperWebSockets and a simple html + javascript page in Chrome. My success has been limited to say the least. To add to the frustration, there is no easy way to examine the TCP data of the WebSocket stream. I use Fiddler extensively when developing web apps, but it is no use for WebSockets - at least not at the moment. Although some support is present - from what I can tell, you can only see the headers, not the stream.

It doesn't take much googling of this problem before you are told to go and use Wireshark. Although I've come across this network packet analyser before, I'd always quickly given up on it. This is not a reflection of the software, but of my impatience in getting to know enough of it to be usable. For WebSockets work, it seems I'm going to have to bite the bullet.

# First Problem: Localhost doesn't have a network interface

Why is this a problem? Because Wireshark needs a network interface to capture packets from. This interface is provided by your network card. Unix systems provide a 'fake' loopback network adapter for localhost. Windows doesn't.

The solution is to add an entry to  Windows' network routing table, so that traffic sent to your local ip address is routed to your network gateway, which will send it straight back to your ip address. Since the traffic now goes through your network adapter, Wireshark should be able to see it.

## Using Netcat to test the simplest case possible

To test this out, I will use [netcat for windows](http://joncraton.org/blog/netcat-for-windows "netcat for windows") . This utility allows us to set up a server which will listen on a port and display any text it receives in the console. The same utility also allows us to send traffic to this same port.

The easiest way to do this is to open two elevated command prompts.

**In Prompt 1 - set up the server**

<pre>nc -L -p 8111</pre>

<pre>-L mean listen, -p is port number</pre>

**In prompt 2 - Create a Route**

<pre>route add&lt;your ip&gt; &lt;your gateway ip&gt;</pre>

e.g.

<pre>route add 192.168.0.16  192.168.0.1</pre>

**Open Wireshark, add a filter**

<pre><strong></strong>tcp.port == 8111</pre>

**In prompt 2 - Connect to the server**

<pre>nc &lt;your ip&gt; 8111</pre>

type some stuff

You should see your text input appear in prompt 1, and see those packets captured in Wireshark. There you will see 3 entries for each request. The first is the original TCP request FROM your ip TO your ip, the second is an ICMP request for a redirect (the routing table at work). The third is the new TCP request FROM your gateway ip TO your ip.

Note that the route will not persist reboots without adding the -p option

So, that proves the network route works.

&nbsp;

# Back to WebSockets

Problem is, it doesn't work with websockets.

I set up SuperWebSocketsServerWeb,  the sample web app from the SuperWebSockets project. I used iis to host it.

  * With the loopback route deleted...
  * browsing to http://<local ip>/SuperWebSocketWeb ... the web site doesn't work
  * browsing to http://localhost/SuperWebSocketWeb ... the web site works, the connection opens and I can use the chat demo - though nothing is captured in Wireshark

  * With the route added...
  * browsing to http://<local ip>/SuperWebSocketWeb ... the web site works, the connection opens, a few packets are captured in Wireshark,  then the connection closes a few seconds later.

<div>
  I can't see why this last option doesn't work.
</div>

<div>
</div>

<div>
  My next step... is to try debugging SuperWebSocketWeb - initial attempts have proved unsuccessful however.
</div>

&nbsp;