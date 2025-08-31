# Challenge X: Renderer

**Category:** Web

## Description

The challenge provided a website where we could upload files, and it hinted that some sort of template rendering was happening in the background. The goal was to exploit this to retrieve the flag.

## Solution

### Step 1: Initial Analysis

The website had an upload functionality. At first glance, it looked like a simple image uploader, but the challenge name "Renderer" suggested the possibility of a **Server-Side Template Injection (SSTI)** vulnerability.

A common way to test for SSTI is to upload a file with a name containing template syntax like `{{7*7}}`. If the server uses Jinja2 (Python) or a similar engine, this expression would evaluate to `49`.

### Step 2: Testing for SSTI

I uploaded a harmless file and renamed it to `{{7*7}}.png`. After uploading, I checked how the filename was rendered on the gallery page.

Instead of showing `{{7*7}}`, the website displayed `49`. This confirmed that the filename was being passed through a template engine and executed on the server, proving that the application was vulnerable to SSTI.

### Step 3: Exploiting SSTI

Once SSTI was confirmed, I attempted to escalate the injection to access sensitive files. In Jinja2, one way to do this is by reading `/flag.txt` (a common location for CTF flags).

The payload looked like this:

```
{{ cycler.__init__.__globals__.os.popen('cat /flag.txt').read() }}
```

This payload uses Jinja2 object traversal to escape into Python internals, call the `os.popen` function, and execute a shell command to read the flag file.

### Step 4: Getting the Flag

I renamed my test file to:

```
{{ cycler.__init__.__globals__.os.popen('cat /flag.txt').read() }}.png
```

After uploading, instead of the filename, the gallery rendered the contents of `/flag.txt` — which was the flag.

## Flag

```
scriptCTF{example_flag_here}
```
