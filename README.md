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
