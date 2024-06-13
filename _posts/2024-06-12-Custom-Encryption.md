---
title: "Custom Encryption"
date: 2024-06-12
categories: [Writeups]
tags: [picoctf24,cryptography]     # TAG names should always be lowercase
---

## Challenge

Can you get sense of this code file and write the function that will decode the given encrypted file content.
Find the encrypted file here [flag_info](https://artifacts.picoctf.net/c_titan/16/enc_flag) and [code file](https://artifacts.picoctf.net/c_titan/16/custom_encryption.py) might be good to analyze and get the flag.

## Solution

At first sight, I thought this is typical RSA encryption, it was similar to it, but not exactly the same.

### Encryption Process

Now lets understand the encryption process

- Two numbers p and q are defined, p=97 and q=31
- Checked if both p and q are prime using is_prime function
- Two numbers, a and b are generated randomly, with p-10 <= a < p and q-10 <= b < q
- Two number u and v are calculated using p,q,a,b as u = (g^a)%p and v = (g^b)%p where ^ represents power
- Two keys, key and b_key are calculated as key = (v^a)%p and b_key = (u^b)%p
- If both keys are same, the key is assigned as shared_key
- The plaintext is reversed and xored with input key string, text_key
- For each character of resultant xor string, its ascii value is multiplied by shared_key and 311 and stored in a list.
- Finally the list is returned as encrypted form

### Decryption Process

For decrypting the encoded flag, all the above steps need to be reversed. Use the below script to decrypt the flag:

```python
def generator(g, x, p):
    return pow(g, x) % p


def decrypt(cipher, key):
    plaintext = []
    for num in cipher:
        plaintext.append(chr(num // (key * 311)))
    return ''.join(plaintext)


def dynamic_xor_decrypt(cipher_text, text_key):
    key_length = len(text_key)
    decrypted_text = ""
    for i, char in enumerate(cipher_text):
        key_char = text_key[i % key_length]
        decrypted_char = chr(ord(char) ^ ord(key_char))
        decrypted_text += decrypted_char
    return decrypted_text[::-1]  # Reverse the string to get original plaintext


def reverse_encryption(cipher, a, b, p=97, g=31, text_key="trudeau"):
    u = generator(g, a, p)
    v = generator(g, b, p)
    shared_key = generator(v, a, p)

    semi_plaintext = decrypt(cipher, shared_key)
    plaintext = dynamic_xor_decrypt(semi_plaintext, text_key)
    return plaintext


if __name__ == "__main__":
    # Example values for a, b, and cipher (these would typically be provided)
    a = 97  # Example value, should be the same as used in encryption
    b = 22  # Example value, should be the same as used in encryption
    cipher = [151146, 1158786, 1276344, 1360314, 1427490, 1377108, 1074816, 1074816, 386262, 705348, 0, 1393902, 352674, 83970, 1141992, 0, 369468, 1444284, 16794, 1041228, 403056, 453438, 100764, 100764, 285498, 100764, 436644, 856494, 537408, 822906, 436644, 117558, 201528, 285498]
  # Example cipher text list
    
    decrypted_message = reverse_encryption(cipher, a, b)
    print(f'Decrypted message: {decrypted_message}')
```
Set the given values of a,b and cipher list in the above script to get the decoded flag.

![CS1](/assets/images/2024-06-08/Custom-Encryption-1.png)