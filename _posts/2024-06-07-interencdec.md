---
title: "interencdec"
date: 2024-06-07
categories: [Writeups]
tags: [picoctf24,base64,caesar,cryptography]     # TAG names should always be lowercase
---

## Challenge

Can you get the real meaning from this file.
Download the file [here](https://artifacts.picoctf.net/c_titan/3/enc_flag)

## Solution

From the title of the challenge 'interencdec', it seems like it involves inter encoding/decoding. Lets download the challenge files

```bash
wget https://artifacts.picoctf.net/c_titan/3/enc_flag
```

The challenge file contains an encoded string. 

```
YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclgya3lNRFJvYTJvMmZRPT0nCg==
```

From the trailing '=', we can guess that the string might be base64 encoded. Lets try decoding it.

```
d3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrX2kyMDRoa2o2fQ==
```

On decoding the string, we get another base64 encoded string. let's try decoding it again.

```
wpjvJAM{jhlzhy_k3jy9wa3k_i204hkj6}
```

This resembles something like a flag, but still encoded!
From the obtained string, we can see that only the alphabets are encoded, while the special characters like underscores and curly braces are intact.
This might indicate a shift cipher.

Pass this string to shift cipher decoder on [dcode.fr](https://www.dcode.fr/shift-cipher)

And guess what, we found our flag!

```
Put efforts for the last step yourself, I'm not gonna give away the plain flag!
```