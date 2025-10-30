**🃏 Card 1: What is the difference between Encoding, Encryption, and Hashing?**

- **Encoding**: Not for security. Just data format (e.g. Base64)
    
- **Encryption**: 2-way, needs a key. For confidentiality.
    
- **Hashing**: 1-way, used for integrity (e.g. SHA-256)
    

---

**🃏 Card 2: OWASP Top 3 Most Exploited in Real World?**

- **SQL Injection**
    
- **Cross-Site Scripting (XSS)**
    
- **Broken Authentication**
    

---

**🃏 Card 3: What’s the difference between Reflected and Stored XSS?**

- **Reflected**: Comes from the URL or request
    
- **Stored**: Stored in DB, reflects on future users
    
- DOM XSS: JS changes DOM without sanitization
    

---

**🃏 Card 4: What are common SQL Injection payloads?**

- `' OR '1'='1`
    
- `UNION SELECT null, version()`
    
- `'; DROP TABLE users --`  
    Always test with `OR 1=1`, `'--`, and time-based if needed
    

---

**🃏 Card 5: How to prevent SQL Injection?**

- **Use Prepared Statements**
    
- **Use ORM properly**
    
- Never trust user input
    

---

**🃏 Card 6: What’s the best protection against CSRF?**

- **CSRF Tokens (per request)**
    
- **SameSite Cookies (`Lax` or `Strict`)**
    
- **Double-submit cookie pattern**
    

---

**🃏 Card 7: What is an IDOR vulnerability?**

- **Insecure Direct Object Reference**
    
- Happens when a user can access someone else's data just by changing a parameter (e.g. `user_id=101` → `user_id=102`)
    
- Fix: Use access control checks
    

---

**🃏 Card 8: What’s the purpose of HttpOnly & Secure flags on cookies?**

- `HttpOnly`: JS can’t access the cookie
    
- `Secure`: Cookie sent only over HTTPS
    

---

**🃏 Card 9: Path Traversal - What does this payload do? `../../../../etc/passwd`**

- Tries to read sensitive files outside the web directory
    
- Defense: Normalize input paths + use allowlist
    

---

**🃏 Card 10: What’s the issue with verbose error messages?**

- Reveal stack traces, internal paths, versions
    
- Helpful to attackers during recon
    
- Always disable detailed error messages in production
    

---

**🃏 Card 11: What is XXE and what can it lead to?**

- XML External Entity injection
    
- Can read local files or perform SSRF
    
- Fix: Disable DTDs in XML parsers
    

---

**🃏 Card 12: What’s the risk of using outdated components (A9:2017)?**

- Known vulnerabilities in libraries/frameworks
    
- Use tools like **OWASP Dependency-Check**, **Snyk**
    

---

**🃏 Card 13: Difference between Authentication & Authorization?**

- **Authentication**: Who you are (Login)
    
- **Authorization**: What you're allowed to do (Access control)
    

---

**🃏 Card 14: What’s a Secure Password Policy?**

- Minimum 8+ chars, mix of types
    
- Hashed with bcrypt or Argon2 + salt
    
- Avoid password hints
    

---

**🃏 Card 15: What does the `Content-Security-Policy` header do?**

- Restricts sources for scripts/images/styles
    
- Mitigates XSS and injection attacks
    
- Example: `default-src 'self'; script-src 'self' https://apis.google.com`
    

---

**🃏 Card 16: Signs of a Business Logic Vulnerability?**

- Bypassing cart total
    
- Skipping payments
    
- Modifying flow like password resets
    
- Fix: Think like a malicious user + code review
    

---

**🃏 Card 17: What is a Supply Chain Attack?**

- Injecting malicious code into dependencies
    
- Fix: Use signed packages, monitor updates, SBOMs
    

---

**🃏 Card 18: What’s a good dev habit to prevent AppSec flaws?**

- Input validation at both client + server
    
- Use security libraries/frameworks
    
- Perform regular security testing (DAST/SAST)
    

---

**🃏 Card 19: Why is logging important for AppSec?**

- Helps detect suspicious behavior
    
- Must not log sensitive data (e.g. passwords)
    
- Log to centralized and secure storage
    

---

**🃏 Card 20: Bonus - How to use Burp Suite smartly for CAP?**

- **Repeater**: Test payloads
    
- **Intruder**: Brute force / fuzzing
    
- **Proxy**: Intercept traffic
    
- **Decoder**: Encode/decode Base64, URL, hex