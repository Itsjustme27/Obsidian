# ✅ Y3ti@Sec CTF Setup Checklist (Beginner-Friendly 6h Event)

---

## 🔧 1. Platform Setup (CTFd)
- [ ] Set **CTF name**, description, start/end time (6h duration).
- [ ] Configure **scoring**:
  - [ ] Static (easy for beginners) OR
  - [ ] Dynamic (points decay per solve).
- [ ] Decide on **solo vs team mode** (e.g., max team size 3–4 for beginners).
- [ ] Enable **registration** (open or invite-only).
- [ ] Set **flag format** (e.g., `Y3TI{...}`).
- [ ] Add **rules page** (fair play, no DoS/bruteforce, don’t attack infra, etc.).
- [ ] Add **privacy/terms page** (optional but good practice).

---

## 🖥️ 2. Infra & Security
- [ ] (Local test) ✅ CTFd works on `localhost`.
- [ ] (If public) Setup **domain & SSL** with Let’s Encrypt.
- [ ] Create **admin account(s)**, secure passwords.
- [ ] Disable/lock test/demo accounts.
- [ ] Schedule **DB & challenge backups** (export `db` + Docker volumes).
- [ ] Optional: Enable **rate limits** in nginx to prevent brute force.

---

## 🏗️ 3. Challenges
- [ ] Define **categories** (Web, Crypto, Forensics, Misc, OSINT, etc.).
- [ ] Prepare **5–10 beginner-friendly challenges**:
  - Easy web (XSS, robots.txt, admin panel, etc.).
  - Simple crypto (Caesar, XOR, base64 chains).
  - Forensics (PCAP file, stego in image/audio).
  - OSINT (find flag in social media, metadata).
  - Misc/fun puzzle.
- [ ] Standardize **flag format** across all challenges.
- [ ] Host infra-based challenges in **isolated Docker containers**.
- [ ] Expose services via **nginx/Traefik subdomains** (`web1.ctf.local`, etc.).
- [ ] Test **solvability** of each challenge (at least 2 teammates test independently).

---

## 🎨 4. Player Experience
- [ ] Customize **logo, colors, theme** → “Y3ti@Sec CTF” branding.
- [ ] Add **announcements section** (for mid-event hints/updates).
- [ ] Configure **hint system** (optional: penalty points for using hints).
- [ ] Upload **practice challenge(s)** before event so players can test submission.

---

## 🧪 5. Dry Run
- [ ] Test **registration flow** (sign up as a participant).
- [ ] Test **team creation** (if enabled).
- [ ] Test **flag submission**.
- [ ] Verify **scoreboard updates** in real time.
- [ ] Stress-test: 5–10 users solving at once (friends can help simulate).
- [ ] Confirm **start/end time lockout** works (challenges hidden until start, submissions blocked after end).

---

## 🚀 6. Game Day
- [ ] Keep **admin panel open** for monitoring.
- [ ] Prepare **quick fixes** (typo in challenge, hint drop).
- [ ] Use announcements for **live updates**.
- [ ] Keep **backups & restart commands** ready in case Docker crashes.

---
