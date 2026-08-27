---
{"dg-publish":true,"permalink":"/cybersecurity/blogs/019-what-happens-after-the-packet-leaves-my-computer/","created":"2026-08-24T13:43:42.698+08:00","updated":"2026-08-27T13:20:32.583+08:00","dg-note-properties":{"created":"2026-07-24 22:22:18","updated":"2026-07-24 22:48:34","status":"Draft","tags":[]}}
---

After learning about the OSI Model, packets, frames, TCP, UDP, and ports, I started understanding how data moves between devices.

But I still had a lot of questions.

**How does my computer automatically get an IP address?**

**How does it know the MAC address of another device?**

**How does a packet know which path to take across the Internet?**

And probably the most interesting one:

**How can all the devices in my house access the Internet when my ISP only gives me one public IP address?**

These questions led me to the next TryHackMe room: **Networking Essentials**.

Instead of introducing completely new networking concepts, this room helped me connect the things I already learned and understand what happens behind the scenes.

---
# DHCP — How Does My Computer Get an IP Address?

One of the first things I learned was **DHCP**, or Dynamic Host Configuration Protocol.

Before this, I knew that a device needs an IP address to communicate over a network. But I never really thought about **how my laptop actually gets one**.

When I connect to a Wi-Fi network, I don't manually enter:

- my IP address
    
- subnet mask
    
- default gateway
    
- DNS server
    

Yet somehow, my computer gets all of them automatically.

That's where DHCP comes in.

DHCP allows devices to automatically receive the network configuration they need.

The process follows four steps that are easy to remember as **DORA**:

**Discover → Offer → Request → Acknowledge**

The process starts with my device asking:

> "Is there a DHCP server here?"

The DHCP server then offers an available IP address.

My device requests that address, and finally, the server acknowledges the request and assigns the configuration.

What I found interesting was what happens **before the device even has an IP address**.

The client initially uses:

```text
0.0.0.0
```

and sends the request to:

```text
255.255.255.255
```

It also uses the broadcast MAC address:

```text
ff:ff:ff:ff:ff:ff
```

That makes sense when I think about it.

The device doesn't know where the DHCP server is yet, so it has to essentially ask **everyone on the local network**.

By the end of the process, the device receives the information it needs to communicate:

**IP address + gateway + DNS server.**

Something that normally feels automatic suddenly became a process I could actually visualize.

---

# ARP — Connecting IP Addresses to MAC Addresses

The next concept was **ARP**, or Address Resolution Protocol.

This connected directly to something I learned earlier about packets and frames.

An IP address operates at Layer 3, while a MAC address is used at Layer 2.

But if my computer knows the destination's IP address, how does it know which MAC address to put inside the Ethernet frame?

That's what ARP helps solve.

Imagine my computer wants to communicate with:

```text
192.168.66.1
```

but it doesn't know the device's MAC address.

It sends an **ARP Request** asking:

> "Who has 192.168.66.1?"

Because it doesn't know the destination MAC address yet, the request is broadcast across the local network.

The device that owns that IP address responds with an **ARP Reply** containing its MAC address.

Now my computer knows where to send the Layer 2 frame.

This helped me connect two concepts that previously felt separate:

**IP address → identifies the destination at Layer 3**

**MAC address → identifies the local destination at Layer 2**

ARP acts as the bridge between the two.

---

# ICMP — Learning How to Troubleshoot Networks

After DHCP and ARP, I moved on to **ICMP**, or Internet Control Message Protocol.

This is where networking started becoming much more practical for me.

I've used `ping` before, but I never really thought about what was happening underneath it.

When I run:

```bash
ping 192.168.11.1
```

my computer sends an **ICMP Echo Request**.

If the destination receives it and responds, I get an **ICMP Echo Reply**.

The result gives me useful information such as:

- whether the host is reachable
    
- whether packets are being lost
    
- how long the round trip takes
    

For example:

```text
4 packets transmitted
4 received
0% packet loss
```

Now I understand that `ping` isn't just a random connectivity test.

It's actually using a networking protocol to determine whether communication between two hosts is working.

---

# Traceroute — Following the Path of a Packet

Then I learned about `traceroute`.

This one was especially interesting because it allowed me to visualize something I've wondered about for a long time:

**How many routers does my traffic actually pass through before reaching a website?**

Traceroute takes advantage of the **TTL (Time To Live)** field in an IP packet.

Every router that forwards the packet decreases its TTL by one.

When the TTL reaches zero, the router drops the packet and sends an ICMP **Time Exceeded** message back.

By manipulating the TTL, traceroute can discover the routers along the path.

So instead of simply thinking:

**My computer → Website**

I can now think:

**My computer → Router → ISP → More routers → Other networks → Destination**

And the interesting part is that the route can change.

The Internet isn't one fixed road.

There can be multiple possible paths between two destinations.

---

# Routing — How Does the Internet Know Where to Go?

This naturally led me to **routing**.

I already knew that routers operate at Layer 3 and forward packets based on IP addresses.

But now I started looking at the bigger picture.

The Internet contains millions of routers and countless networks.

There needs to be a way for these routers to determine where packets should go.

That's where routing protocols come in.

Some of the protocols I encountered were:

- **OSPF** — Open Shortest Path First
    
- **EIGRP** — Enhanced Interior Gateway Routing Protocol
    
- **BGP** — Border Gateway Protocol
    
- **RIP** — Routing Information Protocol
    

The one that stood out the most to me was **BGP**.

BGP is used to exchange routing information between different networks and plays a major role in how traffic moves across the Internet.

This made me realize that when I open a website, the packet isn't simply traveling through "the Internet."

It's traveling through a constantly changing collection of interconnected networks that need to cooperate to deliver that packet.

---

# NAT — How Can Multiple Devices Share One Public IP?

Then I reached **NAT**, or Network Address Translation.

This answered one of the questions I had earlier.

At home, I might have:

- my laptop
    
- my phone
    
- a smart TV
    
- other devices
    

All using private IP addresses.

But my ISP might only provide my network with **one public IP address**.

So how can all of these devices access the Internet?

NAT allows the router to translate between private and public addresses.

For example, internally, my laptop might use:

```text
192.168.0.129
```

with a particular source port.

When the connection goes out to the Internet, the router can translate that connection so the external server sees the router's public IP instead.

The router keeps track of these connections in a translation table.

So from the perspective of the internal network:

```text
Laptop → Private IP
```

But from the perspective of the Internet:

```text
Internet → Public IP
```

The router handles the translation in between.

This helped me understand why private IP addresses such as:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

can be used by countless private networks without needing to be globally unique.

---

# Everything Started Connecting

What I liked most about this room is that it didn't feel like I was learning completely isolated concepts.

Instead, I started seeing how everything connects.

For example:

**DHCP** gives my device its network configuration.

**ARP** helps it discover the MAC address needed for local communication.

**IP** provides logical addressing between networks.

**Routers** determine where packets should go.

**ICMP** helps me troubleshoot connectivity and discover network paths.

**NAT** allows multiple private devices to communicate with the Internet through a public IP address.

And underneath all of this are the concepts I learned from the previous rooms:

**OSI Model → Packets → Frames → TCP/UDP → Ports**

The more I learn, the more networking starts to feel like one interconnected system instead of a collection of definitions.

---

# Why This Matters to My Cybersecurity Journey

This room also changed how I think about network security.

Before, I mostly thought about networking as something necessary for devices to communicate.

Now I'm starting to see that **network behavior itself can provide valuable information for security**.

If I understand DHCP, I can understand how devices appear on a network.

If I understand ARP, I can understand how local devices discover each other.

If I understand routing, I can understand how traffic moves between networks.

If I understand NAT, I can understand how internal devices communicate with external systems.

And if I understand ICMP, I can use tools like `ping` and `traceroute` to investigate connectivity and network paths.

These aren't just networking concepts anymore.

They're becoming part of the foundation I need for cybersecurity.

---

# What I Learned

The biggest lesson I took from **Networking Essentials** is that networking is much more dynamic than I initially thought.

A device joining a network isn't simply "getting an IP."

There is a whole process happening behind the scenes.

A packet isn't simply "sent to the Internet."

It gets encapsulated, forwarded, routed, translated, and eventually delivered through a chain of networks and devices.

And when something goes wrong, protocols like ICMP can help me investigate what happened.

I'm slowly learning to look beyond what I see on the screen and ask:

**"What's actually happening underneath?"**

That's probably becoming one of the most important habits in my cybersecurity journey.

---

# Next Rabbit Hole

Now that I understand the essentials of how devices **get configured, discover each other, route traffic, troubleshoot connections, and communicate across networks**, my next step is to dive deeper into the protocols that make everyday network communication possible.

**Next Rabbit Hole: Networking Core Protocols.**

---
### Resources
- TryHackMe — [Networking Essentials](https://tryhackme.com/r/room/networkingessentials)
- [Youtube](https://youtu.be/R3zZi_d21bk)
