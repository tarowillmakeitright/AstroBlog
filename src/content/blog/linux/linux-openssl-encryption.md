---
author: Taro Gray
pubDatetime: 2025-11-16T08:00:00.000Z
title: How to encrypt the text using OpenSSL Encryption
postSlug: linux-openssl-encryption
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
description: This article describes how to decrypt and encrypt text using openssl.
---

## Table of contents

RSAでメッセージを暗号化したい場合は、OpenSSL で RSA鍵を生成し、その鍵を使って暗号化/復号するのが一般的です。 （GPG でも内部でRSAを使えるが、純粋に「RSAを直接使いたい」なら OpenSSL が簡単）

---

## ✅ 1. RSA鍵の作成

🔑 秘密鍵（private key）の生成

```
openssl genrsa -out private.pem 2048
```

🔑 公開鍵（public key）の生成

```
openssl rsa -in private.pem -pubout -out public.pem
```

これで

- private.pem → 秘密鍵
- public.pem → 公開鍵
  ができる。

---

## ✅ 2. 公開鍵でメッセージを暗号化（RSA暗号）

```
openssl rsautl -encrypt -inkey public.pem -pubin -in message.txt -out message.enc
```

---

## ✅ 3. 秘密鍵で復号

```
openssl rsautl -decrypt -inkey private.pem -in message.enc -out message_decrypted.txt
```

---

⚠️ 注意：RSA単体で大きなファイルは不可

RSAは
• 数百バイトしか直接暗号化できない
• 通常は「ハイブリッド暗号」を使う
（AES鍵をRSAで暗号化）

その場合：

🔹 AES鍵の生成

```
openssl rand 32 > key.bin
```

🔹 AESでデータ暗号化

```
openssl enc -aes-256-cbc -salt -in message.txt -out message.aes -pass file:./key.bin
```

🔹 AES鍵をRSAで暗号化

```
openssl rsautl -encrypt -inkey public.pem -pubin -in key.bin -out key.bin.enc
```

---

## ✔️ 結論

RSAを使いたい場合は OpenSSL の RSAコマンドを使う：

- RSA鍵生成: openssl genrsa
- 公開鍵抽出: openssl rsa -pubout
- 暗号化: openssl rsautl -encrypt
- 復号: openssl rsautl -decrypt

---
