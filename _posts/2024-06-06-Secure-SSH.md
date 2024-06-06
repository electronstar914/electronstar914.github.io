---
title: "Secure SSH"
date: 2024-06-06
categories: [Writeups]
tags: [picoctf24,ssh]     # TAG names should always be lowercase
---

## Challenge

Using a Secure Shell (SSH) is going to be pretty important.
Can you ssh as ctf-player to titan.picoctf.net at port 50400 to get the flag?
You'll also need the password 84b12bae. If asked, accept the fingerprint with yes.

## Solution

From the challenge, we can infer that
- username is 'ctf-player'
- password is '84b12bae'
- hostname is 'titan.picoctf.net'
- port number is 50400

All you have to do is simply login using ssh. Define the port number using '-p' flag.

```bash
ssh ctf-player@titan.picoctf.net -p 50400
```
Since you're connecting to this host first time. type 'yes' when prompted for connection confirmation.
Then enter the given password '84b12bae' when prompted. Don't worry if you don't see it as you type.
And as you press Enter, congrats, you found the flag!

![Profile Image](/assets/images/2024-06-06/Secure-SSH.png)
