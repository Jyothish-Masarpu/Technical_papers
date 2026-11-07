# Comprehensive Linux Command Line Interface (CLI) Master Cheatsheet

Welcome to your ultimate Linux CLI reference guide and revision manual! Designed specifically for beginners and learners, this cheat sheet covers everything from fundamental shell concepts and directory navigation to advanced text processing, process management, and all 20 comprehensive review questions with detailed, step-by-step explanations.

---

## Table of Contents
1. [Introduction to Computers & Shells](#1-introduction-to-computers--shells)
2. [The Unix Philosophy](#2-the-unix-philosophy)
3. [Directory Structure & File Hierarchy](#3-directory-structure--file-hierarchy)
4. [File & Directory Management (Practice Drill 1)](#4-file--directory-management-practice-drill-1)
5. [File Permissions & Octal/Binary Conversions](#5-file-permissions--octalbinary-conversions)
6. [Pipes, Redirection & Text Processing (Practice Drill 2)](#6-pipes-redirection--text-processing-practice-drill-2)
7. [Processes & Port Management](#7-processes--port-management)
8. [Software Management & Networking (Misc)](#8-software-management--networking-misc)
9. [Terminal Control Codes & Shortcuts](#9-terminal-control-codes--shortcuts)
10. [Complete Review Questions & Solutions (Q1 - Q20)](#10-complete-review-questions--solutions-q1---q20)

---

## 1. Introduction to Computers & Shells

Computers understand binary code (zeros and ones). To bridge the gap between human language and computer hardware, operating systems use a **shell**—a command language interpreter that accepts human-readable commands and translates them for the system kernel.

### Common Linux Shells
* **BASH (Bourne-Again SHell):** The most popular default open-source shell in Linux.
* **CSH (C SHell):** Syntax closely mirrors the C programming language.
* **KSH (Korn SHell):** Developed at AT&T Bell Labs; served as the basis for POSIX shell standards.
* **TCSH:** An enhanced, compatible version of the Berkeley UNIX C shell.

### Essential Shell Inspection Commands
```bash
# Display all available shells supported on your platform
cat /etc/shells

# Check your current active shell name
echo $SHELL

# Check current shell process identification numbers
ps $$
ps -p $$
```

---

## 2. The Unix Philosophy

Developed by leading Unix architects, these core design principles also govern Linux systems:
* **Do one thing and do it well:** Write modular programs that handle a single task exceptionally well.
* **Everything is a file:** Simplify hardware and software access by treating devices and streams as files.
* **Small is beautiful & KISS:** Keep It Simple, Stupid.
* **Store data in flat text files:** Text is a universal, easily backup-able, and portable interface.
* **Chain programs together:** Use pipes (`|`) to combine small utilities into powerful workflows.

---

## 3. Directory Structure & File Hierarchy

Unlike Windows (which uses drive letters like `C:\`), Linux organizes everything under a single absolute root directory (`/`).

* `/` : **Root Directory** - The absolute top of the system file tree.
* `/bin` : **Essential User Binaries** - Core commands required in single-user mode (e.g., `bash`, `cat`).
* `/etc` : **Configuration Files** - System-wide configuration files editable by text editors.
* `/home` : **Home Folders** - Personal directories for each user (e.g., `/home/jyothish`).
* `/opt` : **Optional Packages** - Third-party or proprietary software installation directories.
* `/root` : **Root Home Directory** - Home folder specifically for the superuser (root).
* `/sbin` : **System Administration Binaries** - Critical binaries reserved for system administrators.
* `/tmp` : **Temporary Files** - Volatile storage wiped automatically upon reboot.
* `/usr` : **User Binaries & Read-Only Data** - Non-essential user applications and architecture-independent libraries.
* `/var` : **Variable Data Files** - Writable counter-part to `/usr` storing log files (`/var/log`) and queues.

---

## 4. File & Directory Management (Practice Drill 1)

### Creating Directory Structures & Files
```bash
# Create nested directories using the parent (-p) flag
mkdir -p hello/five/six/seven hello/one/two/three/four

# Create empty files using touch
touch hello/five/six/c.txt
touch hello/five/six/seven/error.log
touch hello/one/a.txt
touch hello/one/b.txt
touch hello/one/two/d.txt
touch hello/one/two/three/e.txt
touch hello/one/two/three/four/access.log
```

### Modifying, Moving, and Deleting
```bash
# Delete all files ending with .log extension recursively
find hello -name "*.log" -type f -delete

# Add text content to a file (overwrite with >, append with >>)
echo "Unix is a family of multitasking operating systems..." > hello/one/a.txt

# Delete a directory and all its contents recursively
rm -r hello/five

# Rename a directory (mv handles both renaming and moving)
mv hello/one hello/uno

# Move a file into a subdirectory
mv hello/uno/a.txt hello/uno/two/
```

---

## 5. File Permissions & Octal/Binary Conversions

### Understanding `ls -l` Permissions
Example permission string: `-rw-r--r--`
* Character 1: File type (`-` for file, `d` for directory).
* Characters 2–4: **User (Owner)** permissions (`rw-`).
* Characters 5–7: **Group** permissions (`r--`).
* Characters 8–10: **Others** permissions (`r--`).

### Binary & Octal Math Values
* **Read (r)** = Binary `100` = Decimal `4`
* **Write (w)** = Binary `010` = Decimal `2`
* **Execute (x)** = Binary `001` = Decimal `1`

```bash
# View long file details including permission strings
ls -l d1/a.txt

# Change permissions using octal notation (755 = rwxr-xr-x)
chmod 755 d1/a.txt

# Recursively apply permissions to a directory and all contents
chmod -R 755 d2
```

---

## 6. Pipes, Redirection & Text Processing (Practice Drill 2)

### Downloading & Inspecting Text Files
```bash
# Download a remote book file using curl
curl -O https://raw.githubusercontent.com/bobdeng/owlreader/master/ERead/assets/books/Harry%20Potter%20and%20the%20Goblet%20of%20Fire.txt

# Print the first 3 lines of a file
head -n 3 Harry%20Potter%20and%20the%20Goblet%20of%20Fire.txt

# Print the last 10 lines of a file
tail -n 10 Harry%20Potter%20and%20the%20Goblet%20of%20Fire.txt

# Print the last 30 lines of a file
tail -n 30 Harry%20Potter%20and%20the%20Goblet%20of%20Fire.txt
```

### Advanced Text Parsing (`grep`, `sed`, `find`)
```bash
# Count exact word occurrences case-insensitively (-o prints each match on a new line)
grep -o -i "Harry" Harry%20Potter%20and%20the%20Goblet%20of%20Fire.txt | wc -l

# Print specific line ranges using stream editor (sed)
sed -n '100,200p' Harry%20Potter%20and%20the%20Goblet%20of%20Fire.txt

# Search for files or directories case-insensitively across the current path
find . -iname "*java*"

# Count unique words in a text file
grep -oE '[a-zA-Z]+' Harry%20Potter%20and%20the%20Goblet%20of%20Fire.txt | tr '[:upper:]' '[:lower:]' | sort | uniq | wc -l
```

---

## 7. Processes & Port Management

```bash
# List all running processes in full format
ps aux

# Find process ID (PID) of a specific application (bracket trick hides grep)
ps -ef | grep -i '[f]irefox'

# Terminate process gracefully or forcefully
pkill firefox
kill $(lsof -t -i:8000)

# Complex pipeline to find and force-kill a process (e.g. firefox)
ps aux | grep firefox | grep -v grep | awk '{print $2}' | xargs kill -9

# List top processes by CPU or Memory usage
ps aux --sort=-%cpu | head -n 4
ps aux --sort=-%mem | head -n 4

# Start local test servers
python3 -m http.server 8000
sudo python3 -m http.server 90   # Ports < 1024 require sudo privileges

# Inspect active network listening sockets and ports
ss -tuln
lsof -i :5432
```

---

## 8. Software Management & Networking (Misc)

```bash
# Install and remove software packages (Ubuntu/Debian apt)
sudo apt update && sudo apt install htop vim nginx
sudo apt remove nginx

# Network diagnostics & IP addresses
ip a
nslookup google.com
ping -c 4 google.com

# Locate binary paths on the system
which node
which code
```

---

## 9. Terminal Control Codes & Shortcuts

* `Ctrl + C` : Instantly terminate the currently running foreground process.
* `Ctrl + Z` : Suspend/pause a foreground process and send it to the background.
* `Ctrl + D` : Send an End-of-File (EOF) signal; closes shells or terminals.
* `Ctrl + R` : Interactive reverse-search through previously executed command history.
* `Tab` : Auto-complete file names, folder paths, and command names.
* `Up / Down Arrows` : Navigate back and forth through your command history.

---

## 10. Complete Review Questions & Solutions (Q1 - Q20)

| No. | Review Task / Question | Exact Command Solution | Beginner Explanation |
| :---: | :--- | :--- | :--- |
| **1** | Go into your home directory | `cd ~` | The tilde (`~`) is a universal shortcut for your user home folder (`/home/username`). |
| **2** | Create a directory `d1` | `mkdir d1` | `mkdir` (make directory) creates a new folder in your current location. |
| **3** | Create a file `a.txt` inside it | `touch d1/a.txt` | `touch` creates an empty file using a relative path inside folder `d1`. |
| **4** | Check permission of `a.txt` | `ls -l d1/a.txt` | The `-l` flag displays long format details, revealing permission strings like `-rw-r--r--`. |
| **5** | Explain octal decimal permissions | User(rw-)=6, Group(rw-)=6, Others(r--)=4 | Permissions are calculated by adding Read(4), Write(2), and Execute(1) bit values. |
| **6** | Change permissions of `a.txt` to 755 | `chmod 755 d1/a.txt` | `7` grants owner full access; `5` grants groups and others read and execute access. |
| **7** | Add a directory `d2` | `mkdir d2` | Creates a second folder named `d2`. |
| **8** | Add `b.txt` inside `d2` | `touch d2/b.txt` | Creates an empty text file inside folder `d2`. |
| **9** | Change permissions of `d2` (and contents) to 755 | `chmod -R 755 d2` | The `-R` flag applies permissions **recursively** to every file and folder inside `d2`. |
| **10** | Start the Firefox browser | `firefox &` | The ampersand (`&`) runs the application in the **background**, freeing up your terminal prompt. |
| **11** | List all processes in your computer | `ps aux` | `ps aux` takes a comprehensive snapshot of all user and background processes running. |
| **12** | Find PID of Firefox & understand parent/child | `ps aux \| grep firefox` | Parent processes spawn child processes (like tabs/plugins). If a child crashes, the parent survives. |
| **13** | Complex kill pipeline | `ps aux \| grep firefox \| grep -v grep \| awk '{print $2}' \| xargs kill -9` | Filters processes, extracts the PID column via `awk`, and force terminates them via `kill -9`. |
| **14** | What is your user in Linux? | `whoami` (or `id -u -n`) | Outputs your active account username tied to your user ID (UID). |
| **15** | What is your group in Linux? | `id -g -n` | Outputs your primary security group name (GID). |
| **16** | What is your computer architecture? | `uname -m` | Prints your machine hardware name (e.g., `x86_64` for 64-bit CPUs). |
| **17** | What is your audio driver? | `lspci \| grep -i audio` | Scans the PCI hardware bus list case-insensitively for sound cards. |
| **18** | Go to home folder & search for "java" | `cd ~ && find / -iname "*java*"` | Searches the entire system starting from root (`/`) case-insensitively for any file/folder containing "java". |
| **19** | List home folder sorted by time (reverse) with human sizes | `cd ~ && ls -lhart` | `-l` (long), `-h` (human sizes), `-a` (all/hidden), `-r` (reverse), `-t` (time modified). Newest files appear at the bottom! |
| **20** | Get last 30 lines & word counts for Harry Potter | `tail -n 30 Harry_Potter.txt`<br>`grep -o -i "Harry" Harry_Potter.txt \| wc -l` | `tail -n 30` extracts the final 30 lines, while `grep -o` combined with `wc -l` counts exact keyword frequencies. |
