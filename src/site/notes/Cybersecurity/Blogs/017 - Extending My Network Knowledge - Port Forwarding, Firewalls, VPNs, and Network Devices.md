---
{"dg-publish":true,"permalink":"/cybersecurity/blogs/017-extending-my-network-knowledge-port-forwarding-firewalls-vp-ns-and-network-devices/","created":"2026-08-14T23:22:50.348+08:00","updated":"2026-08-21T08:17:46.281+08:00","dg-note-properties":{"created":"2026-07-24 22:22:18","updated":"2026-07-24 22:48:34","status":"Draft","tags":[]}}
---


After learning about packets, frames, TCP, UDP, and ports, I started to understand how data actually moves across a network.

But that raised another question.

**What controls where that traffic can go?**

Knowing how communication works is one thing.

Understanding how networks are connected, controlled, and protected is another.

So my next step was to explore four concepts that started bringing the bigger picture together:

**Port forwarding, firewalls, VPNs, and networking devices.**

---

# Port Forwarding: Making Services Accessible

The first concept I encountered was **port forwarding**.

I already knew that ports are used to identify services running on a device.

But what happens when a service inside a private network needs to be accessed from the Internet?

That's where port forwarding comes in.

Imagine a server inside a private network with the address:

```text
192.168.1.10
```

and a web server running on port **80**.

Devices inside that local network can access it.

But devices on the Internet can't simply connect directly to that private IP address.

If the administrator wants the web server to be publicly accessible, the network's router can be configured to **forward traffic from a specific external port to the internal server**.

For example:

```text
Internet
   ↓
Public IP
   ↓
Router
   ↓
192.168.1.10:80
```

This allows traffic arriving at the router to be forwarded to the appropriate service inside the private network.

This was an important distinction for me because I initially thought port forwarding and firewalls were basically the same thing.

They're not.

**Port forwarding determines where traffic can be forwarded.**

**A firewall determines whether traffic should be allowed or denied.**

That distinction became much clearer as I continued through the lesson.

---

# Firewalls 101

If port forwarding helps determine where traffic goes, then a **firewall** helps determine whether that traffic should be allowed through.

The analogy that helped me understand this was **border security**.

Imagine a country with a border.

Not everyone who arrives should automatically be allowed in.

The border security system can ask questions like:

- Where are you coming from?

- Where are you going?

- What are you trying to access?

- What type of traffic are you using?


A firewall works in a similar way.

It can be configured to **permit or deny traffic** based on different characteristics.

For example:

- source address

- destination address

- port

- protocol


So if a firewall rule says that traffic to port 80 is allowed, HTTP traffic may be permitted.

If traffic comes from a blocked source or attempts to access a restricted service, the firewall can deny it.

This made me realize that network security isn't necessarily about stopping all traffic.

It's about **controlling which traffic is allowed and which isn't**.

---

# Stateful vs Stateless Firewalls

I also learned that firewalls can operate in different ways.

Two important categories are **stateful** and **stateless** firewalls.

### Stateless Firewalls

A stateless firewall evaluates individual packets against a predefined set of rules.

It doesn't maintain the broader context of the connection.

This makes it relatively simple and resource-efficient.

But it also means that the firewall has less context when making decisions.

### Stateful Firewalls

A stateful firewall keeps track of the state of network connections.

Instead of looking at every packet completely independently, it can consider the broader context of the connection.

For example, it can understand that a packet belongs to an already-established TCP connection.

This gives the firewall more information when making decisions, although it also requires more resources.

The difference helped me understand that packet inspection isn't always just:

**“Is this packet allowed?”**

Sometimes the firewall also needs to ask:

**“What is happening with this connection?”**

---

# VPNs: Creating a Private Path

The next concept I encountered was something I've heard about many times before:

**VPNs.**

A **Virtual Private Network** creates a secure connection between devices or networks over the Internet.

The easiest way I found to understand it was to think about a **tunnel**.

Imagine two offices located in different places.

Normally, they're connected through the public Internet.

A VPN can create a secure tunnel between them so that devices in one office can communicate with resources in the other office as though they were part of a connected private network.

The important part is that the communication is protected through encryption.

This makes VPNs useful for situations where data needs to travel across networks that aren't completely trusted.

---

# VPNs in the Real World

One example that made this especially relevant to my cybersecurity learning was **TryHackMe itself**.

TryHackMe uses a VPN to allow users to connect to vulnerable machines without exposing those machines directly to the public Internet.

That means I can interact with the machines through a controlled environment rather than having those systems openly accessible from anywhere on the Internet.

This made the concept much easier to understand because I wasn't just learning about VPNs theoretically.

I've actually used one as part of my cybersecurity training.

---

# VPN Technologies

The lesson also introduced me to several VPN technologies, including:

- **PPP**

- **PPTP**

- **IPsec**


I found this section interesting because it showed me that VPNs aren't just one specific technology.

They're built using different protocols and technologies that have evolved over time.

For example, **IPsec** provides security at the IP level and is widely used for securing network communication.

I also learned about **PPTP**, which is much older and has significant security weaknesses compared with modern alternatives.

This was another reminder that in cybersecurity, knowing that a technology exists isn't enough.

I also need to understand **whether that technology is still considered secure**.

---

# Routers: Connecting Networks

After learning about how networks are controlled, I moved on to the physical devices that make those networks possible.

The first was the **router**.

I had already encountered routers when learning about the Network Layer of the OSI Model.

Now I had a clearer understanding of what they actually do.

A router's primary job is to **connect different networks and forward packets between them**.

That's where routing comes in.

If a packet needs to travel from one network to another, the router determines where it should go next.

The path isn't necessarily always the same.

Routing decisions can consider factors such as:

- path length
- reliability
- connection speed
- routing protocols

This connected directly back to what I learned earlier about Layer 3.

**Routers operate primarily at Layer 3 because they make forwarding decisions using IP addressing.**

---

# Switches: Connecting Devices Within a Network

Then I came back to something I had already encountered earlier in my networking lessons:

**switches.**

A switch connects multiple devices within a network.

While a router connects different networks, a switch primarily connects devices **within the same network**.

This distinction became much clearer to me:

**Switch → connects devices**

**Router → connects networks**

At Layer 2, switches use **MAC addresses** to determine where frames should be forwarded.

Remembering what I learned from the previous lesson made this much easier to understand.

A packet contains Layer 3 information such as IP addresses.

That packet can be encapsulated inside a Layer 2 frame.

The switch then uses the frame's MAC address information to determine which device should receive it.

Suddenly, the concepts I had learned separately started connecting together.

---

# Layer 2 vs Layer 3 Switches

I also learned that not all switches operate at exactly the same level.

A **Layer 2 switch** primarily forwards frames using MAC addresses.

A **Layer 3 switch** can also perform routing functions using IP addresses.

This makes Layer 3 switches more capable than traditional Layer 2 switches.

This distinction was interesting because it showed me that networking devices aren't always neatly separated into one role.

Some devices can perform multiple networking functions.

---

# VLANs: Separating a Network

The final concept that really caught my attention was **VLANs — Virtual Local Area Networks**.

A VLAN allows devices connected to the same physical network infrastructure to be logically separated.

For example, imagine a company with:

- Sales
- Accounting
- IT

All three departments might use the same physical switching infrastructure.

But with VLANs, they can be logically separated into different networks.

For example:

```text
VLAN 10 → Sales
VLAN 20 → Accounting
VLAN 30 → IT
```

The devices can still use the same physical infrastructure while being treated as separate network segments.

This can improve organization and security because administrators can control how traffic moves between the different VLANs.

For example, Sales might be allowed to access the Internet but prevented from directly communicating with Accounting.

That made VLANs feel much more relevant to cybersecurity.

Network security isn't only about detecting attacks.

Sometimes security comes from **how the network itself is designed**.

---
# Connecting Everything Together

This lesson helped me see networking as more than just devices exchanging packets.

There are multiple layers of control involved.

A simplified way I'm starting to visualize it is:

```text
Internet
   ↓
Router
   ↓
Firewall
   ↓
Switch
   ↓
VLANs
   ↓
Devices
```

And each concept has a different role.

**Port forwarding** determines where certain incoming traffic should be forwarded.

**Firewalls** determine which traffic should be allowed or denied.

**VPNs** can create secure tunnels between networks.

**Routers** connect different networks and forward packets.

**Switches** connect devices within networks and forward frames.

**VLANs** allow networks to be logically separated.

Instead of seeing these as isolated technologies, I'm beginning to see them as pieces of the same system.

---

# What I Learned

This lesson introduced me to several concepts that made my understanding of networks much broader.

I learned that:

- **Port forwarding** can make services inside a private network accessible through a public address.
- **Firewalls** control whether network traffic is permitted or denied.
- **Stateful firewalls** consider the state of connections.
- **Stateless firewalls** evaluate packets against predefined rules.
- **VPNs** create secure tunnels between devices or networks.
- **Routers** connect different networks and forward packets.
- **Switches** connect devices and forward frames.
- **Layer 2 switches** primarily use MAC addresses.
- **Layer 3 switches** can also perform routing using IP addresses.
- **VLANs** allow networks to be logically separated even when sharing physical infrastructure.

But once again, the biggest thing I took away wasn't simply memorizing what each technology does.

It was understanding **how they fit together**.

---
# Conclusion

This lesson expanded my understanding of networking beyond packets and protocols.

I started with a simple question:

**What controls where network traffic can go?**

That question led me through port forwarding, firewalls, VPNs, routers, switches, and VLANs.

Each concept gave me another piece of the bigger picture.

I'm beginning to see that a secure network isn't created by one technology.

It's built through layers of design, segmentation, access control, routing, and secure communication.

And the more I learn, the more I realize that cybersecurity isn't just about defending individual computers.

It's also about understanding **the network that connects everything together.**

---
# Next Rabbit Hole

I've learned how networks can be connected, segmented, and protected.

Now I want to look deeper into **how we can make the communication itself more secure**.

My next rabbit hole is:

**Network Secure Protocols.**

I want to understand how protocols such as **SSH, HTTPS, TLS, and other secure networking protocols** protect information as it travels across a network.

---
### Resources

- TryHackMe — [Extending Your Network](https://tryhackme.com/room/extendingyournetwork)
- [Youtube](https://www.youtube.com/watch?v=uMkjvpux70I)
