# How It Works

## Technical Overview

VEIL combines three technologies:
1. **Strong encryption** (AES-256-GCM)
2. **Steganography** (zero-width Unicode)
3. **Cover generation** (contextual NLP)

## Encryption

### Algorithm

- **Cipher**: AES-256-GCM (Authenticated Encryption)
- **Key Derivation**: PBKDF2-SHA256 with 310,000 iterations
- **IV**: Random 12 bytes per message
- **Salt**: Random 16 bytes per message

### Why AES-256-GCM?

- Industry standard
- Provides both confidentiality and integrity
- Hardware accelerated in modern CPUs
- Native Web Crypto API support

## Steganography

### Zero-Width Characters

VEIL uses four Unicode characters that are invisible:

| Character | Unicode | Binary    |
|-----------|---------|-----------|
| ZWSP      | U+200B  | 0         |
| ZWNJ      | U+200C  | 1         |
| ZWJ       | U+200D  | separator |
| WJ        | U+2060  | marker    |

### Encoding Process

```
Data: 0x48 (H) = 01001000

Encoded: WJ + ZWSP ZWNJ ZWSP ZWSP ZWNJ ZWSP ZWSP ZWSP + WJ
         ↑                                              ↑
      start                                           end
      marker                                        marker
```

### Injection Strategies

Payload can be injected:
- At the end of the cover message
- Distributed between words
- After punctuation marks

Strategy is chosen randomly to increase variability.

## Cover Generation

### Language Detection

VEIL analyzes recent messages to detect language:
- Word frequency matching
- Pattern recognition (accents, contractions)
- Weighted scoring system

### Context Analysis

The system tracks:
- Conversation theme (gaming, casual, planning, etc.)
- Recent message mood (positive, negative, neutral)
- Average message length
- Common phrases used

### Template System

Templates are organized by:
- Language (FR/EN)
- Category (reactions, continuations, contextual)
- Mood (positive, negative, neutral, surprised)

### Humanization

Generated covers are "humanized" with:
- Random typos (10% chance)
- Variable capitalization (25% chance)
- Punctuation variation (35% chance)
- Filler words for length matching

## Message Flow

### Sending

```
1. User types message
2. Plugin intercepts send event
3. Analyze channel context
4. Generate contextual cover
5. Encrypt original message
6. Encode as zero-width
7. Inject into cover
8. Send modified message
```

### Receiving

```
1. Message received
2. Try to extract zero-width payload
3. If found: attempt decryption
4. If success: display decrypted message
5. If failure: display message as-is
```

## Security Properties

### Confidentiality

Only parties with the correct passphrase can read messages.

### Integrity

AES-GCM provides authenticated encryption - tampering is detected.

### Plausible Deniability

Observers cannot distinguish encrypted messages from normal ones.

### Forward Secrecy

Each message uses unique salt and IV, limiting damage from key compromise.

## Limitations

- **Metadata**: Timing, sender, recipient still visible
- **Key distribution**: Must share passphrase securely out-of-band
- **Client compromise**: If device is compromised, encryption doesn't help
