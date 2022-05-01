# NahamCon CTF 2022: Personnel

Category: Web

Points: 50

## Description

> A challenge that was never discovered during the 2021 Constellations mission..
. now ungated :)

## Attached Files

 - [app.py](attached/app.py)

## Summary

For this challenge we are given an Python file that contains the code for a web application. The code uses regular expressions, though it has not been implemented securely. We can use an OR operator ("|") to add our own regex to match the pattern of the flag.

## Flag

```
flag{f0e659b45b507d8633065bbd2832c627}
```

## Detailed Solution

In the Python code, there is a regex findall function that can be used to find the flag.

```python
name = request.form["name"]
setting = int(request.form["setting"])
if name:
    if name[0].isupper():
        name = name[1:]

results = re.findall(r"[A-Z][a-z]*?" + name + r"[a-z]*?\n", users, setting)
results = [x.strip() for x in results if x or len(x) > 1]

return render_template("lookup.html", passed_results=True, results=results)
```

The format of the flag is `flag{<hex>}`, which is problematic to extract if we abide by the regex. This is due to the first character being uppercase. We can use an OR operator ("|") to add our own regex. Let's create our payload. We know the flag format which is `flag{[0-9a-f]{32}}`, so let's just simply search for that after the OR operator.

```
|flag{[0-9a-f]{32}}
```

As the final component of the regex checks for any length, we can ignore that as it will have a length of 0 after the final "}" character. After submitting the payload, we see many results with single characters. Though at the end of the page we can see the flag.

---
[Back to home](../../README.md)
