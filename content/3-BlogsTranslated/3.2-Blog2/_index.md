---
title: "Blog 2"
date: "2026-06-18"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Building Secure, Verifiable Blockchain Key Management on AWS Nitro Enclaves at Turnkey

<span class="meta-info">by Harshvardhan Chunawala and Jack Kearney | on 08 JUN 2026 | in</span> [Security](https://aws.amazon.com/blogs/web3/category/security-identity-compliance/security/), [Blockchain](https://aws.amazon.com/blogs/web3/category/blockchain/), [Architecture](https://aws.amazon.com/blogs/web3/category/architecture/) | [Permalink](https://aws.amazon.com/blogs/web3/building-secure-verifiable-blockchain-key-management-on-aws-nitro-enclaves-at-turnkey/)

Private key management is one of the hardest security challenges in Web3. Every transaction requires a cryptographic signature, and whoever possesses the private key controls the associated assets. A single compromise means irreversible loss.

[Turnkey](http://turnkey.com/) built a verifiable key management system on [AWS Nitro Enclaves](https://aws.amazon.com/ec2/nitro/nitro-enclaves/) that solves this — providing enclave-isolated key generation, attestable operations, and policy-based access controls without the traditional tradeoffs of DIY infrastructure, opaque custodians, or complex MPC systems.

---

## Architecture: Enclave-Native Key Management

Nitro Enclaves are hardened compute environments with no persistent storage, no interactive access, and no external networking. Turnkey runs all security-critical services — key generation, signing, and the policy engine — inside enclaves. Raw key material is **never exposed outside the enclave boundary**, including to Turnkey's own infrastructure.

Private keys are decrypted only inside the enclave at the moment of use. Key ciphertext persisted to the database is encrypted using a symmetric key derived from the **Quorum Key** — a master secret that exists only inside the enclave and is never exported.

### Key Generation & Storage

Turnkey uses a hierarchical deterministic (HD) wallet model. The Signer enclave generates a wallet seed using secure entropy from the [Nitro Security Module (NSM)](https://github.com/aws/aws-nitro-enclaves-nsm-api). Child key pairs are derived on demand via BIP-32/BIP-44 paths.

The seed is never stored in plaintext — it's encrypted under the Quorum Key and persisted to the database. At signing time, the enclave fetches the ciphertext, decrypts it entirely within its boundary, derives the child key, signs, then **discards the raw key material**.

### Enclave Applications

| Enclave | Role |
|---|---|
| **Signer** | Key generation and signing using NSM entropy |
| **Policy Engine** | Authentication and authorization via policy language |
| **Parser** | Extracts metadata from unsigned transactions |
| **Notarizer** | Authenticates organizational data before other enclaves act on it |
| **TLS Fetcher** | Only enclave with controlled external connectivity (via vsock) |

Enclaves do not trust each other by default. Each is independently attested at boot — inter-enclave requests verified against a known **Quorum Public Key**. Even a compromised host cannot impersonate an enclave.

---

## Enclave Attestation & Verification

When an enclave boots, the NSM records cryptographic measurements (PCR0–PCR3) and signs them into an **attestation document** containing:

- **PCR0** – Hash of the Enclave Image File (EIF)
- **PCR1** – Linux kernel hash
- **PCR2** – Hash of user applications
- **PCR3** – Hash of the IAM role of the Nitro host
- **Certificate** – X.509 cert with enclave-specific public key
- **cabundle** – Certificate chain to AWS root (valid until 2049)

Anyone can verify an enclave certificate originates from Amazon by walking this chain — transferring trust from Amazon's root key to the enclave-specific key. Signatures use P-384 (FIPS 186-4).

---

## Quorum Deployment & Reproducible Builds

Each enclave is configured with a **Share Set** — operators who each hold a share of the Quorum Key. Only after a threshold number of shares are submitted does the enclave reconstruct the key and launch.

Operators independently build enclave software and verify PCR measurements match before posting their key share. **No single engineer** can alter an enclave or reconstruct core secrets.

The foundation is [QuorumOS (QOS)](https://github.com/tkhq/qos) — a minimal, immutable Linux unikernel. All artifacts are **deterministically built** using [StageX](https://stagex.tools/), fully source-bootstrapped from a trusted 181-byte assembly seed. Anyone can download QOS source, build it locally, and verify the hash matches a live enclave's PCR measurements.

---

## Turnkey Verified: Boot Proofs in Practice

Turnkey exposes cryptographic proofs publicly through [Turnkey Verified](https://docs.turnkey.com/security/turnkey-verified). Two representative proof types:

**1) Address Derivation Proof** — confirms a wallet address was derived deterministically inside the enclave without the private key ever leaving the trust perimeter.

**2) Policy Outcome Proof** — confirms the Policy Engine evaluated a signing request against organizational rules entirely inside the enclave.

Each proof is a signed JSON payload, verifiable without trusting Turnkey's operational assertions.

---

## Threat Model

Turnkey treats **only enclave applications and their Share Sets as trusted**. Everything else — the host VM, Coordinator, database, even AWS infrastructure outside Nitro — is considered potentially compromised. This is achievable because Nitro Enclaves provide:

- **No persistent storage** — volatile memory cleared on restart
- **No network access** — vsock to host only
- **Hardware-rooted entropy and time** via NSM

Even a fully compromised host cannot extract keys from the enclave or modify enclave code.

---

## Real-World Use Cases

- **Embedded consumer wallets** — one wallet per user, genuine custody (developer cannot unilaterally move funds). Policy rules enforced inside the enclave.
- **AI agent transaction management** — constrain what an agent can sign (by asset, counterparty, size) without exposing private keys to the agent runtime.
- **Enterprise payments & smart contracts** — quorum-controlled provisioning, attestation-backed audit trail for compliance.

---

## Conclusion

Turnkey has operated in production for nearly four years, securing millions of wallets. The combination of **hardware isolation** (Nitro Enclaves), **reproducible builds** (QuorumOS + StageX), **quorum-controlled provisioning**, and **remote attestation** creates infrastructure that is both more secure and more transparent than previous approaches.

Start building: [Turnkey developer docs](https://docs.turnkey.com) | [Nitro Enclaves docs](https://docs.aws.amazon.com/enclaves/latest/user/nitro-enclave.html)
