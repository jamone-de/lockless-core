# Lockless-Core Architecture

This document outlines the cryptographic workflow and the Negative-Trust philosophy behind Lockless-Core.

## The Stateless Derivation Path

Unlike traditional vault-based systems, Lockless-Core never stores a secret. It utilizes a multi-layered Key Derivation Function (KDF) chain to compute identities on-the-fly.

### 1. Entropy Injection
The process begins with user-provided entropy. This input is never stored and exists only in volatile memory during the derivation process.

### 2. Hardware Anchoring (TPM 2.0)
To prevent offline brute-force attacks, the user entropy is bound to the local machine:
* A unique Hardware Root Key is generated inside the TPM 2.0 chip.
* The TPM performs a keyed-hash operation that cannot be exported from the silicon.
* This ensures that the identity can only be derived on the specific authorized device.

### 3. Computation Layer (Argon2id)
The resulting hardware-bound seed is processed through the Argon2id algorithm:
* Memory-Hardness: Designed to resist ASIC and GPU-accelerated cracking attempts.
* Side-Channel Resistance: Configured to mitigate timing attacks.

$$MasterKey = Argon2id(UserEntropy + TPM\_Hardware\_Binding, Salt, Iterations)$$

### 4. Zero-Persistence Output
The final key resides in Memory-Only. Once the session is closed or the duress-protocol is triggered, the key is wiped from RAM. No trace of the secret remains on the disk.

## Security Paradigms

* Negative-Trust: We assume the environment is compromised. Security is moved to the hardware-silicon and mathematical derivation.
* Anti-Forensics: Since there is no Vault File, there is nothing for an attacker to steal for offline analysis.
* Duress Protocol: Integration for automated emergency signals if the wrong derivation path is forced.

---
*Part of the JamOne Ecosystem. Just automate more.*
