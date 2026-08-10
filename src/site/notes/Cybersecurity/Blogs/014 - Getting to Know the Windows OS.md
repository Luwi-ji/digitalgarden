---
{"dg-publish":true,"permalink":"/cybersecurity/blogs/014-getting-to-know-the-windows-os/","created":"2026-08-09T16:59:25.000+08:00","updated":"2026-08-10T12:04:33.292+08:00","dg-note-properties":{"created":"2026-07-24 22:22:18","updated":"2026-07-24 22:48:34","status":"Draft","tags":[]}}
---

After spending the last few journals learning Linux, I realized that understanding cybersecurity means I can't stay on just one operating system.

Linux is everywhere in servers, cloud infrastructure, and security tooling.

But **Windows is just as important**, especially in corporate environments.

So this is where I start learning the other side of the equation.

---
## From Linux to Windows

My Linux journey started with the terminal.

Now I'm switching environments and learning how Windows is structured, how users and permissions work, where important files live, and how Windows manages the programs running on a machine.

Windows has been around since **1985** and became dominant in both home and corporate environments.

Because of how widely it is used, Windows has also been a major target for hackers and malware writers.

Looking at its history, Microsoft went through several major versions:

- Windows XP
- Windows Vista
- Windows 7
- Windows 8/8.1
- Windows 10
- Windows 11

Some versions were much more successful than others.

Windows Vista, for example, wasn't received particularly well, while Windows 8 had a relatively short lifespan.

Microsoft eventually moved toward Windows 10 and then Windows 11 for desktop users.

The important lesson for me isn't really memorizing every Windows version.

It's understanding that **the operating system constantly evolves**, and security professionals need to understand the environment they're actually working with.

---
# The Windows Desktop

The first thing I encountered was the part of Windows I'm already familiar with:

the **Graphical User Interface (GUI)**.

Unlike the Linux terminal-heavy experience I've been learning, Windows gives me a visual environment where I can interact with applications, files, settings, and system components.

After logging in, the main components I need to recognize are:

1. Desktop
2. Start Menu
3. Search
4. Task View
5. Taskbar
6. Toolbars
7. Notification Area

Most of these probably seem obvious to someone who has used Windows for years.

But I'm looking at them differently now.

Instead of just asking **"How do I use Windows?"**, I'm starting to ask:

**"What does this part of the operating system actually do?"**

That mindset is important for cybersecurity.

---
# The Desktop

The Desktop is basically the workspace where I can place shortcuts to programs, files, and folders.

I can also right-click it to access options for things like:

- creating new files or folders
- arranging icons
- changing display settings
- changing the wallpaper
- customizing themes and colors

Nothing here felt particularly complicated.

But it reminded me of something I learned from Linux:

**the graphical interface is just another way of interacting with the underlying operating system.**

---
# The Start Menu

The Start Menu is one of the main ways I access applications and system utilities.

It provides shortcuts to things such as:

- user account settings
- Documents
- Pictures
- Settings
- Power options
- installed applications

Applications can also be pinned to the Start Menu for easier access.

There's also a search function that makes it easier to find applications, settings, and other parts of the operating system.

Coming from Linux, this is one of the biggest differences I've noticed so far.

Linux often makes me think:

```
"What command do I need?"
```

Windows often makes me think:

```
"Where in the interface can I find this?"
```

But underneath that interface, Windows still has plenty of command-line and administrative tools.

I'll eventually get to those.

---
# The Taskbar

The Taskbar shows the applications, folders, and files that are currently open.

It can also contain pinned applications for quick access.

One feature I found useful is the preview that appears when hovering over an application's icon.

This becomes especially useful when multiple windows of the same application are open.

It's a small feature, but it shows how Windows is designed around managing multiple applications visually.

---
# The Notification Area

The Notification Area sits in the bottom-right corner of the Windows desktop.

This is where I can typically find things like:

- the date and time
- network status
- volume
- other system notifications

It might seem like a minor part of Windows, but from a security perspective, system status information can be useful.

For example, the network icon immediately gives me an indication of the machine's connectivity.

---
# Understanding the Windows File System

This is where things started getting more interesting for me.

Modern Windows systems commonly use **NTFS (New Technology File System**).

Before NTFS, Windows used filesystems such as:

- FAT16
- FAT32
- HPFS

FAT-based filesystems are still commonly encountered in removable storage such as USB drives and memory cards.

But NTFS became much more capable for Windows systems.

---
# Why NTFS Matters

NTFS is a **journaling filesystem**.

One of the interesting things about journaling is that the filesystem maintains information that can help it recover from certain failures.

NTFS also provides features such as:

- support for files larger than 4 GB
- file and folder permissions
- compression
- encryption through **Encrypting File System (EFS)**

The permissions aspect immediately caught my attention.

This is something I already encountered in Linux.

Linux has permissions like:

```
rwxr-xr-x
```

Windows approaches the problem differently, but the underlying idea is similar:

**Not everyone should automatically have access to everything.**

---
# NTFS Permissions

NTFS allows permissions to be assigned to files and folders.

Some of the permissions I encountered are:

- **Full Control**
- **Modify**
- **Read & Execute**
- **List Folder Contents**
- **Read**
- **Write**

To view these permissions, I can:

**Right-click → Properties → Security**

From there, Windows shows the users and groups that have permissions for that particular file or folder.

This was another moment where I could connect Windows to what I learned in Linux.

In Linux, I learned about:

```
Owner
Group
Others
```

In Windows, permissions are also closely connected to **users and groups**.

The implementation is different, but the security principle is familiar:

**access should be controlled based on identity and permissions.**

---
# Alternate Data Streams

This was probably one of the more interesting concepts in this lesson.

NTFS supports something called **Alternate Data Streams (ADS)**.

Normally, when I think about a file, I imagine it containing one set of data.

But NTFS allows a file to contain additional streams of data.

Windows Explorer doesn't normally show these alternate streams to the user.

PowerShell and other tools can be used to inspect them.

From a cybersecurity perspective, this becomes interesting because ADS has been used by malware authors to hide information.

But it's important not to assume that ADS automatically means something malicious.

There are legitimate uses too.

For example, Windows can store information associated with downloaded files in an alternate data stream.

This was my first real glimpse into something that looks completely normal from a user's perspective but can have a deeper security significance underneath.

---
# The Windows Directory

Another important location is:

```
C:\Windows
```

This is traditionally where the Windows operating system is installed.

However, the Windows directory doesn't necessarily have to be located on the C: drive.

This is where **environment variables** become useful.

For example:

```
%windir%
```

represents the location of the Windows directory.

Environment variables store information about the operating system environment, such as system paths and temporary directories.

This reminded me of Linux again.

Linux also has environment variables that provide information about the current environment.

---
# System32

Inside the Windows directory is one of the most well-known folders:

```
C:\Windows\System32
```

System32 contains important files and tools that are critical to Windows.

This is also where many of the tools I'll encounter throughout the Windows Fundamentals series are located.

Because of how important this directory is, interacting with its contents requires caution.

Accidentally modifying or deleting critical system files can cause serious problems for the operating system.

So I definitely don't want to treat System32 like an ordinary folder.

---
# Users, Accounts, and Permissions

This section immediately reminded me of Linux.

Windows typically has two local account types:

### Administrator

An Administrator can perform system-level actions such as:

- adding users
- deleting users
- modifying groups
- changing system settings

### Standard User

A Standard User has more limited permissions and generally can't make system-level changes without elevated privileges.

This distinction is important for security.

If every user automatically had unrestricted control over the operating system, compromising a single user account could potentially give an attacker much more control.

---
# Windows User Profiles

When a user account is created and logs into a Windows system, Windows creates a user profile.

These profiles are stored under:

```
C:\Users
```

For example:

```
C:\Users\Max
```

A user profile contains folders such as:

```
Desktop
Documents
Downloads
Music
Pictures
```

This is another concept that felt familiar after learning Linux.

Linux has user home directories such as:

```
/home/user
```

Windows uses:

```
C:\Users\user
```

Different structure, similar purpose.

---
# Local Users and Groups

Windows also provides a management tool called:

```
lusrmgr.msc
```

This opens **Local Users and Groups**.

Inside, there are two major sections:

- Users
- Groups

Groups are particularly important because permissions can be assigned to groups rather than individual users.

A user can belong to multiple groups and inherit the permissions associated with those groups.

This is something I'll need to understand deeply as I move toward enterprise cybersecurity.

---
# User Account Control

This was one of the most important security concepts in this lesson.

It's called **User Account Control**, or **UAC**.

The problem UAC tries to solve is pretty simple:

What happens if an administrator is using the computer, but a program doesn't actually need administrator privileges?

Running everything with elevated privileges would increase the damage malware could potentially cause.

So Windows introduced UAC to prevent administrators from automatically operating with elevated privileges all the time.

When an action requires higher privileges, Windows can display a prompt asking for confirmation or administrator credentials.

For example, a program might display a small shield icon indicating that elevated privileges are required.

The user then encounters a UAC prompt before the action is allowed to continue.

This is another example of the **principle of least privilege** in action:

Give users and programs only the privileges they need to perform their task.

That principle is going to be extremely important as I continue learning cybersecurity.

---
# Settings vs Control Panel

Windows has two major places for changing system configurations:

- **Settings**
- **Control Panel**

Settings is the newer interface and is increasingly the primary place for changing Windows configurations.

Control Panel has existed much longer and still contains many administrative options.

Sometimes I can start changing something through Settings and end up inside Control Panel.

At first that seemed a little messy.

But it also showed me something important:

**Windows has accumulated a lot of functionality over decades.**

Not everything has been moved into one unified interface yet.

When I'm unsure where a setting is located, Windows Search can usually help me find it.

---
# Task Manager

The final major topic of this lesson was **Task Manager**.

I've used Task Manager before.

Usually, I think of it as:

"That thing I open when Chrome freezes."

But there's much more to it.

Task Manager provides information about applications and processes currently running on the system.

It can also show resource usage such as:

- CPU
- RAM
- and other system activity

I can open it by right-clicking the Taskbar and selecting Task Manager.

The default view is relatively simple, but selecting **More details** reveals much more information about the system.

And this immediately connects to something I learned in **Linux Fundamentals Part 3**.

In Linux, I learned about:

```
ps
top
```

and how they can be used to inspect running processes.

Windows has Task Manager for a similar purpose.

Different operating system.

Different tools.

**Same fundamental question:**

 **What's currently running on this machine?**

That's a question I'll probably be asking a lot as I continue into cybersecurity.

---
# What I Learned

This lesson was supposed to be a basic introduction to Windows, but I found a lot of connections to what I already learned from Linux.

I learned about:
- the Windows GUI
- the Desktop
- Start Menu
- Taskbar
- Notification Area
- NTFS
- NTFS permissions
- Alternate Data Streams
- environment variables
- `C:\Windows`
- `System32`
- user accounts
- user profiles
- groups
- UAC
- Settings
- Control Panel
- Task Manager

But more importantly, I started seeing **the same security concepts appearing across different operating systems**.

Linux has users and groups.

Windows has users and groups.

Linux has file permissions.

Windows has NTFS permissions.

Linux has processes.

Windows has processes.

Linux has system directories.

Windows has system directories.

The commands and interfaces are different, but the underlying concepts aren't completely foreign.

---
# Conclusion

One thing I realized from this lesson is that learning cybersecurity isn't really about memorizing a collection of tools.

It's about understanding **how systems work**.

If I only memorize that `ls` lists files or that Task Manager shows processes, I might be able to follow a tutorial.

But if I understand why permissions exist, how users interact with those permissions, why processes need to be monitored, and why administrative privileges should be controlled, I can start reasoning about security problems myself.

That's the kind of understanding I'm trying to build. Linux gave me my first foundation.

Now Windows is giving me another perspective. And I have a feeling the two are going to keep connecting as I go deeper into cybersecurity.

---
# Next Rabbit Hole

I've now had my first look at how Windows is **structured** from its filesystem and permissions to users, groups, processes, and administrative controls.

What I found interesting is that the same security concepts I learned in Linux like **users, permissions, processes, and privilege** is also existing in Windows, just implemented differently.

But cybersecurity isn't only about understanding individual operating systems.

I also need to understand **how these systems communicate with each other**.

So, for my next step, I'm moving again from operating systems into **networking fundamentals**, starting with the **OSI Model**.

See you in the next learning journal. 👋

---

### Reference

- TryHackMe — [**Windows Fundamentals 1**](https://tryhackme.com/room/windowsfundamentals1xbx)
