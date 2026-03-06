# Redeemer

**Machine URL:** [Redeemer](https://app.hackthebox.com/machines/Redeemer?sort_by=created_at&sort_type=desc)

**Difficulty:** Very Easy

**Author:** Abdur Rehman Siddiqui

**Date Completed:** 06-Mar-2026

---

## Overview

![overview](/Machine%20Writeups/Starting%20Point/Images/Dancing/overview.png)

## Solution

First we start with basic enumeration of the target by running nmap on the given machine IP

`nmap -p- -minrate 1000 <MACHINE-IP>`

![nmap](/Machine%20Writeups/Starting%20Point/Images/Redeemer/nmap.png)

The nmap scan revealed a redis server running on port `6379`.

> Redis (REmote DIctionary Server) is an open-source, in-memory data structure store used as a database, cache, message broker, and streaming engine.  It stores data in RAM, enabling sub-millisecond response times and high throughput—making it ideal for applications requiring speed and real-time performance.

In order to interact with redis server we use a command line utility called `redis-cli`

For establishing a connection with redis we can refer to the help manual of redis-cli.

`redis-cli --help`

![redis-cli hep command](/Machine%20Writeups/Starting%20Point/Images/Redeemer/help.png)

From here we can see that we have to utilize the `-h` flag to specify the host. So we simply connect to redis databse using the following command:

`redis-cli -h <MACHINE-IP>`

After that we can list down the information available inside by using the `info` command.

![connection](/Machine%20Writeups/Starting%20Point/Images/Redeemer/connection.png)

From the info command we can see that there is a Keyspace section that describes how many keys are associated with a particular database.

> Keys in Redis are unique identifiers used to store, access, and manage data in Redis.  Every piece of data stored in Redis is associated with a key, forming a key-value pair, where the key is a string (or binary-safe sequence) and the value can be any Redis-supported data type (e.g., string, hash, list, set). 

In our case there is only a single Database (`db0`) with `4` keys.

![keys](/Machine%20Writeups/Starting%20Point/Images/Redeemer/keys.png)

We can select this database by typing `select 0` and we can view the all the keys avaialble inside using the `keys *` command.

![all keys](/Machine%20Writeups/Starting%20Point/Images/Redeemer/all%20keys.png)

Then we can simply listdown and extract the contents of the keys by using the command: `get <key-name>`.

![get flag](/Machine%20Writeups/Starting%20Point/Images/Redeemer/get%20flag.png)

---

## Tasks Answers

### Task 1

Which TCP port is open on the machine?

`6379`

### Task 2

Which service is running on the port that is open on the machine?

`redis`

### Task 3

What type of database is Redis? Choose from the following options: (i) In-memory Database, (ii) Traditional Database

`In-memory Database`

### Task 4

Which command-line utility is used to interact with the Redis server? Enter the program name you would enter into the terminal without any arguments.

`redis-cli`

### Task 5

Which flag is used with the Redis command-line utility to specify the hostname?

`-h`

### Task 6

Once connected to a Redis server, which command is used to obtain the information and statistics about the Redis server?

`info`

### Task 7

What is the version of the Redis server being used on the target machine?

`5.0.7`

### Task 8

Which command is used to select the desired database in Redis?

`select`

### Task 9

How many keys are present inside the database with index 0?

`4`

### Task 10

Which command is used to obtain all the keys in a database?

`keys *`

---