---
title: "CanYouSee"
date: 2024-06-07
categories: [Writeups]
tags: [picoctf24,forensics,cryptography,metadata]     # TAG names should always be lowercase
---

## Challenge

How about some hide and seek?
Download this file [here](https://artifacts.picoctf.net/c_titan/5/unknown.zip).

## Solution

The challenge checks your knowledge for metadata and encodings

### Searching in Metadata

Download and extract the challenge files. It contains an image, but the image doesn't contain any flags when rendered.
Let's check this file's metadata using exiftool. Metadata is information about the file.

```bash
exiftool ukn_reality.jpg
```
![UKN1](/assets/images/2024-06-07/CanYouSee-1.png)

There seems to be some encoded string in the attribution URL, which looks weird. This string might be useful.

### Base64 Decoding

The string that we found has trailing '='. This might indicate that string is base64 encoded. Let's try decoding it.

```bash
echo cGljb0NURntNRTc0RDQ3QV9ISUREM05fNGRhYmRkY2J9Cg== | base64 -d
```

Run the above command

![UKN2](/assets/images/2024-06-07/CanYouSee-2.png)

And guess what, we got the flag!