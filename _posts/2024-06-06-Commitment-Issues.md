---
title: "Commitment Issues"
date: 2024-06-06
categories: [Writeups]
tags: [picoctf24,git]     # TAG names should always be lowercase
---

## Challenge

I accidentally wrote the flag down. Good thing I deleted it!
You download the challenge files here:
- [challenge.zip](https://artifacts.picoctf.net/c_titan/137/challenge.zip)

## Solution

### Download the challenge files

You can directly download the files by clicking on the link or use wget:
```bash
wget https://artifacts.picoctf.net/c_titan/137/challenge.zip
```

![P1](/assets/images/2024-06-06/Commitment-Issues-1.png)

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
![P2](/assets/images/2024-06-06/Commitment-Issues-2.png)

There's nothing here. Notice that the title says 'Commit'ment Issues. So the flag might be deleted by a git commit. Lets check the git logs
```bash
git log --oneline
```
There's some interesting commit there which says 'remove sensitive info'. Let's go to its previous commit stage. Might find something useful there.
```bash
git reset --hard ea859bf
```

Now lets check the message.txt file again. Congrats, we found the flag!
![P3](/assets/images/2024-06-06/Commitment-Issues-3.png)
