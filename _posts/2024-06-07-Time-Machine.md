---
title: "Time Machine"
date: 2024-06-07
categories: [Writeups]
tags: [picoctf24,git]     # TAG names should always be lowercase
---

## Challenge

What was I last working on? I remember writing a note to help me remember...
You can download the challenge files here:
- [challenge.zip](https://artifacts.picoctf.net/c_titan/67/challenge.zip)

## Solution

### Download the challenge files

You can directly download the files by clicking on the link or use wget:
```bash
wget https://artifacts.picoctf.net/c_titan/67/challenge.zip
```

### Extract the files

Open terminal and go to the folder which contains the downloaded files.
Then run the following command to unzip the given zip file:
```bash
unzip challenge.zip
```

### Finding the flag

Go to the extracted folder named 'drop-in'. There's a file named message.txt. Let's see what's inside it.
```bash
cat message.txt
```
![P1](/assets/images/2024-06-07/Time-Machine-1.png)

The file doesn't contain flag, but it gives us a hint. It says "This is what I was working on, but I'd need to look at my commit history to know why..."
It might be a hint to check the commit history. Run the following command to get commit logs:
```bash
git log
```
![P2](/assets/images/2024-06-07/Time-Machine-2.png)

And there it is, our flag! Easy enough, right!