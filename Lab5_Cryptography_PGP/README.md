# Lab 5 – Cryptography & PGP Digital Signatures

## Objective
Demonstrate practical understanding of public-key cryptography by encrypting a file using a recipient's public key, signing it with a personal private key using SHA256, and submitting all three components needed for verification.

## Background

This lab covers two foundational concepts in cryptography:

**Encryption** ensures that only the intended recipient can read a message. By encrypting with the instructor's public key, only their private key can decrypt it — meaning the answers are unreadable to anyone else in transit.

**Digital signatures** provide authentication and integrity. Signing the file with a private key and SHA256 produces a unique signature that anyone with the corresponding public key can verify. If the file is tampered with after signing, the signature will no longer match.

Together these two concepts form the basis of secure communication — used in everything from HTTPS and email (PGP/GPG) to code signing and SSL certificates.

## What I Did

1. Generated a PGP key pair using Keybase (OpenPGP v2.1.17)
2. Wrote answers to the 10 activity packet questions in a plain text file
3. Encrypted the answers file using the instructor's public key — only the instructor can decrypt it
4. Digitally signed the answers file using my private key and SHA256 — the instructor can verify authenticity using my public key
5. Submitted all three required files uncompressed

## Submitted Files

| File | Purpose |
|------|---------|
| `Daphny_Forcho_public_key.pem` | Public key — used by the instructor to verify the digital signature |
| `Daphny_Forcho_question_set_answers.txt` | Activity packet answers encrypted with the instructor's public key |
| `Daphny_Forcho_digital_signature.txt` | PGP digital signature of the answers file, signed with SHA256 |

## Tools Used

- **Keybase** — PGP key generation, encryption, and signing
- **OpenPGP v2.1.17**
- **SHA256** — hashing algorithm used for the digital signature
