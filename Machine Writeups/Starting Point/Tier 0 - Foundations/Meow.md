# Meow

**Machine URL:** [Meow](https://app.hackthebox.com/machines/Meow?sort_by=created_at&sort_type=desc)

**Difficulty:** Very Easy

**Author:** Abdur Rehman Siddiqui

**Date Completed:** 21-Feb-2026

---

## Overview

![overview image](/Machine%20Writeups/Starting%20Point/Images/Meow/overview%20-%20meow.png)

## Solution

First we start with basic enumeration of the target by running nmap on the target machine IP 

`nmap -sC -minrate 1000 <machine-ip>`

![nmap](/Machine%20Writeups/Starting%20Point/Images/Meow/nmap%20-%20meow.png)

The nmap scan revealed an open port 23 running telnet. So we can basically try out connecting with telnet and see if it supports default credentials or not.

`telnet <machine-ip> <port-number>`

Upon connecting with the telnet service, I tried the default username `root` and the machine granted me full root access with blank password field.

Further exploration within the system revealed a `flag.txt` file from which I extracted the final flag.

![telnet](/Machine%20Writeups/Starting%20Point/Images/Meow/telnet%20-%20meow.png)

---

## Task Answers

### Task 1

What does the acronym VM stand for?

`Virtual Machine`

### Task 2

What tool do we use to interact with the operating system in order to issue commands via the command line, such as the one to start our VPN connection? It's also known as a console or shell.

`terminal`

### Task 3

What service do we use to form our VPN connection into HTB labs?

`openvpn`

### Task 4

What tool do we use to test our connection to the target with an ICMP echo request?

`ping`

### Task 5

What is the name of the most common tool for finding open ports on a target?

`nmap`

### Task 6

What service do we identify on port 23/tcp during our scans?

`telnet`

### Task 7

What username is able to log into the target over telnet with a blank password?

`root`

---