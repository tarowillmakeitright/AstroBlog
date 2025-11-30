---
author: Taro Gray
pubDatetime: 2025-11-28T08:00:00.000Z
title: How to enrypt a file other then zip command 
postSlug: linux-file-encryption
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux, encryption
description: This article describes how to decrypt a file oter than zip command.
---

## Table of contents

If you want **strong encryption** (instead of the weak encryption used by `zip -er`), you should avoid ZIPCrypto and use **AES-256 encryption**.

Here are the secure alternatives depending on what tool you prefer:

---

## ✅ **Best Alternative (Recommended): Use 7z with AES-256**

`zip -er` uses old, weak ZIPCrypto.
**7z uses AES-256**, which is secure.

## # **Encrypt a file**

```bash
7z a -tzip -p -mem=AES256 file.zip file
```

Explanation:

* `-tzip` → output ZIP format
* `-p` → prompt for password
* `-mem=AES256` → use AES-256 instead of ZIPCrypto

---

## ✅ **Alternative for systems without 7z: Use gpg**

GPG gives you **strong encryption** and does not rely on ZIP format at all.

## # **Encrypt a file into .gpg**

```bash
gpg -c file
```

This produces `file.gpg` using AES-256 by default.

If you want ZIP-like compression + encryption manually:

```bash
tar -cf file.tar file
gpg -c file.tar
```

---

## ✅ **Alternative using `zip` but forcing AES (if supported)**

Some `zip` implementations support AES:

```bash
zip -e --compression-method aes256 file.zip file
```

or sometimes:

```bash
zip -ea file.zip file
```

**BUT** this only works if your `zip` binary was compiled with AES support.
Run:

```bash
zip -v
```

Look for:

```
AES encryption
```

If not present → it will still use **weak ZIPCrypto**.

---

## Summary

| Method                    | Encryption | Secure?  | Command                                   |
| ------------------------- | ---------- | -------- | ----------------------------------------- |
| `zip -er`                 | ZIPCrypto  | ❌ No     | `zip -er file.zip file`                   |
| **7z**                    | AES-256    | ✅ Yes    | `7z a -tzip -p -mem=AES256 file.zip file` |
| **GPG**                   | AES-256    | ✅ Yes    | `gpg -c file`                             |
| `zip` (AES-enabled build) | AES-256    | ⚠️ Maybe | varies                                    |

---


