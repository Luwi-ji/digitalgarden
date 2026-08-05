---
{"dg-publish":true,"permalink":"/cybersecurity/blogs/005-how-do-devices-find-each-other/","created":"2026-07-24T11:02:49.455+08:00","updated":"2026-08-05T17:54:38.364+08:00","dg-note-properties":{"created":"2026-07-24 22:22:18","updated":"2026-07-24 22:48:34","status":"Draft","tags":[]}}
---

After learning about [[Cybersecurity/Terms/IP address\|IP addresses]] in my [first journal](obsidian://open?vault=Luwiji's%20Vault&file=Cybersecurity%2FBlogs%2F001%20-%20Networking%20is%20Everywhere), I thought I finally understood how devices communicate. But along the way, it created a question:

**If my laptop knows another device's IP address, how does it actually find that device on the network?**

An IP address tells me **where** a device is. But computers don't plug into IP addresses.

They communicate through their physical network hardware, and every network interface has its own [[Cybersecurity/Terms/MAC Address\|MAC Address]].

So somehow, a device has to translate an IP address into a MAC address before communication can begin.

That's exactly the problem today's lesson answered.

---
## Meet ARP

The solution is something called the **[[005 - ARP\|Address Resolution Protocol (ARP)]]**.

From what I've understood so far, ARP acts like a translator between two identifiers that I learned about in my [first networking journal](obsidian://open?vault=Luwiji's%20Vault&file=Cybersecurity%2FBlogs%2F001%20-%20Networking%20is%20Everywhere).

- An [[Cybersecurity/Terms/IP address\|IP Address]] tells a device **where** another device is.
- A [[Cybersecurity/Terms/MAC Address\|MAC Address]] identifies the actual network hardware.

**ARP simply connects those two pieces of information together.**

Without it, devices would know the destination's IP address but wouldn't know which physical device should receive the data.

---
## How Does ARP Know?

The part I found interesting is that ARP doesn't magically know every MAC address on the network. Instead, it asks. 

Imagine walking into a classroom looking for someone you've never met. You probably wouldn't ask every person individually. Instead, you'd ask the entire room,

**"Does anyone know where John is?"**

That's almost exactly what ARP does.

When a device needs the MAC address that belongs to an IP address, it sends an **[[Cybersecurity/Terms/ARP Request\|ARP Request]]** to every device on the local network. The request is basically asking:

**"Who owns this IP address?"**

Every device receives the request. Most ignore it and only the device that actually owns that IP address responds.

It sends back an **[[Cybersecurity/Terms/ARP Reply\|ARP Reply]]** containing its MAC address. **Once the requesting device receives the reply, communication can finally begin** as we can see in the diagram below:

![Pasted image 20260724092614.png](/img/user/Archive/Pasted%20image%2020260724092614.png)


---
## The ARP Cache

One thing I wondered while reading this was:

**Does every device have to ask this question every single time?**

Thankfully, no. Devices keep a small record called an **[[Cybersecurity/Terms/ARP cache\|ARP Cache]]**.

I like thinking of it as a contact list so instead of asking the network the same question repeatedly, a computer remembers the MAC addresses it has already discovered.

The next time it wants to communicate with the same device, it can simply check its cache first and that makes communication much faster.

---
## Conclusion

 I learned that an IP address alone isn't enough. Inside a local network, computers eventually need to know the physical hardware they're talking to.

That's where ARP quietly does its job.

It's one of those technologies I had never heard of before, yet it's happening constantly whenever devices communicate on the same network.
## Next Rabbit Hole

Today's lesson answered how devices discover each other. But to our next stop, we'll answer a question immediately followed after learning about it:

**If every device needs an IP address before ARP can even work... who gives that IP address in the first place?**

Looks like the next stop is about [DHCP](obsidian://open?vault=Luwiji's%20Vault&file=Cybersecurity%2FBlogs%2F006%20-%20How%20Do%20Devices%20Get%20an%20IP%20Address)-[[Cybersecurity/Blogs/006 - How Do Devices Get an IP Address\|006 - How Do Devices Get an IP Address]].

---
Reference
- [Intro to Lan](https://tryhackme.com/room/introtolan) 