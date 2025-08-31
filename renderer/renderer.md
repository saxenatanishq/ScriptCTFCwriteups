# Challenge 1: Renderer

**Category:** Web
**Points:** 498

## Solution

This web challenge was a capture-the-flag (CTF) puzzle involving a small Flask application. The goal was to exploit a vulnerability to read the contents of a file named `flag.txt` on the server. The solution involved a three-step process to bypass a cookie-based authentication system.

---

### Step 1: Initial Reconnaissance

After downloading and extracting the `chall.zip` file, the following key files were identified:

- `app.py`: The main Flask application logic.
- `templates/display.html`: A template file.
- `flag.txt`: The target file containing the flag.

The `display.html` file contained an `<iframe>` tag that seemed to be a potential target for a Server-Side Template Injection (SSTI) attack. However, closer inspection revealed that the filename was concatenated within a single Jinja expression `{{'/static/uploads/' + filename}}`. This means that any input provided for the `filename` parameter would be treated as data, not as a nested template, effectively neutralizing the SSTI attack vector.

The `app.py` file contained a `/developer` route that was the key to the challenge. The logic for this route was as follows:

- It checks for a cookie named `developer_secret_cookie`.
- It compares the cookie's value to the contents of a file located at `./static/uploads/secrets/secret_cookie.txt`.
- If the `secret_cookie.txt` file is empty, it generates a new SHA256 hash and writes it to the file.
- If the cookie value matches the file content, the server returns the contents of `flag.txt` and then rotates the secret by writing a new one to the file.

A critical observation was that the `secret_cookie.txt` file was located within the `/static/uploads` directory. This is significant because static files are publicly accessible, meaning we could potentially read the contents of this file directly.

---

### Step 2: Exploitation Strategy

The vulnerability lies in the fact that the secret required for authentication is stored in a publicly accessible location. The exploit strategy leverages this fact in three sequential requests:

1. **Force Secret Generation:** Send a GET request to the `/developer` endpoint without the required cookie. If the `secret_cookie.txt` file is empty, this action will trigger the server to generate and write a new secret to the file.
2. **Read the Secret:** Send a GET request to the public path `/static/uploads/secrets/secret_cookie.txt` to read the newly generated secret value.
3. **Authenticate and Get Flag:** Use the secret obtained in the previous step to make a GET request to `/developer`, this time including the `developer_secret_cookie` with the correct value. The server will then return the flag.

---

### Step 3: Raw HTTP Requests

The following raw HTTP requests were used to execute the exploit:

**Request to trigger secret generation:**
```http
GET /developer HTTP/1.1
Host: play.scriptsorcerers.xyz:10268
Connection: close
```
This request forces the server to create a secret if one doesn't exist. The server responds with "You are not a developer!", but the secret is now in the file.

**Request to read the secret:**
```http
GET /static/uploads/secrets/secret_cookie.txt HTTP/1.1
Host: play.scriptsorcerers.xyz:10268
Connection: close
```
The response body will contain the new secret, a SHA256 hex string.

**Request to authenticate and retrieve the flag:**
```http
GET /developer HTTP/1.1
Host: play.scriptsorcerers.xyz:10268
Cookie: developer_secret_cookie=<the_hex_secret_from_step_2>
Connection: close
```
Upon a successful match, the server responds with the flag. The response body will look like this:

---

### Result

By following these steps, the flag was successfully retrieved from the `/developer` endpoint.

**Flag:**
`scriptCTF{my_c00k135_4r3_n0t_s4f3!}`
