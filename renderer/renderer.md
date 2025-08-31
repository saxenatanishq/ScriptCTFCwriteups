# Challenge 1: Renderer

**Type:** Web Challenge
**Points:** 498

---

## What Was the Challenge About?

This was a fun web hacking challenge where we had to find a way to read a secret file called `flag.txt` from a website. The website was built using Flask.

---

## How Did We Solve It?

### Step 1: Looking Around

First, we downloaded and opened the challenge files. Inside, we found:

- `app.py`: The main website code.
- `display.html`: A webpage template.
- `flag.txt`: The file we needed to read.

At first, we thought we could trick the website into running code (a common hack called SSTI), but the way the website was built made that impossible.

Then, we noticed a special page: `/developer`. This page checks for a special cookie called `developer_secret_cookie`. If the cookie matches a secret stored in a file, the website gives us the flag.

**Important:** The secret was stored in a file called `secret_cookie.txt`, which was inside a folder that anyone could access!

---

### Step 2: How We Tricked the Website

The website had a big mistake: it stored the secret in a place where anyone could read it. Here’s how we took advantage of that:

1. **Make the Website Create a Secret:**
   We visited the `/developer` page without any cookie. The website saw that there was no secret, so it created a new one and saved it in `secret_cookie.txt`.

2. **Read the Secret:**
   We then opened the file `secret_cookie.txt` directly from the website’s public folder. This gave us the secret code.

3. **Get the Flag:**
   We used the secret code as a cookie and visited `/developer` again. This time, the website recognized us and gave us the flag!

---

### Step 3: The Exact Steps We Used

Here are the exact web requests we made:

**First, we asked the website to create a secret:**
```
GET /developer
Host: play.scriptsorcerers.xyz:10268
```
The website said "You are not a developer!", but it secretly created a new code and saved it.

**Then, we read the secret code:**
```
GET /static/uploads/secrets/secret_cookie.txt
Host: play.scriptsorcerers.xyz:10268
```
The website sent us the secret code, something like `a94f2d6f...`.

**Finally, we used the secret to get the flag:**
```
GET /developer
Host: play.scriptsorcerers.xyz:10268
Cookie: developer_secret_cookie=a94f2d6f...
```
The website then gave us the flag!
![My solution screenshot](https://github.com/saxenatanishq/ScriptCTFCwriteups/blob/main/renderer/renderer_flag.jpg
)

---

## Final Result

By following these simple steps, we were able to read the secret file and get the flag!

**Flag:**
`<scriptCTF{REDACTED_FLAG_PASTE_HERE}>`
