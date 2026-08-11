---
{"dg-publish":true,"permalink":"/cybersecurity/blogs/015-understanding-how-machines-communicate/","created":"2026-08-10T12:05:44.773+08:00","updated":"2026-08-11T20:50:18.838+08:00","dg-note-properties":{"created":"2026-07-24 22:22:18","updated":"2026-07-24 22:48:34","status":"Draft","tags":[]}}
---

After learning the fundamentals of Linux and Windows, I started noticing something.

Understanding an operating system is only part of understanding cybersecurity.

Computers don't exist in isolation.

They constantly communicate with other computers, servers, routers, and devices across networks.

So my next step was to understand **what actually happens when data travels from one device to another**.

That's where I encountered the **OSI Model**.

---
# What is the OSI Model?

The **Open Systems Interconnection (OSI) Model** is a framework used to describe how networked devices communicate and how data is sent, received, and interpreted.

The model divides networking into **seven different layers**.

Each layer has its own responsibilities.

The interesting part is that data doesn't simply travel directly from one application to another.

As data moves through the layers, different information is added to it.

This process is called **encapsulation**.

The seven layers are:

|Layer|Name|
|---|---|
|7|Application|
|6|Presentation|
|5|Session|
|4|Transport|
|3|Network|
|2|Data Link|
|1|Physical|

At first, seven layers seemed like a lot to remember.

But instead of trying to memorize the names immediately, I wanted to understand what each layer actually does.

---
# Layer 1 — Physical

The **Physical Layer** is the lowest layer of the OSI Model.

This is where networking becomes physical.

It deals with the actual hardware and signals used to transmit data.

For example:

- Ethernet cables
- electrical signals
- physical network connections
- binary data represented through physical signals

At this layer, information is ultimately represented as **1s and 0s**.

This was probably the easiest layer for me to visualize.

If two computers are physically connected through a network cable, something has to physically carry the data between them.

That's Layer 1.

---

# Layer 2 — Data Link

Moving one level up brings me to the **Data Link Layer**.

This layer focuses on physical addressing.

One important concept here is the **MAC address**.

A **MAC (Media Access Control) address** is associated with a device's network interface.

A computer's **NIC (Network Interface Card)** has a MAC address that can be used to identify the device at the local network level.

This is different from an IP address.

That's an important distinction:

**MAC address → physical/local network addressing**

**IP address → network-level addressing**

The Data Link Layer also prepares data into a format suitable for transmission across the network.

What I found interesting is that this is where networking starts becoming more identifiable to me.

I'm no longer just dealing with physical cables.

Now I'm dealing with **how devices are identified on the network**.

---

# Layer 3 — Network

Then comes the **Network Layer**.

This is where **IP addresses and routing** become important.

If I want to send data to another device, the network needs to determine where that data should go.

That's where routing comes in.

Routers operate at Layer 3 because they make forwarding decisions based on IP addresses.

For example:

```
192.168.1.100
```

is an example of an IP address.

The network layer is responsible for determining an appropriate path for data to travel.

Some routing protocols mentioned in this lesson include:

- **OSPF** — Open Shortest Path First
- **RIP** — Routing Information Protocol

The route can be influenced by factors such as:

- path length
- reliability
- connection speed

This is where I started seeing the bigger picture.

A computer isn't simply sending data randomly into the network.

There are mechanisms that determine **where that data needs to go and how it should get there**.

---

# Layer 4 — Transport

Layer 4 is where things became much more interesting.

The **Transport Layer** is responsible for transporting data between devices, and two protocols I encountered here are:

- **TCP**
- **UDP**

These two protocols approach communication very differently.

---

## TCP — Reliability First

**TCP (Transmission Control Protocol)** is designed around reliability.

It establishes a connection between devices and performs additional processing to make sure data is delivered correctly.

It also provides error checking and helps ensure that data can be reconstructed in the correct order.

This makes TCP useful for situations where accuracy matters.

For example:

- file transfers
- web browsing
- email

If I'm downloading a file, I don't want half of it to arrive and the other half to disappear.

I need the complete data.

That's where TCP's reliability becomes valuable.

The downside is that this additional reliability comes with overhead.

More processing means TCP can be slower than UDP.

---

# UDP — Speed and Simplicity

**UDP (User Datagram Protocol)** takes a very different approach.

Instead of prioritizing guaranteed delivery, UDP focuses on speed and simplicity.

There is no guarantee that every piece of data will arrive.

There is also no guarantee that everything will arrive in the same way TCP handles it.

At first, that sounded like a terrible design.

Why would anyone want unreliable communication?

But then I realized that **not every application needs perfect delivery**.

UDP can be useful when speed matters more than recovering every lost piece of data.

Examples from the lesson include things such as:

- device discovery
- DHCP
- ARP
- video streaming

For something like video streaming, losing a small amount of data may be preferable to stopping everything while waiting for retransmission.

That made the difference between TCP and UDP much easier for me to understand.

### TCP

**"Make sure it gets there correctly."**

### UDP

**"Get it there quickly."**

It's obviously more complicated than that in practice, but this mental model helped me understand the basic difference.

---

# Layer 5 — Session

Above the Transport Layer is the **Session Layer**.

This layer is responsible for establishing and maintaining communication sessions between devices.

When a connection is established, a session is created.

The session remains active while the communication continues.

The Session Layer can also handle things such as:

- maintaining sessions
- closing inactive or lost connections
- creating checkpoints

The checkpoint concept was particularly interesting.

If some data is lost, checkpoints can allow communication to resume from a certain point rather than starting completely over.

So this layer is essentially concerned with **managing the conversation between systems**.

---

# Layer 6 — Presentation

Then we reach the **Presentation Layer**.

This layer is responsible for making sure data is represented in a format that the receiving system can understand.

Different applications can represent and handle data differently.

The Presentation Layer acts as a kind of translator between the application and the underlying network communication.

It also deals with things such as data formatting and, according to the lesson, security features such as encryption.

The important idea I took away from this layer is:

**The data needs to be understandable to both sides.**

It isn't enough to successfully deliver the data.

The receiving system also needs to know what that data means.

---

# Layer 7 — Application

Finally, we reach **Layer 7, the Application Layer**.

This is probably the layer I interact with most directly as a user.

The Application Layer contains protocols and rules that applications use to communicate.

Examples include:

- web browsers
- email applications
- file transfer software
- DNS

One example that stood out to me was **DNS (Domain Name System)**.

When I type a website address into my browser, DNS helps translate that domain name into an IP address.

So something as simple as visiting a website actually involves networking concepts operating underneath the application I'm interacting with.

---

# The Seven Layers Finally Started Connecting

At first, the OSI Model felt like seven unrelated concepts.

But once I looked at them together, I started seeing a flow.

```
7 — Application
6 — Presentation
5 — Session
4 — Transport
3 — Network
2 — Data Link
1 — Physical
```

Each layer has a different responsibility.

And together, they provide a structured way of understanding network communication.

I also started connecting this to what I've already learned.

I previously learned about:

- **ARP**
- **DHCP**
- **DNS**
- IP addresses
- MAC addresses
- switches
- networking

Now I have a framework for understanding where many of these concepts fit.

For example:

**MAC addresses → Layer 2**

**IP addresses and routing → Layer 3**

**TCP/UDP → Layer 4**

**DNS → Layer 7**

That made the OSI Model feel much less like something I simply have to memorize.

It's becoming a way to **organize what I already know**.

---

# Why Does the OSI Model Matter in Cybersecurity?

This is where the lesson became especially relevant to me.

Cybersecurity isn't just about running security tools.

When something goes wrong on a network, I need to understand **where the problem is happening**.

Is the problem physical?

Is it related to MAC addresses?

Is routing failing?

Is a TCP connection behaving unexpectedly?

Is an application communicating with the wrong service?

The OSI Model gives me a way to break those problems down.

Instead of looking at networking as one giant complicated system, I can ask:

 **Which layer am I dealing with?**

That question can make troubleshooting and security analysis much easier.

---

# What I Learned

This lesson introduced me to the seven layers of the OSI Model:

|Layer|Name|What I Understand|
|---|---|---|
|7|Application|Network services and application-level communication|
|6|Presentation|Data formatting and translation|
|5|Session|Establishing and managing sessions|
|4|Transport|TCP and UDP communication|
|3|Network|IP addressing and routing|
|2|Data Link|MAC addressing and local network communication|
|1|Physical|Hardware, cables, and physical signals|

But the biggest thing I learned isn't the seven names.

It's the idea that **network communication can be broken down into layers**.

That gives me a framework for understanding what's happening underneath the applications I use every day.

---

# Conclusion

Before this lesson, I knew networking concepts like IP addresses, MAC addresses, DNS, DHCP, and ARP individually.

But I didn't have a clear mental model connecting them together.

The OSI Model started giving me that structure.

I can now look at network communication and think about it layer by layer:

**Physical connection → MAC addressing → IP routing → transport → sessions → data representation → applications.**

And that's a much better way of thinking about networking than simply memorizing definitions.

I'm beginning to realize that cybersecurity requires me to understand what happens **underneath the tools**.

If I want to understand network attacks, troubleshoot connectivity, analyze traffic, or eventually work with tools like Wireshark and Nmap, I need to understand the underlying communication first.

The OSI Model is giving me that foundation.

---
# Next Rabbit Hole

Now that I have a better understanding of the OSI Model and how network communication is divided into layers, my next step is to understand **what actually happens to the data as it moves through those layers**.

That leads me to **packets and frames** which are the actual structures used to carry data across a network.

---
### Reference
- TryHackMe - [OSI Model](https://tryhackme.com/room/osimodelzi)
- [Youtube](https://www.youtube.com/watch?v=hWIktHvNjeM&t=139s)
