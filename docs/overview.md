# Overview

## What is VEIL?

VEIL is a local privacy layer for text-based communication. It provides encryption with plausible deniability - your encrypted messages appear as normal conversation to anyone who doesn't have your key.

## Key Concepts

### Plausible Deniability

Unlike traditional encryption that produces visible ciphertext, VEIL generates natural-looking messages. An observer cannot distinguish between:
- A real message
- A VEIL-encrypted message

### Cover Messages

When you send an encrypted message, VEIL generates a "cover" - a natural-sounding message that:
- Matches the conversation context
- Uses appropriate language (French/English)
- Appears genuine to outside observers

### Steganography

VEIL uses zero-width Unicode characters to hide encrypted data within the cover message. These characters are:
- Invisible to the human eye
- Not displayed by most applications
- Preserved through message transmission

## How It Works

```
┌─────────────────────────────────────────────────────┐
│                    SENDING                          │
├─────────────────────────────────────────────────────┤
│                                                     │
│  Your message: "RDV 18h gare du nord"               │
│                        │                            │
│                        ▼                            │
│  ┌─────────────────────────────────┐                │
│  │ 1. Encrypt with AES-256-GCM     │                │
│  │ 2. Encode as zero-width chars   │                │
│  │ 3. Generate contextual cover    │                │
│  │ 4. Inject hidden payload        │                │
│  └─────────────────────────────────┘                │
│                        │                            │
│                        ▼                            │
│  Sent: "ouais ça marche" (+ invisible payload)      │
│                                                     │
└─────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────┐
│                   RECEIVING                         │
├─────────────────────────────────────────────────────┤
│                                                     │
│  Received: "ouais ça marche" (+ invisible payload)  │
│                        │                            │
│                        ▼                            │
│  ┌─────────────────────────────────┐                │
│  │ 1. Extract zero-width payload   │                │
│  │ 2. Try decryption with key      │                │
│  │ 3. Success → show real message  │                │
│  │    Failure → show cover only    │                │
│  └─────────────────────────────────┘                │
│                        │                            │
│                        ▼                            │
│  With correct key: "RDV 18h gare du nord"           │
│  Without key: "ouais ça marche"                     │
│                                                     │
└─────────────────────────────────────────────────────┘
```

## Security Model

### Protected Against

- Passive eavesdropping
- Message interception
- Server-side message reading
- Metadata analysis (content only)

### Not Protected Against

- Compromised devices
- Screen recording/sharing
- Physical observation
- Key compromise

## Requirements

- Modern browser with Web Crypto API
- Compatible client application
- Shared passphrase with communication partner

## Next Steps

- [Getting Started](getting-started.md) - Installation guide
- [Configuration](configuration.md) - Setup options
- [Security](security.md) - Security details
