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

![Salsa20 Nonce Reuse Output](PASTE_YOUR_IMAGE<img width="1488" height="471" alt="Screenshot from 2025-12-26 20-13-41" src="https://github.com/user-attachments/assets/8db69261-b7dc-4d38-bc6c-66c510214f2b" />
_URL_HERE)

