# NahamCon CTF 2022: Unimod

Category: Cryptography

Points: 50

## Description

> I was trying to implement ROT-13, but got carried away.

## Attached Files

 - [unimod.py](attached/unimod.py)
 - [out](attached/out)

## Summary

For this challenge we are given an Python file that contains opens a file and writes to it. The contents that it writes are the flag though encoded with a rotation of an arbitrary number. We know that the flag must start with a lowercase "f" and can therefore calculate the rotation. We then apply this rotation to the other bytes in the output file and we get out flag.

## Flag

```
flag{4e68d16a61bc2ea72d5f971344e84f11}
```

## Detailed Solution

In the Python code, a random key is chosen between `0` and `0xFFFD`. Each character in the flag is then encoded with this key. We can then decode the flag by applying the same key to the encoded flag.


Let's begin by first working out the rotation. We know that the flag must start with a lowercase "f" and can therefore calculate the rotation. Let's get the first character of the output file and brute force the rotation.
    
```python
flag = open('out', 'r').read()
key = 0
for x in range(0, 0x0FFFD):
    c = chr((ord(flag[0]) + x) % 0xFFFD)
    if (c == 'f'):
        key = x     
        break
```

We will now have our key and can decode the flag by simply looping through each character and applying the key to each character.

```python
ct = ''
for c in flag:
    ct += chr((ord(c) + key) % 0xFFFD)
            
print(ct)
```

And that's it! Our flag is now decoded and ouputted to the terminal.

---
[Back to home](../../README.md)
