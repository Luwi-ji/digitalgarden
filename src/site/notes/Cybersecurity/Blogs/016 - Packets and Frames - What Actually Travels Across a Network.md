---
{"dg-publish":true,"permalink":"/cybersecurity/blogs/016-packets-and-frames-what-actually-travels-across-a-network/","created":"2026-08-11T20:51:15.879+08:00","updated":"2026-08-13T21:04:36.134+08:00","dg-note-properties":{"created":"2026-07-24 22:22:18","updated":"2026-07-24 22:48:34","status":"Draft","tags":[]}}
---

After learning about the OSI Model, I finally had a framework for understanding how network communication is divided into different layers.

But that left me with another question.

**What actually moves through those layers?**

I understood that devices communicate with each other, but I hadn't really thought about what the data itself looks like while traveling across a network.

That led me to my next rabbit hole: **packets and frames**.

---
# What Are Packets and Frames?

Packets and frames are pieces of data used during network communication.

They're closely related, but they exist at different layers of the OSI Model.

A **packet** operates at **Layer 3, the Network Layer**. It contains information such as IP addresses and the data being transported.

A **frame** operates at **Layer 2, the Data Link Layer**. It encapsulates the packet and adds information such as MAC addresses.

At first, I found this distinction confusing.

Then I went back to encapsulation which is something I learned from the OSI Model.

As data moves down the networking stack, each layer adds information that helps the data reach its destination.

It's like mailing a letter.

The actual letter represents the data I want to send. The envelope helps carry that letter to another location.

In networking, the packet is like the letter, while the frame provides the additional information needed to move that packet across a local network.

This made the relationship between Layer 2 and Layer 3 much easier for me to understand.

---
# Data Doesn't Travel as One Giant Message

One thing that stood out to me was that data isn't normally sent as one huge piece.

Instead, it's broken down into smaller pieces.

For example, when I download an image from a website, the entire image isn't simply sent to my computer as one giant block.

The data is divided into smaller pieces that can travel across the network and eventually be reconstructed by the receiving device.

This makes communication more manageable and efficient.

It also helped me understand why the word **packet** comes up so often when learning about networking.

I'm not just sending "a file."

I'm sending pieces of information that are being transported across a network according to a set of rules.

And those rules matter.

With billions of devices communicating across networks, everyone needs to follow common standards. Otherwise, devices wouldn't know how to interpret the information they're receiving.

---
# What's Inside a Packet?

Packets aren't just random pieces of data.

They contain **headers** that provide additional information about how the data should be handled.

Some of the fields I encountered include:

|Header|What I Understand|
|---|---|
|**Time to Live (TTL)**|Limits how long a packet can remain in a network|
|**Checksum**|Helps detect whether data has been corrupted|
|**Source Address**|Identifies where the packet came from|
|**Destination Address**|Identifies where the packet is going|

The **source and destination IP addresses** were particularly interesting to me.

When I previously learned about IP addresses, I understood them mostly as addresses assigned to devices.

Now I'm starting to see their purpose inside actual network communication.

A packet needs to know:

**Where did I come from?**

**Where am I going?**

That information helps routers make forwarding decisions and allows communication to happen between different networks.

---
# TCP: Establishing a Conversation

The next part of the lesson brought me back to something I encountered in the OSI Model:

**TCP.**

TCP, or Transmission Control Protocol, is connection-oriented.

Before data is exchanged, TCP establishes a connection between the two devices.

This happens through something called the **Three-Way Handshake**.

The three main steps are:

**SYN → SYN/ACK → ACK**

I started thinking about it like two devices introducing themselves before having a conversation.

The client essentially says:

 "Can we establish a connection?"

The server responds:

 "Yes, I received your request, and I'm ready."

The client then acknowledges:

"Got it. We're connected."

Only after this process can the communication proceed.

---
# Understanding SYN, SYN/ACK, and ACK

The Three-Way Handshake became much easier to understand when I looked at what each message actually does.

### 1. SYN

The client sends a **SYN** packet to initiate the connection.

It also includes an initial sequence number.

### 2. SYN/ACK

The server responds with **SYN/ACK**.

It acknowledges the client's sequence information and provides its own initial sequence number.

### 3. ACK

The client sends an **ACK** to acknowledge the server.

Now the connection is established.

This process also introduces an important concept:

**sequence numbers.**

TCP uses sequence numbers to help keep transmitted data organized and in the correct order.

That matters because data doesn't necessarily travel across a network in one perfectly organized stream.

TCP needs mechanisms to make sure the receiving system can reconstruct the data correctly.

This was one of the moments where packets started feeling much more real to me.

They're not just "pieces of data."

They contain information that allows computers to manage communication between each other.

---
# TCP Flags

I also encountered several TCP flags that help determine how a connection should behave.

Some of the important ones are:

- **SYN** — initiates a connection

- **ACK** — acknowledges received information

- **FIN** — cleanly closes a connection

- **RST** — abruptly terminates a connection
    
The **FIN** flag was particularly interesting because it showed me that ending a connection is also part of the communication process.

A TCP connection doesn't just magically disappear.

There are mechanisms for properly closing it and acknowledging that closure.

On the other hand, **RST** can be used when a connection needs to be terminated abruptly.

This made me realize that networking involves a lot more coordination than I initially thought.

---
# TCP Doesn't Just Start a Conversation as It also Ends One

After learning how TCP establishes a connection, I also learned how it closes one.

A device can send a **FIN** packet to indicate that it wants to close the connection.

The other device acknowledges it and can also indicate that it wants to close its side of the connection.

Eventually, both sides acknowledge the closure.

This made sense when I thought about TCP as an actual conversation.

There's a process for saying:

**"Let's start talking."**

There's a process for saying:

**"I received what you sent."**

And there's even a process for saying:

**"We're finished."**

---
# UDP: A Different Approach

After spending time with TCP, I moved on to **UDP — User Datagram Protocol**.

UDP takes a completely different approach.

Unlike TCP, UDP is **connectionless**.

There is no Three-Way Handshake before data is sent.

There is also no built-in guarantee that the data will arrive or arrive in order.

At first, I wondered why anyone would want this.

Wouldn't reliability always be better?

But this brought me back to what I learned previously.

Not every application needs the same kind of communication.

Sometimes minimizing overhead and avoiding connection setup is more useful than having all the reliability mechanisms TCP provides.

UDP can be useful for things like:

- video streaming

- voice communication

- situations where losing some data is preferable to waiting for retransmission


The biggest difference became clearer to me:
### TCP

**Reliability and ordered delivery with data integrity**

### UDP

**Simplicity and low overhead**

Neither protocol is universally "better."

They are designed for different situations.

---
# Ports: Where Does the Data Go?

Then I reached another concept that immediately connected several things together:

**Ports.**

A device can have many applications and services communicating over the network at the same time.

So knowing the destination IP address isn't always enough.

The device also needs to know **which application or service should receive the data**.

That's where ports come in.

Ports are numerical values ranging from **0 to 65535**.

I found the harbor analogy from the lesson helpful here.

Imagine a large harbor.

Ships arrive at the harbor, but they don't all dock at the same place.

Different ports are designed for different purposes.

Networking works similarly.

An IP address can help identify the destination device, while a port helps identify the service or application that should handle the communication.

That gave me a much better mental model:

**IP address → Which device?**

**Port → Which service?**

---
# Common Ports I Encountered

Some of the common ports I learned about were:

|Protocol|Port|Purpose|
|---|--:|---|
|**FTP**|21|File transfer|
|**SSH**|22|Secure remote access|
|**HTTP**|80|Web communication|
|**HTTPS**|443|Secure web communication|
|**SMB**|445|File and resource sharing|
|**RDP**|3389|Remote desktop access|

Seeing these ports together was useful because I've encountered some of these protocols before without fully understanding the role of the port.

For example, when I see:

**192.168.1.100:22**

I can now interpret that as communication directed toward the device at `192.168.1.100` through port `22`, which is commonly associated with SSH.

This also started making cybersecurity tools like **Nmap** make more sense to me.

When security professionals scan a system for open ports, they're essentially investigating what network services may be accessible on that device.

I'm not just seeing numbers anymore.

I'm beginning to understand what those numbers represent.

---
# Connecting Everything Together

This lesson helped me connect several concepts that I had previously learned separately.

Before this, I had encountered:

- MAC addresses
    
- IP addresses
    
- TCP
    
- UDP
    
- ports
    
- switches
    
- routers
    
- DNS
    
- DHCP
    
- the OSI Model
    

But I didn't fully understand how they fit together during actual communication.

Now I can start visualizing the process.

Data begins at an application.

It moves down through the networking layers.

The Transport Layer can add TCP or UDP information.

The Network Layer adds IP addressing.

The Data Link Layer encapsulates the packet into a frame and adds local network information such as MAC addresses.

Then the data is transmitted across the physical network.

On the receiving side, the process happens in reverse.

The receiving device removes the encapsulating information layer by layer until the original data reaches the appropriate application.

**Encapsulation sends the data down the stack.**

**Decapsulation brings it back up.**

That connection made the OSI Model feel much more practical than it did before.

---
# What I Learned

This lesson taught me that network communication isn't just about sending data from one computer to another.

There's a lot happening underneath.

I learned that:

- **Packets** operate at Layer 3 and contain network-level information.
    
- **Frames** operate at Layer 2 and encapsulate packets for local network delivery.
    
- **TCP** establishes connections and provides reliable, ordered communication.
    
- **UDP** provides connectionless communication with less overhead.
    
- **TCP flags** help control the state of a connection.
    
- **Sequence numbers** help TCP organize data.
    
- **Ports** help identify the service or application involved in network communication.
    
- Common services use standard ports such as **22 for SSH, 80 for HTTP, and 443 for HTTPS**.
    

But once again, the biggest thing I learned wasn't a definition.

It was a better mental model.

---
# Conclusion

The OSI Model gave me a way to understand **where network functions happen**.

Packets and Frames gave me a better idea of **what is actually being carried through those layers**.

And learning about TCP, UDP, and ports helped me understand how devices establish communication and direct data toward the services that need it.

I'm slowly moving from memorizing networking concepts to actually building a mental model of how communication works.

And that feels like an important step in my cybersecurity journey.

Because before I can properly analyze a network, I need to understand how that network communicates in the first place.

---
# Next Rabbit Hole

Now that I understand packets, frames, TCP, UDP, and ports, I want to move one step closer to understanding how networks are actually controlled and protected.

My next rabbit hole is:

**Port Forwarding, Firewalls, VPNs, and LAN Networking Devices.**

I'm starting to move from understanding **how data travels** to understanding **how networks control where that data can go**.

---
### Resources

- TryHackMe — [Packets and Frames](https://tryhackme.com/room/packetsframes)
- [YouTube](https://www.youtube.com/watch?v=vzcLrE0SfiQ)
