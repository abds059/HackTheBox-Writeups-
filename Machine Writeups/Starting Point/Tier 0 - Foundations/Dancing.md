# Dancing

**Machine URL:** [Dancing](https://app.hackthebox.com/machines/Dancing?sort_by=created_at&sort_type=desc)

**Difficulty:** Very Easy

**Author:** Abdur Rehman Siddiqui

**Date Completed:** 05-Mar-2026

---

## Overview

![overview](/Machine%20Writeups/Starting%20Point/Images/Dancing/overview.png)

## Solution

First we start with basic enumeration of the target by running nmap on the given machine IP

`nmap -sC -minrate 1000 <MACHINE-IP>`

![nmap](/Machine%20Writeups/Starting%20Point/Images/Dancing/nmap.png)

The nmap scan revealed the following services:

- msrpc (Microsoft RPC) running on port `135`
- netbios-ssn (NetBIOS Session) running on port `139`
- microsoft-ds (SMB) running on port `445`
- wsman (WinRM) running on port `5985`

Since RPC and WinRM usually require credentials we can first test SMB service to check for user names and if it allows anonymous access or not.

So we can use the follwoing command to test for listing SMB shares available and to check if the service allows anonymous login or not:

`smbclient -L //<MACHINE-IP>/ -N `

![smbclient shares](/Machine%20Writeups/Starting%20Point/Images/Dancing/user%20enumeration.png)

The first three shares are default windows shares but the fourth one (WorkShares) is a bit interesting to note. So we can try accessing it without password:

`smbclient //<MACHINE-IP>/WorkShares -N`

![smb connection](/Machine%20Writeups/Starting%20Point/Images/Dancing/smb%20connection%20and%20help.png)

So we are able to connect without password. We can then use the `help` command to view all available commands we can use inside.

From the help command we can see that we can list down the content available inside a directory by using the `ls` command.

After listing down the content we can see that there are two user directories `Amy.J` and `James.P`. We can check for the flag.txt file or any other file from these directories.

First we search for files inside `Amy.J` directory where we find a `worknotes.txt` file and on enumerating the `James.P` directory gives us the file `flag.txt`. We can download both of these files to our machine by using the `get` command.

![ls command](/Machine%20Writeups/Starting%20Point/Images/Dancing/flag%20enumeration.png)

After that we can simple extract out the content of the files using the `cat` command.

![worknotes.txt file](/Machine%20Writeups/Starting%20Point/Images/Dancing/worknotes.txt%20file.png)

![flag.txt file](/Machine%20Writeups/Starting%20Point/Images/Dancing/flag.txt%20file.png)

---

## Task Answers

### Task 1

What does the 3-letter acronym SMB stand for?

`Server Message Block`

## Task 2

What port does SMB use to operate at?

`445`

## Task 3

What is the service name for port 445 that came up in our Nmap scan?

`microsoft-ds`

## Task 4

What is the 'flag' or 'switch' that we can use with the smbclient utility to 'list' the available shares on Dancing?

`-L`

## Task 5

How many shares are there on Dancing?

`4`

## Task 6

What is the name of the share we are able to access in the end with a blank password?

`WorkShares`

## Task 7

What is the command we can use within the SMB shell to download the files we find?

`get`

---
