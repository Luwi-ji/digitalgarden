---
{"dg-publish":true,"permalink":"/cybersecurity/blogs/013-linux-beyond-basics/","created":"2026-08-08T20:31:51.673+08:00","updated":"2026-08-09T16:59:04.088+08:00","dg-note-properties":{"created":"2026-07-24 22:22:18","updated":"2026-07-24 22:48:34","status":"Draft","tags":[]}}
---

In the first two Linux Fundamentals rooms, I learned how to navigate the Linux filesystem, work with files, understand permissions, and even connect to remote machines using SSH.

This time, the focus shifted from simply **using Linux** to actually **managing a Linux system**.

I learned how to edit files directly from the terminal, transfer files between computers, manage running processes, automate repetitive tasks, install software through package managers, and understand where Linux stores important system logs.

These are the kinds of skills that system administrators, cloud engineers, and cybersecurity professionals rely on every day.

---
# Editing Files Without Leaving the Terminal

Up until now, whenever I wanted to create a text file, I relied on commands like `echo` together with redirection operators (`>` and `>>`).

That works for simple files, but it quickly becomes inconvenient when working with larger files or multiple lines of text.

This lesson introduced me to **terminal text editors**, which make editing files much more practical.
## Nano

The first editor I learned was **Nano**.

Opening or creating a file is as simple as:

```
nano myfile.txt
```

Once Nano opens, I can immediately begin typing.

Unlike graphical editors, everything happens directly inside the terminal.

Some features I found useful include:

- Searching for text
- Copying and pasting
- Jumping to a specific line
- Viewing my current line number

Most commands are accessed using keyboard shortcuts that begin with the **Ctrl** key.

For example:

```
Ctrl + X
```

exits Nano.

At first, editing files entirely from the terminal felt unusual, but Nano is surprisingly beginner-friendly.

---
## Vim

The lesson also introduced **Vim**, another terminal text editor.

Unlike Nano, Vim has a much steeper learning curve, but it's incredibly powerful.

Some of its advantages include:

- Highly customizable shortcuts
- Syntax highlighting for programming
- Available on almost every Linux system
- Extremely efficient once mastered

I don't know Vim yet, but I can already see why many developers and cybersecurity professionals prefer it.

It's definitely something I'd like to learn later.

---
# Downloading Files with `wget`

Another useful utility I learned is `wget`.

This command downloads files directly from the internet without opening a web browser.

For example:

```
wget https://example.com/file.txt
```

Instead of manually downloading files through a browser, Linux can retrieve them directly from the terminal.

I immediately realized how useful this would be during penetration testing or system administration, where downloading scripts or tools from remote servers is a common task.

---
# Securely Transferring Files with `scp`

Downloading files is useful, but sometimes I need to move files between two computers.

That's where **SCP (Secure Copy Protocol)** comes in.

Unlike the regular `cp` command, `scp` copies files between machines using SSH.

Because it uses SSH, the transfer is both **encrypted** and **authenticated**.

Uploading a file looks like this:

```
scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt
```

Downloading a file works in reverse:

```
scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt
```

This showed me that SSH isn't only for remote command execution as it also provides a secure way to move files across systems.

---
# Turning My Computer into a Web Server

One of the coolest things I learned in this room was that Python can instantly create a web server.

Using:

```
python3 -m http.server
```

starts a lightweight HTTP server that shares every file inside the current directory.

Another machine can then download those files using:

```
wget http://IP_ADDRESS:8000/file
```

I thought this was a clever trick.

Instead of installing complicated software just to share files, Python already includes everything needed to create a simple web server.

It's easy to imagine using this during labs or penetration testing to transfer tools between machines.

---
# Understanding Linux Processes

One concept that helped me understand Linux better is that **everything running on the system is a process**.

Every program has its own **Process ID (PID)** assigned by the kernel.

Linux provides several commands to monitor these processes.

Using:

```
ps
```

shows the processes running under my current session.

To view every running process on the system, including those owned by other users, I can use:

```
ps aux
```

For a live view of system activity:

```
top
```

displays running processes in real time along with CPU and memory usage.

Instead of seeing Linux as a black box, I'm beginning to understand that it's simply managing hundreds of individual processes simultaneously.

---
# Managing Running Processes

Sometimes programs stop responding or need to be terminated.

Linux provides the `kill` command for this.

For example:

```
kill 1337
```

sends a signal to the process with PID **1337**.

I also learned that not all kill signals behave the same way.

Some common signals include:

- **SIGTERM** — asks the process to shut down cleanly
- **SIGKILL** — immediately terminates the process
- **SIGSTOP** — pauses the process

This helped me realize that process management isn't simply "closing programs."

Linux gives administrators fine-grained control over how applications are stopped.

---
# How Linux Starts Programs

One topic I hadn't considered before was how programs actually start after the computer boots.

Linux uses **systemd**, one of the first processes started during startup.

Every application launched afterward becomes a **child process** of systemd.

In other words, systemd acts as the manager responsible for starting and supervising services running on the operating system.

Understanding this made Linux feel much more organized.

Programs don't simply appear—they're managed through a structured hierarchy.

---
# Managing Services with `systemctl`

Since systemd controls services, Linux provides the `systemctl` command to interact with it.

Some of the most common commands are:

Start a service:

```
systemctl start apache2
```

Stop a service:

```
systemctl stop apache2
```

Enable a service to start automatically:

```
systemctl enable apache2
```

Disable automatic startup:

```
systemctl disable apache2
```

Check a service's status:

```
systemctl status apache2
```

This is one of those commands that I know I'll continue using as I learn more about Linux servers.

---
# Background and Foreground Processes

Another feature I found interesting is that Linux allows commands to run in either the foreground or the background.

Normally, commands run in the foreground.

For example:

```
echo "Hello"
```

finishes before I can continue typing.

However, adding:

```
&
```

runs the command in the background.

For example:

```
long_script.sh &
```

This allows me to continue using the terminal while the command keeps running.

I also learned that pressing:

```
Ctrl + Z
```

temporarily suspends a running process.

To bring it back into focus:

```
fg
```

returns it to the foreground.

This is incredibly useful for long-running scripts or large file transfers.

---
# Automating Tasks with Cron

One of my favorite concepts in this room was **automation**.

Instead of manually repeating tasks every day, Linux can schedule them automatically using **cron jobs**.

Cron reads instructions stored inside a **crontab** file.

Each scheduled task includes six fields:

- Minute
- Hour
- Day of Month
- Month
- Day of Week
- Command

For example:

```
0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/
```

backs up a directory every twelve hours.

I also learned that an asterisk (`*`) acts as a wildcard, meaning "every possible value."

Editing cron jobs is done with:

```
crontab -e
```

I can already imagine using cron to automate backups, cleanup scripts, monitoring tasks, or even scheduled security scans.

---
# Installing Software with APT

Unlike Windows, Linux usually installs software through a **package manager**.

Ubuntu uses **APT**.

Instead of searching websites for installers, Linux downloads trusted software from repositories.

Some useful commands include:

Update package information:

```
sudo apt update
```

Install software:

```
sudo apt install package-name
```

Remove software:

```
sudo apt remove package-name
```

I also learned that developers sign their software using **GPG keys**, allowing Linux to verify that downloaded packages are authentic and haven't been modified.

This makes software installation both easier and more secure.

---
# Understanding Linux System Logs

The final topic introduced one of the most important parts of Linux for both administrators and cybersecurity professionals:

**system logs**.

Most logs are stored inside:

```
/var/log
```

Different services maintain their own logs.

For example:

- Apache web server logs
- Firewall logs (UFW)
- Fail2Ban logs
- Authentication logs

These logs record what happens on the system.

For web servers, logs may contain every incoming request.

Authentication logs record login attempts.

Firewall logs show blocked network traffic.

During troubleshooting, incident response, or forensic investigations, these logs become one of the most valuable sources of information.

This helped me realize that logs tell the story of everything happening on a Linux machine.

---
# Conclusion

This lesson made Linux feel much more like a complete operating system rather than just a collection of terminal commands.

I learned how to edit files directly from the terminal using Nano, securely transfer files with SCP, download files using wget, create a simple web server with Python, monitor and manage running processes, understand how Linux starts programs through systemd, control services using `systemctl`, automate repetitive tasks with cron, install software through APT, and inspect system logs.

What stood out to me most is how everything in Linux is designed to work together.

Small tools, each with a specific purpose, combine to create a flexible and powerful operating system.

The more I learn, the more I appreciate why Linux powers so many servers, cloud platforms, and cybersecurity tools.

I'm starting to feel more comfortable working entirely from the terminal, and that's a skill I know will continue to grow as I move deeper into cybersecurity.

---
# Next Rabbit Hole

After spending three learning journals understanding Linux from navigating the terminal to managing processes, services, packages, and system logs, I realized something important:

**Linux isn't the only operating system cybersecurity professionals need to know.**

While Linux dominates servers and penetration testing environments, many organizations around the world still rely heavily on **Windows** for their desktops, enterprise networks, and Active Directory environments.

To become a well-rounded cybersecurity professional, I need to understand both sides.

That's why my next step is diving into **Windows Fundamentals**.

Understanding both Linux and Windows will give me a much stronger foundation before moving into networking, privilege escalation, and eventually penetration testing.

See you in the next learning journal.

---
## References

- TryHackMe — [_Linux Fundamentals Part 3_](https://tryhackme.com/room/linuxfundamentalspart3)
- [YouTube](https://www.youtube.com/watch?v=bwgaZCb2ft8) 
