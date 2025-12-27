# Salsa20 Demo (libsodium, C)

This repository documents my first successful cryptography build using the Salsa20 stream cipher via **libsodium**.

## What this project demonstrates
- Proper libsodium setup on Linux
- Random key and nonce generation
- Salsa20 encryption using XOR keystream
- Decryption by reapplying the same operation
- Why **nonce reuse is dangerous** in stream ciphers

## Build & Run

```bash
gcc salsa20_demo.c -o salsa20_demo $(pkg-config --cflags --libs libsodium)
./salsa20_demo
```
## Why Nonce Reuse Breaks Stream Ciphers

Stream ciphers like Salsa20 generate a keystream that is XORed with plaintext
to produce ciphertext.

If the same key and nonce are reused, the keystream is reused.

This allows an attacker to XOR two ciphertexts together:

C1 ⊕ C2 = (P1 ⊕ K) ⊕ (P2 ⊕ K) = P1 ⊕ P2

Once parts of one plaintext are known or guessed, the other plaintext
can be recovered. This is why nonce reuse is catastrophic in stream ciphers.
## Demo Output

The screenshot below shows the result of encrypting two different plaintext messages
using the same key and nonce with the Salsa20 stream cipher.

This demonstrates why nonce reuse is catastrophic in stream ciphers.

![Salsa20 Nonce Reuse Output](PASTE_YOUR_IMAGE_URL_HERE)
<img width="938" height="1281" alt="2222" src="https://github.com/user-attachments/assets/593092f2-3d68-476f-9567-086b029d8c8a" />

## Security Takeaway

⚠️ **This project intentionally demonstrates insecure cryptographic practice.**

Nonce reuse in stream ciphers (Salsa20, ChaCha20, etc.) is **catastrophic** and breaks confidentiality guarantees.

When the same key + nonce pair is reused:
- The keystream is reused
- XORing ciphertexts cancels the keystream
- The XOR of plaintexts is revealed
- Knowing or guessing one plaintext leaks the other

### Correct Practice
- **Never reuse a nonce with the same key**
- Use constructions that enforce nonce safety, such as **AEAD**
  - Example: `ChaCha20-Poly1305`

This code is for **educational purposes only** and must **never** be used in production.
