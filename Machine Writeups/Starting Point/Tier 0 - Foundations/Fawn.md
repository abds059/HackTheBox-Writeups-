# Fawn

**Machine URL:** [Fawn](https://app.hackthebox.com/machines/Fawn?sort_by=created_at&sort_type=desc)

**Difficulty:** Very Easy

**Author:** Abdur Rehman Siddiqui

**Date Completed:** 25-Feb-2026

---

## Overview

![overview image](/Machine%20Writeups/Starting%20Point/Images/Fawn/overview.png)

## Solution

First we start with basic enumeration of the target by running nmap on the given machine IP

`nmap -sC -minrate 1000 <MACHINE-IP>`

![nmap](/Machine%20Writeups/Starting%20Point/Images/Fawn/nmap.png)

The nmap scan revealed an open port 21 running ftp with anonymous login enabled. So we can basically connect to ftp server without creating an account.

Before connecting to the service itself we can lookup for different commands for ftp service by running: 

`ftp -?`

![ftp help](/Machine%20Writeups/Starting%20Point/Images/Fawn/ftp%20help.png)

Here we get a comprehensive list of commands for interacting with the ftp service.

We then move onto connecting with the ftp service using the following command:

`ftp <MACHINE-IP>`

After running this the server prompts us for a username (which we already know from our nmap scan) so we enter `anonymous` and upon prompted for password we just keep it blank and press enter.

![ftp](/Machine%20Writeups/Starting%20Point/Images/Fawn/ftp%20get%20file.png)

On enumerating the server we discover a `flag.txt` file that we download to our attacker machine using the `get <file>` command.

After downloading we can simply run `cat <file>` to view the root flag.

![root flag](/Machine%20Writeups/Starting%20Point/Images/Fawn/root%20flag.png)

---

## Task Answers

### Task 1

What does the 3-letter acronym FTP stand for?

`File Transfer Protocol`

### Task 2

Which port does the FTP service listen on usually?

`21`

### Task 3

FTP sends data in the clear, without any encryption. What acronym is used for a later protocol designed to provide similar functionality to FTP but securely, as an extension of the SSH protocol?

`SFTP`

### Task 4

What is the command we can use to send an ICMP echo request to test our connection to the target?

`ping`

### Task 5

From your scans, what version is FTP running on the target?

`vsftpd 3.0.3`

### Task 6

From your scans, what OS type is running on the target?

`UNIX`

### Task 7

What is the command we need to run in order to display the 'ftp' client help menu?

`ftp -?`

### Task 8

What is username that is used over FTP when you want to log in without having an account?

`anonymous`

### Task 9

What is the response code we get for the FTP message 'Login successful'?

`230`

### Task 10

There are a couple of commands we can use to list the files and directories available on the FTP server. One is dir. What is the other that is a common way to list files on a Linux system.

`ls`

### Task 11

What is the command used to download the file we found on the FTP server?

`get`

---