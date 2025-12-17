# Security

## Cryptographic Design

### Encryption Algorithm

VEIL uses **AES-256-GCM** (Galois/Counter Mode), an authenticated encryption algorithm that provides:

- **Confidentiality**: 256-bit key strength
- **Integrity**: Built-in authentication tag
- **Performance**: Hardware acceleration on modern CPUs

### Key Derivation

Passphrases are converted to encryption keys using **PBKDF2-SHA256**:

- **Iterations**: 310,000 (OWASP 2023 recommendation)
- **Salt**: 16 random bytes per message
- **Output**: 256-bit key

### Initialization Vector

Each message uses a **unique 12-byte IV** generated with cryptographically secure randomness (`crypto.getRandomValues`).

## Security Properties

### What VEIL Protects

| Threat | Protection |
|--------|------------|
| Server reading messages | ✅ End-to-end encrypted |
| Network eavesdropping | ✅ Encrypted in transit |
| Message tampering | ✅ Authenticated encryption |
| Traffic analysis (content) | ✅ Hidden in cover messages |
| Casual observation | ✅ Plausible deniability |

### What VEIL Does NOT Protect

| Threat | Reason |
|--------|--------|
| Compromised device | Encryption happens on device |
| Screen capture | Visual access bypasses encryption |
| Key compromise | Security depends on key secrecy |
| Metadata | Timing, sender, recipient visible |
| Physical coercion | Human factor |

## Implementation Security

### Web Crypto API

All cryptographic operations use the browser's native **Web Crypto API**:

- No custom cryptographic implementations
- FIPS 140-2 compliant in most browsers
- Constant-time operations (side-channel resistant)

### Memory Handling

- Keys cleared from memory after use
- No plaintext logging
- Sensitive data not persisted in browser storage

### Random Number Generation

All random values generated using `crypto.getRandomValues()`:

- Cryptographically secure PRNG
- OS-level entropy source
- No Math.random() usage

## Threat Model

### In Scope

1. **Passive adversary**: Can read all messages on the server
2. **Active adversary**: Can modify messages (detected via authentication)
3. **Curious observer**: Cannot distinguish encrypted from normal messages

### Out of Scope

1. **Compromised endpoint**: Malware on user's device
2. **Targeted attacks**: State-level adversaries with device access
3. **Rubber-hose cryptanalysis**: Physical coercion

## Best Practices

### Passphrase Selection

- Minimum 8 characters (enforced)
- Recommended 12+ characters
- Use mixed case, numbers, symbols
- Avoid dictionary words
- Consider passphrase generators

### Key Exchange

**DO**:
- Share passphrases in person
- Use phone calls (voice verification)
- Use separate secure channel

**DON'T**:
- Send passphrase over Discord
- Use the same channel you're protecting
- Share via unencrypted email

### Operational Security

1. **Unique keys**: Different passphrase per conversation
2. **Regular rotation**: Change passphrases periodically
3. **Verify contacts**: Confirm identity before sharing keys
4. **Check indicators**: Watch for decryption success indicators

## Audit Status

### Code Review

- [ ] Independent security audit (planned)
- [x] Internal code review
- [x] Open architecture documentation

### Known Limitations

1. **Metadata leakage**: Message timing and frequency visible
2. **Steganographic capacity**: Very long messages may have larger covers
3. **Platform changes**: Discord updates may affect functionality

## Responsible Disclosure

Found a security issue? Please report responsibly:

1. **DO NOT** post publicly
2. Contact maintainers privately
3. Allow 90 days for fix before disclosure
4. We appreciate your help keeping users safe

## Comparison with Alternatives

| Feature | VEIL | Signal Protocol | PGP |
|-----------------|------|-----------------|-----|
| Forward secrecy | Per-message salt/IV | Full ratchet | None |
| Plausible deniability | ✅ Visual | ✅ Cryptographic | ❌ |
| Key exchange | Manual | Automatic | Manual |
| Metadata protection | Content only | Partial | None |

## Technical References

- [AES-GCM - NIST SP 800-38D](https://csrc.nist.gov/publications/detail/sp/800-38d/final)
- [PBKDF2 - RFC 8018](https://tools.ietf.org/html/rfc8018)
- [Web Crypto API - W3C](https://www.w3.org/TR/WebCryptoAPI/)
- [OWASP Password Storage](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html)
