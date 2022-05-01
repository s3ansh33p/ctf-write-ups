# NahamCon CTF 2022: Jurassic Park

Category: Web

Points: 50

## Description

> Dr. John Hammond has put together a small portfolio about himself for his new theme park, Jurassic Park. Check it out here!


## Summary

In the robots.txt file there was a disallowed route that might include the flag. Sure enough, there was. Below is the robots file.

```
User-agent: *
Disallow: /ingen/
```

After opening this route I found that the flag was located at /ingen/flag.txt.

## Flag

```
flag{c2145f65df7f5895822eb249e25028fa}
```

---
[Back to home](../../README.md)
