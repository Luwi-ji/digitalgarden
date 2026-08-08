---
{"dg-publish":true,"permalink":"/cybersecurity/blogs/012-learning-how-linux-really-works/","created":"2026-08-08T16:48:26.285+08:00","updated":"2026-08-08T20:29:25.437+08:00","dg-note-properties":{"created":"2026-07-24 22:22:18","updated":"2026-07-24 22:48:34","status":"Draft","tags":[]}}
---

## From Using Linux to Connecting to Linux

In my previous journal, I learned the basic Linux commands by interacting directly with a Linux machine.

This time, I learned something much more interesting:

**I don't actually have to sit in front of a Linux computer to use it.**

Instead, I can securely connect to another Linux machine over a network using **SSH (Secure Shell)**.

This is one of the most common ways system administrators, cloud engineers, and cybersecurity professionals manage remote servers.

---
# What is SSH?

**SSH (Secure Shell)** is a protocol that allows me to securely access another computer over a network.

Instead of physically using another machine, I can open my terminal and remotely execute commands as if I were sitting in front of it.

The important part is that everything sent between my computer and the remote machine is **encrypted**.

That means usernames, passwords, commands, and other data can't easily be read by someone monitoring the network.

To connect through SSH, I only need three things:

- the `ssh` command
- the username
- the IP address of the remote machine

For example:

```
ssh tryhackme@MACHINE_IP
```

After entering the correct password, every command I type is executed on the remote Linux machine instead of my own computer.

It felt pretty cool the first time I logged into another system entirely from the terminal.

---
# Learning That Commands Have Superpowers

One thing I quickly realized is that Linux commands rarely have only one behavior.

Most commands become much more useful when combined with **flags** (or switches).

For example, I already knew that:

```
ls
```

lists the contents of a directory.

But adding the `-a` flag changes its behavior:

```
ls -a
```

Now it also shows **hidden files**, which normally begin with a dot (`.`).

This made me realize that learning Linux isn't just memorizing commands—it's also learning how to modify them using different options.

---
# When I Don't Know a Command...

I also learned something that every Linux user relies on:

The documentation is already built into the operating system.

There are two easy ways to discover what a command can do.

Using:

```
ls --help
```

shows a quick summary of available options.

For more detailed documentation, Linux provides **manual pages**, commonly called **man pages**.

For example:

```
man ls
```

opens the complete manual for the `ls` command, including its syntax, description, and available flags.

Instead of searching Google every time I forget a command, I can often find the answer directly from the terminal.

---
# Working with Files and Folders

In the previous journal, I learned how to navigate the filesystem.

This time, I learned how to actually manage it.

Linux provides commands for creating, copying, moving, deleting, and inspecting files.

|Command|Purpose|
|---|---|
|`touch`|Create a new file|
|`mkdir`|Create a directory|
|`cp`|Copy files or folders|
|`mv`|Move or rename files|
|`rm`|Delete files or folders|
|`file`|Identify a file's type|

For example:

```
touch notes.txt
```

creates an empty file.

```
mkdir projects
```

creates a new directory.

If I want to duplicate a file:

```
cp notes.txt backup.txt
```

If I want to rename or move it:

```
mv backup.txt archive.txt
```

To remove files:

```
rm notes.txt
```

Or remove an entire directory:

```
rm -R projects
```

I also discovered the `file` command.

Unlike Windows, Linux doesn't rely only on file extensions.

Running:

```
file notes.txt
```

tells me what kind of file it actually is, regardless of its filename.

---
# Understanding Linux Permissions

One of the biggest concepts I learned in this room is that Linux is built around permissions.

Not every user is allowed to access every file.

Using:

```
ls -l
```

shows a permission string that looks something like:

```
-rwxr-xr--
```

At first this looked confusing, but it's actually divided into three groups:

- Owner
- Group
- Others

Each group can have three permissions:

- **Read (r)**
- **Write (w)**
- **Execute (x)**

This system allows Linux administrators to control exactly who can access or modify files.

---
# Numeric Permissions Finally Made Sense

I also learned that permissions can be written using numbers.

Each permission has a value:

|Permission|Value|
|---|---|
|Read|4|
|Write|2|
|Execute|1|

Adding these together creates the numeric permission.

For example:

|Symbolic|Numeric|
|---|---|
|`rwx`|7|
|`rw-`|6|
|`r-x`|5|
|`r--`|4|

This explains why permissions like these are so common:

|Permission|Meaning|
|---|---|
|`777`|Everyone has full access|
|`755`|Owner has full access; others can read and execute|
|`644`|Owner can read and write; everyone else can only read|
|`700`|Only the owner has access|

These values are frequently used with the `chmod` command to change file permissions.

For example:

```
chmod 755 script.sh
```

Now the numbers finally make sense instead of looking random.

---
# Users and Groups

Another thing I learned is that Linux separates permissions using both **users** and **groups**.

A file may belong to one user while still allowing an entire group of users to access it.

This provides much finer control over who can read, modify, or execute files.

If I need to switch to another user account, Linux provides the `su` command.

For example:

```
su user2
```

Or, to start a full login session for that user:

```
su -l user2
```

This switches me into the new user's environment, including their home directory and environment settings.

---
# Important Linux Directories

I also became familiar with several directories that appear on almost every Linux system.

|Directory|Purpose|
|---|---|
|`/etc`|Stores system configuration files such as `passwd`, `shadow`, and `sudoers`.|
|`/var`|Stores frequently changing data like logs, caches, and databases.|
|`/root`|Home directory of the root user.|
|`/tmp`|Temporary files that are usually removed after a reboot.|

Knowing these directories helps me understand where Linux stores important information and where I might need to look during system administration or cybersecurity investigations.

---
## Conclusion

This lesson made Linux feel much less like a collection of commands and more like a complete operating system.

I learned how to connect to remote machines using SSH, discover command options through flags and manual pages, manage files, understand permissions, and recognize some of the most important directories in Linux.

One thing that stood out to me is how much control Linux gives its users. Almost everything—from file access to system configuration—can be managed directly from the terminal.

It's easy to see why Linux is the preferred operating system for servers, cloud environments, and cybersecurity professionals.

---
## Next Rabbit Hole

Learning how to connect to a Linux machine is only the beginning.

Now that I know how to navigate the filesystem, manage files, understand permissions, and work with remote machines through SSH, I'm curious about what it's actually like to **manage** a Linux system.

These are the day-to-day skills that system administrators, cloud engineers, and cybersecurity professionals use to keep Linux systems running.

I'm excited to move beyond simply **using Linux** and start learning how to **manage it**.

See you in the next learning journal.

---
### Reference
- TryHackMe — [_Linux Fundamentals Part 2_](https://tryhackme.com/room/linuxfundamentalspart2)
- [Youtube](https://www.youtube.com/watch?v=7Zt2Mp2IeBI&t=653s)
