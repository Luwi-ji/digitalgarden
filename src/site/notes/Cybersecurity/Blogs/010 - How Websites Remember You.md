---
{"dg-publish":true,"permalink":"/cybersecurity/blogs/010-how-websites-remember-you/","created":"2026-08-06T23:35:39.242+08:00","updated":"2026-08-14T09:19:40.473+08:00","dg-note-properties":{"created":"2026-07-24 22:22:18","updated":"2026-07-24 22:48:34","status":"Draft","tags":[]}}
---

In my previous journal, I learned that browsers communicate with web servers using **HTTP Requests** and **HTTP Responses**.

But as I looked at an HTTP request more closely, I noticed something interesting.

Besides the request itself, there were extra pieces of information attached to it.

Things like:
- Host
- User-Agent
- Content-Type
- Cookies

That made me wonder:

**What are these extra pieces of information for?**

This lesson answered that question by introducing me to **HTTP Headers** and **Cookies**.

---
## What are HTTP Headers?

HTTP headers are **additional pieces of information** that are sent together with every HTTP request and response.

Think of them like the label attached to a package before it's shipped.

The package contains the actual content, while the label tells the receiver useful information about it.

In the same way, headers don't contain the webpage itself. Instead, they provide context that helps the browser and the server understand each other.

---
## Request Headers

Request headers are sent **from my browser to the web server**.

They give the server more information about who is making the request and how the response should be delivered.

Some of the most common request headers are:
### Host

The **Host** header tells the server which website I'm trying to access.

This is important because one server can host multiple websites. Without the Host header, the server wouldn't know which one I actually wanted.

---
### User-Agent

The **User-Agent** identifies the browser and operating system making the request.

For example, it may tell the server that I'm using Chrome on Windows or Safari on an iPhone.

Some websites use this information to display pages differently depending on the device or browser I'm using.

---
### Content-Length

Whenever I send information to a server such as submitting a form, the **Content-Length** header tells the server how much data to expect.

This helps the server know whether it has received the complete request.

---
### Accept-Encoding

The **Accept-Encoding** header tells the server which compression methods my browser supports.

If both my browser and the server support compression, the webpage can be sent in a smaller size, making it load faster.

---
### Cookie

Whenever I've previously visited a website, my browser may already have cookies stored for it.

The **Cookie** header sends those saved cookies back to the server so it can recognize me.

---
## Response Headers

Response headers are sent **from the server back to my browser**.

They tell my browser how to handle the response it has received.

Some common response headers include:

### Set-Cookie

The **Set-Cookie** header tells my browser to save a new cookie.

That cookie will be stored locally and automatically sent back with future requests to the same website.

---
### Cache-Control

The **Cache-Control** header tells my browser how long it can keep a copy of the webpage before asking the server for a new version.

This helps websites load faster because the browser doesn't always have to download everything again.

---
### Content-Type

The **Content-Type** header tells the browser what kind of data it is receiving.

For example, the response might contain:
- HTML
- CSS
- JavaScript
- Images
- Videos
- PDFs

Knowing the content type allows the browser to display the data correctly.

---
### Content-Encoding

If the server compressed the response before sending it, the **Content-Encoding** header tells the browser which compression method was used so it knows how to decompress it.

---
## What are Cookies?

One thing I always heard people talk about was website cookies.

I used to think they were just annoying pop-ups asking for permission.

Now I understand that **cookies are simply small pieces of data stored by my browser**.

Whenever a server sends a **Set-Cookie** header, my browser saves that information locally.

The next time I visit the same website, my browser automatically sends that cookie back with the request.

---
## Why Do Websites Use Cookies?

HTTP is a **stateless protocol**.

That means every request is treated as if it's completely new.

Without cookies, websites wouldn't remember that I've already logged in or even that I've visited before.

Cookies solve this problem by giving the browser a way to identify itself on future requests.

That's why websites can:
- keep me logged in
- remember my shopping cart
- save my language preference
- remember dark mode settings
- personalize my experience

Most of the time, cookies don't store sensitive information like my password.

Instead, they usually store a unique identifier or token that the server recognizes.

---
## Why This Matters

Before learning this, I assumed websites somehow "remembered" me automatically.

Now I know that every request includes extra information through **headers**, and cookies allow websites to recognize returning users even though HTTP itself doesn't remember previous requests.

It's a simple idea, but it's one of the reasons modern web applications work the way they do.

---
## Conclusion

HTTP Headers and Cookies add important context to web communication.

Headers tell browsers and servers how to handle requests and responses, while cookies give websites a way to remember users across multiple visits.

Understanding these concepts helped me see that browsing the web is much more than simply loading pages as it's a constant exchange of information happening behind the scenes.

---

## Next Rabbit Hole

So far, I've learned how devices communicate on a network and how browsers interact with web servers.

The next step is to leave the web behind for a while and explore the operating system that powers most servers around the world.

That's where I'll begin learning **Linux Fundamentals**.

See you in the next learning journal. 👋

---
### Reference
- TryHackMe — [HTTP in Detail]([https://tryhackme.com/module/how-the-web-works](https://tryhackme.com/module/how-the-web-works))
