---
{"dg-publish":true,"permalink":"/cybersecurity/blogs/011-my-first-steps-into-linux/","created":"2026-08-07T19:38:22.023+08:00","updated":"2026-08-08T16:47:35.812+08:00","dg-note-properties":{"created":"2026-07-24 22:22:18","updated":"2026-07-24 22:48:34","status":"Draft","tags":[]}}
---

## So... Why Do Cybersecurity Professionals Use Linux?

As I continue learning cybersecurity, one operating system keeps showing up everywhere: **Linux**.

At first, I thought Linux was just another alternative to Windows or macOS.

But I quickly learned that it's much more than that.

Linux powers a huge part of the technology we use every day, including
- websites
- cloud servers
- Android phones
- smart devices
- supercomputers
- enterprise infrastructure
- even traffic systems and industrial machines

Most cybersecurity tools are also built to run on Linux, which is one of the reasons it's considered an essential skill for anyone entering the field.

This journal marks my first time learning how to actually interact with a Linux machine.

---
## What is Linux?

Linux is an **operating system**, just like Windows and macOS.

An operating system is responsible for managing a computer's hardware and software while providing a way for users to interact with the machine.

Unlike Windows, Linux is **open-source**, meaning anyone can view, modify, and improve its source code.

Because of this, there are many different versions called **distributions** or **distros** that are designed for different purposes.

Some of the most popular ones include:
- Ubuntu
- Debian
- Kali Linux
- Fedora
- Arch Linux

For this learning journey, I'm using **Ubuntu**, one of the most beginner-friendly Linux distributions.

---
## The Terminal Looks Scary... Until You Start Using It
One thing that immediately stood out to me is that Linux doesn't always rely on a graphical interface like Windows.

Instead, many Linux systems are controlled through the **Terminal**.

At first glance, it honestly looked intimidating.

```
tryhackme@linux:~$
```

But after using it for a while, I realized something.

The terminal isn't complicated because it's difficult.

It's unfamiliar because I'm used to clicking buttons instead of typing commands.

Once I learned a few basic commands, it started making much more sense.

---
## My First Linux Commands

The very first commands I learned were surprisingly simple.
### echo

The `echo` command simply prints text to the terminal.

```
echo "Hello World"
```

Output:

```
Hello World
```

It's commonly used for displaying messages or testing commands.

---
### whoami

The `whoami` command tells me which user I'm currently logged in as.

```
whoami
```

Example output:

```
ubuntu
```

This becomes useful when working on systems with multiple users or checking what permissions I currently have.

---
## Navigating the Linux Filesystem

Knowing how to move around the filesystem is one of the first practical Linux skills.

I learned four essential commands.

|Command|Purpose|
|---|---|
|`ls`|Lists files and folders|
|`cd`|Changes directories|
|`pwd`|Shows my current location|
|`cat`|Displays the contents of a file|

Instead of clicking folders like I normally would in Windows, Linux expects me to navigate using these commands.

For example:

```
ls
```

shows everything inside my current directory.

To move into another folder:

```
cd Documents
```

If I ever forget where I am:

```
pwd
```

prints my current path.

And if I want to read a text file:

```
cat notes.txt
```

outputs its contents directly in the terminal.

These commands seem small, but they're the foundation of working in Linux.

---
## Finding Files Without Opening Every Folder

Imagine trying to locate one file among hundreds of directories.

Instead of manually checking every folder, Linux provides a command called **find**.

For example:

```
find -name passwords.txt
```

searches for a file named **passwords.txt**.

I can even search for every text file using a wildcard:

```
find -name "*.txt"
```

This saves a huge amount of time when working on large systems.

---
## Searching Inside Files with grep

Finding a file is useful.

Finding a specific word inside hundreds of files is even better.

That's where `grep` comes in.

For example:

```
grep "password" notes.txt
```

searches for the word **password** inside the file.

If I want to search across an entire directory and all its subdirectories, I can use recursive mode:

```
grep -R "PRETTY_NAME" /etc/
```

This command searches through multiple files and tells me exactly where the matching text appears.

I can already see why this command is heavily used in cybersecurity, especially when searching logs and configuration files.

---
## Making Commands More Powerful with Shell Operators

I also learned that Linux commands can be combined using **shell operators**.

These make the command line much more powerful.
### `&`

Runs a command in the background so I can continue using the terminal.

---
### `&&`

Runs another command only if the first one succeeds.

For example:

```
command1 && command2
```

This is useful when multiple commands depend on each other.

---
### `>`

Redirects the output of a command into a file.

```
echo "Hello" > notes.txt
```

If the file already exists, its contents are replaced.

---
### `>>`

Appends new content instead of replacing the existing file.

```
echo "Another line" >> notes.txt
```

This simply adds the new line to the end of the file.

---
## Conclusion

Before this lesson, Linux felt like a completely different world.

Now I realize that most of what I'm doing is simply learning a new way to interact with a computer.

Instead of clicking through folders, I use commands.

Instead of opening files with a text editor, I can read them directly from the terminal.

Instead of manually searching through directories, Linux provides tools like `find` and `grep` that can do it in seconds.

I'm beginning to understand why cybersecurity professionals spend so much time in the terminal.

It's faster, more efficient, and gives far more control over the system.

---
## Next Rabbit Hole

Now that I can move around a Linux system and use its basic commands, I'm curious about what happens beyond my own computer.

Those concepts are essential for both system administration and cybersecurity, and they'll help me understand why certain users can access some files while others cannot.

See you in the next learning journal. 👋

---
### Reference
- TryHackMe — [_Linux Fundamentals Part 1_](https://tryhackme.com/room/linuxfundamentalspart1)
