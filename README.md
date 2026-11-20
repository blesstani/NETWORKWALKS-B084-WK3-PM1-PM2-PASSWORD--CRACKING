# NETWORKWALKS-B084-WK3-PM1-PM2-PASSWORD--CRACKING
password cracking using john and networkwalks tools# PDF Password Cracking Lab Report

# 🔐 PDF Password Cracking Lab Report

![Status](https://img.shields.io/badge/status-complete-brightgreen)
![Tool](https://img.shields.io/badge/tool-John%20the%20Ripper-red)
![Tool](https://img.shields.io/badge/tool-Networkwalks-blue)
![Type](https://img.shields.io/badge/type-password%20recovery-orange)

**Topic:** Recovering passwords from encrypted PDF files using John the Ripper (JTR) and online hash-cracking utilities
**Tools used:** John the Ripper (via Johnny GUI), onlinehashcrack.com PDF Hash Extractor, Networkwalks Hash Calculator, Networkwalks Password Cracker

---

## 🎯 1. Objective

This lab demonstrates two independent workflows for recovering the password of an encrypted PDF document:

1. 🖥️ **Local cracking** — extracting the PDF's hash and cracking it offline with John the Ripper.
2. 🌐 **Online cracking** — using web-based hash and password-cracking utilities to achieve the same result without local tooling.

> **Principle:** PDF encryption derives a verifiable hash from the user password, and that hash can be attacked with a wordlist or brute-force strategy until a candidate password reproduces it.

---

## 🖥️ 2. Method A — John the Ripper (via Johnny) + onlinehashcrack.com

### 2.1 Procedure

| Step | Action |
|:---:|---|
| 1️⃣ | Three password-protected PDF files were prepared as cracking targets. |
| 2️⃣ | Each PDF was uploaded to **onlinehashcrack.com/tools-pdf-hash-extractor** to extract its password hash. |
| 3️⃣ | Each extracted hash was saved individually into its own `.txt` file. |
| 4️⃣ | The hash files were loaded into **John the Ripper**, operated through the **Johnny** GUI front-end. |
| 5️⃣ | JTR was run against each hash file until a matching password was recovered. |

### 2.2 Results

```diff
+ File 1  →  good-luck
+ File 2  →  password1
+ File 3  →  1qaz2wsx
```

| PDF File | Recovered Password | Strength |
|---|---|:---:|
| File 1 | `good-luck` | 🟡 Weak (dictionary phrase) |
| File 2 | `password1` | 🔴 Very weak (common + digit) |
| File 3 | `1qaz2wsx` | 🟠 Weak (keyboard-walk pattern) |

> ⚠️ **Observation:** All three passwords are low-entropy, dictionary-style or keyboard-pattern passwords. This made them recoverable quickly with a standard wordlist attack, without needing brute force or a custom rule set.

---

## 🌐 3. Method B — Networkwalks Hash Calculator & Password Cracker

### 3.1 Procedure

1. 📤 Open the **Networkwalks Hash Calculator** in a web browser and upload the target PDF file. The tool reads the file's encryption data and outputs a hash string beginning with `$pdf$...`.
2. 📋 Copy the complete hash string.
3. 🧩 Open the **Networkwalks Password Cracker** in a web browser and paste the hash value into it.
4. ▶️ Start the attack. The tool iterates through candidate passwords until it finds one that matches the hash.
5. ✅ Once finished, the cracked password is displayed on screen. Copy it and use it to unlock the PDF.

### 3.2 Notes

- 🔁 This method mirrors Method A conceptually (hash extraction → hash-based attack) but offloads both steps to browser-based tools rather than local software.
- 🏷️ Hash format `$pdf$...` is the standard representation John the Ripper and compatible crackers use for PDF encryption hashes (it encodes the PDF revision, encryption algorithm, and key material needed for the attack).

---

## ⚖️ 4. Comparison of Methods

| Aspect | 🖥️ Method A (JTR + Johnny) | 🌐 Method B (Networkwalks) |
|---|---|---|
| Environment | Local (offline) | Online (browser-based) |
| Hash extraction | onlinehashcrack.com | Networkwalks Hash Calculator |
| Cracking engine | John the Ripper | Networkwalks Password Cracker |
| Control over attack mode | 🟢 High (wordlists, rules, masks configurable) | 🔴 Low (predefined attack on hosted service) |
| Data privacy | 🟢 Hash processed locally once extracted | 🟠 Hash/file passed to third-party web services |
| Best suited for | Repeatable, auditable, offline lab work | Quick one-off checks without local setup |

---

## ✅ 5. Conclusion

> Both workflows successfully recovered the passwords of the encrypted PDF files, confirming that **weak, predictable passwords** (common words, simple word+number combinations, keyboard-walk sequences) are readily broken by dictionary-based attacks — whether the attack is run locally via John the Ripper or through hosted online tools.

🛡️ **Takeaway:** Use long, random, non-dictionary passphrases when encrypting sensitive PDF documents.
