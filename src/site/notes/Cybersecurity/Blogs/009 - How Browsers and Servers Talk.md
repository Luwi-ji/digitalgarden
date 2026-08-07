---
{"dg-publish":true,"permalink":"/cybersecurity/blogs/009-how-browsers-and-servers-talk/","created":"2026-08-06T23:30:14.857+08:00","updated":"2026-08-07T16:00:36.590+08:00","dg-note-properties":{"created":"2026-07-24 22:22:18","updated":"2026-07-24 22:48:34","status":"Draft","tags":[]}}
---

In my previous journal, I learned that every time I visit a website, my browser sends an **HTTP Request**, and the server replies with an **HTTP Response**.

But I started wondering something.

**How does the server know what I actually want to do?** Am I simply viewing a page, creating an account, updating my profile, or deleting something?

And once the server processes my request, **how does it tell me whether it succeeded or failed?**

That's exactly what HTTP Methods and Status Codes are for.

---
## HTTP Methods

An **HTTP Method** tells the web server **what action the client wants to perform**.

I like thinking of it as the **verb** of an HTTP request. It tells the server what I'm trying to do with a resource.

Although HTTP supports many methods, these are the ones I'll probably encounter most often.

### GET

The **GET** method asks the server to send information back.

Whenever I open a webpage, search on Google, or view a YouTube video, my browser is usually sending a GET request.

The important thing to remember is that **GET only retrieves data**. It doesn't modify anything on the server.

---
### POST

The **POST** method is used when I want to send data to the server.

For example, when I register a new account, submit a login form, or leave a comment, my browser sends a POST request containing the information I've entered.

Unlike GET, POST usually creates something new.

---
### PUT

The **PUT** method updates an existing resource.

If I edit my profile picture or change my username, my browser may send a PUT request to replace the old information with the new one.

---
### DELETE

As the name suggests, **DELETE** removes a resource from the server.

For example, deleting a post, removing a comment, or permanently deleting an account may involve a DELETE request.

---
## HTTP Status Codes

After the server receives my request, it needs to let my browser know what happened.

That's where **HTTP Status Codes** come in.

Every HTTP response begins with a status code that tells the browser whether the request succeeded or if something went wrong.

For example:

```
HTTP/1.1 200 OK
```

The **200** is the status code, while **OK** is a short description.

Instead of memorizing every code, I found it easier to understand them by their categories.

---
### 1xx — Informational

These codes tell the client that the request has been received and the communication can continue.

They're not very common in everyday browsing.

---
### 2xx — Success

These indicate that everything worked as expected.

The most common one is:

- **200 OK** — The request completed successfully.

Another useful one is:

- **201 Created** — A new resource was successfully created, such as a new user account or blog post.

---
### 3xx — Redirection

Sometimes a webpage has moved to another location.

Instead of showing an error, the server tells the browser where to go next.

Common examples include:

- **301 Moved Permanently** — The page has permanently moved.
- **302 Found** — The page has temporarily moved.

---
### 4xx — Client Errors

These errors usually mean the problem came from the client, not the server.

Some of the most common ones are:

- **400 Bad Request** — The request was malformed.
- **401 Unauthorized** — Authentication is required.
- **403 Forbidden** — I don't have permission to access the resource.
- **404 Not Found** — The requested page doesn't exist.
- **405 Method Not Allowed** — I used the wrong HTTP method.

The **404** status code is probably the one I've seen the most while browsing the web.

---
### 5xx — Server Errors

Unlike 4xx errors, these usually mean something went wrong on the server itself.

Some common examples are:

- **500 Internal Server Error** — The server encountered an unexpected problem.
- **503 Service Unavailable** — The server is temporarily unavailable, often because it's overloaded or under maintenance.

---
## Why This Matters

Before learning this, I thought websites simply loaded or failed to load.

Now I understand there's actually a conversation happening between my browser and the server.

The browser first tells the server **what it wants to do** using an HTTP Method.

The server then replies with a **Status Code** explaining whether that request succeeded, failed, or needs further action.

Every webpage I visit is constantly exchanging these requests and responses in the background.

---
## Conclusion

HTTP Methods and Status Codes are two of the building blocks of web communication.

Methods describe **the action I'm requesting**, while Status Codes describe **the result of that request**.

Understanding both makes it much easier to read browser developer tools, understand APIs, and troubleshoot web applications.

---
## Next Rabbit Hole

Now I understand **what** my browser is asking the server to do and **how** the server responds.

But HTTP requests contain much more than just a method and a status code.

They also include extra information called **headers**, and websites use **cookies** to remember who I am between requests.

That's what I'll be exploring in the next learning journal.

See you there. 👋

---
### Reference
- TryHackMe — [HTTP in Detail]([https://tryhackme.com/module/how-the-web-works](https://tryhackme.com/module/how-the-web-works))
