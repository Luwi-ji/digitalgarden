---
{"dg-publish":true,"permalink":"/cybersecurity/blogs/018-understanding-the-life-of-a-packet/","created":"2026-08-20T20:39:57.249+08:00","updated":"2026-08-21T23:56:03.675+08:00","dg-note-properties":{"created":"2026-07-24 22:22:18","updated":"2026-07-24 22:48:34","status":"Draft","tags":[]}}
---

Before moving on to network security protocols, I decided to take a step back.

I've already written about the **OSI Model**, packets and frames, TCP and UDP, ports, firewalls, VPNs, routers, switches, and VLANs.

At first, I thought I had a pretty good understanding of networking.

But the more I learned, the more I realized something:

**Knowing individual concepts isn't the same as understanding how they work together.**

So instead of immediately jumping into secure networking protocols, I went back to one of the earlier TryHackMe networking rooms: **Networking Concepts**.

I wanted to make sure my foundation was actually solid.

And surprisingly, going back helped me understand things I had previously only memorized.

---

# Starting With the OSI Model 

The OSI Model was one of the first networking concepts I studied.

It's a seven-layer conceptual framework for understanding how network communication works:

|Layer|Name|What I Understand|
|--:|---|---|
|7|Application|Network services used by applications|
|6|Presentation|Data encoding, compression, and encryption|
|5|Session|Establishing and managing communication sessions|
|4|Transport|End-to-end communication using TCP and UDP|
|3|Network|IP addressing and routing|
|2|Data Link|Communication between devices on the same network segment|
|1|Physical|Physical transmission of data|

When I first encountered these layers, I mostly saw them as seven things I needed to remember.

Now I look at them differently.

They're not just seven definitions.

They're different responsibilities involved in moving data from one application to another.

And that distinction matters.

---

# OSI vs TCP/IP

One thing I wanted to understand better was the difference between the **OSI Model** and the **TCP/IP Model**.

The OSI Model is primarily a conceptual framework.

The TCP/IP model is closer to how modern networking is actually implemented.

The TCP/IP model groups some of the OSI layers together:

|OSI|TCP/IP|
|---|---|
|Application|Application|
|Presentation|Application|
|Session|Application|
|Transport|Transport|
|Network|Internet|
|Data Link|Link|
|Physical|Link / Physical|

The important thing I took away isn't which model is "better."

It's that they give me different ways to think about the same networking process.

The OSI Model gives me a more detailed breakdown.

The TCP/IP Model gives me a more practical view of the protocols that make Internet communication possible.

That helped me understand why I keep seeing both models throughout cybersecurity resources.

---

# IP Addresses: More Than Just Numbers

The next part brought me back to IP addresses.

I've used IP addresses countless times while learning cybersecurity.

But going through the fundamentals again helped me understand the structure behind them.

An IPv4 address consists of **32 bits**, divided into four octets.

For example:

```text
192.168.1.10
```

Each octet represents 8 bits, giving a possible value from 0 to 255.

But the part I found more useful was revisiting **subnets**.

For example:

```text
192.168.66.89/24
```

The `/24` tells me that the first 24 bits represent the network portion.

That means addresses such as:

```text
192.168.66.1
192.168.66.2
192.168.66.50
192.168.66.100
```

can belong to the same subnet.

This connected directly to what I learned earlier about local networks.

I'm starting to understand that an IP address isn't simply an identifier.

It's also part of a larger addressing structure that helps devices determine whether another destination is local or somewhere else.

---

# Private vs Public IP Addresses

I also revisited the difference between **private and public IP addresses**.

The private IPv4 ranges defined by RFC 1918 are:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

I've seen addresses like `192.168.1.1` so many times that they almost feel ordinary now.

But understanding that these are **private addresses** explains why devices inside my home network can communicate with each other while those same addresses aren't directly routable across the public Internet.

This also led me back to something I encountered in the previous lesson:

**NAT as the Network Address Translation.**

A private device can access the Internet through a router using the network's public IP address.

So the IP address I see on my local device isn't necessarily the same address that the Internet sees.

That was an important distinction to reinforce.

---

# Routing: How Does the Packet Know Where to Go?

This brought me back to **routing**.

I already knew that routers operate at Layer 3 and use IP addresses to forward packets.

But I wanted to think about what that actually means.

Imagine sending a package to another country.

I don't personally need to know the entire journey.

I just need to give it the correct destination.

Intermediate postal facilities can decide where it should go next.

Routing works similarly.

A packet may pass through multiple routers before reaching its final destination.

Each router examines information such as the destination IP address and determines the appropriate next step.

So when I send data across the Internet, my computer isn't necessarily deciding the entire path.

It's participating in a much larger system of routers that continuously forward packets toward their destination.

That makes the Internet feel much less like one giant network and more like **many interconnected networks working together**.

---

# TCP and UDP — Looking at Them Again

I had already studied TCP and UDP in my previous learning journal.

But revisiting them after understanding IP addressing made their roles clearer.

An IP address identifies the **host**.

But that's not enough.

A single computer can run many applications and services simultaneously.

So how does the network know which application should receive the data?

That's where **port numbers** come in.

This gave me a simple mental model:

**IP address → Which host?**

**Port → Which process or service?**

That distinction seems simple now, but it helped connect Layer 3 and Layer 4 in my head.

---

# TCP: Reliable Communication

TCP is a **connection-oriented** transport protocol.

Before data is transmitted, the client and server establish a connection through the **Three-Way Handshake**:

```text
Client              Server

  SYN  ────────────→
       ←──────── SYN/ACK
  ACK  ────────────→

Connection established
```

The handshake allows both sides to synchronize and establish the connection.

TCP also uses sequence numbers and acknowledgements to help provide reliable and ordered data delivery.

This is something I understood much better this time.

TCP isn't simply:

**“Send the data and make sure it arrives.”**

There are actual mechanisms behind that reliability.

The receiver can acknowledge received data, identify missing or duplicated information, and help reconstruct the original stream.

---

# UDP: When Reliability Isn't the Priority

UDP takes the opposite approach.

It's **connectionless**.

There is no Three-Way Handshake.

There is no built-in acknowledgement mechanism like TCP's.

The sender simply sends the datagrams.

This gives UDP less overhead and makes it useful for applications where waiting for retransmission isn't necessarily desirable.

The important thing I took away is that TCP and UDP aren't competing to be the "better" protocol.

They're designed around different requirements.

**TCP prioritizes reliable, ordered communication.**

**UDP prioritizes simplicity and low overhead.**

---

# Encapsulation Finally Makes Sense

This was probably the most valuable part of revisiting the room.

I had already learned about encapsulation in my previous posts.

But now I could see the entire process more clearly.

Imagine I send a message through an application.

It starts as:

**Application Data**

Then the Transport Layer adds its information:

**TCP Segment / UDP Datagram**

Then the Network Layer adds an IP header:

**IP Packet**

Then the Data Link Layer adds its own information:

**Frame**

So the simplified process looks like:

```text
Application Data
       ↓
TCP Segment / UDP Datagram
       ↓
IP Packet
       ↓
Ethernet / Wi-Fi Frame
       ↓
Physical Transmission
```

Each layer adds information needed for its own responsibilities.

On the receiving side, the process happens in reverse.

That's **decapsulation**.

This was one of those concepts that I technically already knew, but revisiting it helped turn it from something I memorized into something I could actually visualize.

---

# The Life of a Packet

The most interesting part of the room was putting everything together into a single journey.

For example, imagine that I search for something on TryHackMe.

I enter my search query in the browser and press Enter.

The browser prepares an HTTP request.

If the connection is using HTTPS, the communication is secured through the appropriate protocols.

The Transport Layer handles the TCP connection.

The TCP segment is passed down to the Internet Layer.

The IP layer adds the source and destination IP addresses.

Then the Link Layer encapsulates the packet into a frame.

The frame is transmitted to my router.

The router examines the destination IP address and decides where to forward the packet next.

The packet may pass through several routers before reaching the destination network.

Then the process happens in reverse.

The destination device receives the frame, removes the Layer 2 information, processes the IP packet, processes the transport-layer information, and eventually delivers the original data to the appropriate application.

What started as:

**“I searched for something.”**

actually involved multiple layers of networking underneath.

That was probably my biggest takeaway from this room.

---

# I Also Got to Talk Directly to a Server

The room also introduced me to **Telnet**.

Telnet is an old protocol designed for remote terminal communication, but it can also be used to connect to a TCP service listening on a particular port.

For example:

```bash
telnet MACHINE_IP 7
```

can connect to an echo service.

I could send text and have the server send it back.

I could also connect to other services, such as the daytime service or an HTTP server.

One example was connecting to port 80 and manually sending an HTTP request:

```text
GET / HTTP/1.1
Host: telnet.thm
```

Seeing an HTTP request manually like this was interesting because it stripped away the browser interface.

Normally, I type a website address and the browser handles everything.

With Telnet, I could see that underneath the interface, communication is still based on protocols and structured messages.

It reminded me of something I've been realizing throughout this journey:

**The tools and interfaces we use often hide the underlying technology.**

Learning cybersecurity means learning how to look underneath them.

---

# What I Learned

Going back to Networking Concepts reinforced several important ideas for me:

- The **OSI Model** provides a framework for understanding network communication.
    
- The **TCP/IP Model** provides a practical model for Internet networking.
    
- **IP addresses** provide logical addressing for hosts.
    
- **Subnets** organize IP addresses into networks.
    
- **Private IP addresses** are used within private networks and aren't directly routable across the public Internet.
    
- **Routers** forward packets between networks.
    
- **TCP** provides connection-oriented and reliable communication.
    
- **UDP** provides connectionless communication with less overhead.
    
- **Ports** identify processes and services on a host.
    
- **Encapsulation** adds information as data moves down the networking stack.
    
- **Decapsulation** removes that information as data moves back up the stack.
    
- **Telnet** can be used to manually communicate with TCP services.
    

But more importantly, I learned something about **how I should learn cybersecurity**.

---

# Conclusion

I originally wanted to move on to **Networking Secure Protocols**.

But instead of rushing forward, I decided to make sure I actually understood the networking concepts that come before it.

I'm glad I did.

Because now, when I think about a packet traveling across the Internet, I don't just see an abstract piece of data.

I can imagine its journey:

**Application → Transport → IP → Frame → Router → Network → Router → Destination**

I can think about its source and destination IP.

I can think about its transport protocol and port.

I can think about the frame carrying it across the local network.

And I can think about the routers forwarding it toward its destination.

I'm starting to understand not just **what networking concepts are**, but **how they work together to make communication possible**.

And now I feel much more prepared to take the next step.

---
# Next Rabbit Hole

Now that I've strengthened my understanding of the networking fundamentals, I'm ready to explore the next part of the journey:

**Networking Essentials.**

From there, I'll continue building toward **Networking Core Protocols** and eventually **Networking Secure Protocols**.

The goal isn't to rush through the rooms.

It's to understand the foundation well enough that when I eventually study secure protocols, I can understand **what problem they're solving and why they exist**.

---
### Resources

- TryHackMe — [Networking Concepts](https://tryhackme.com/r/room/networkingconcepts)
- TryHackMe — [Networking Essentials](https://tryhackme.com/r/room/networkingessentials)