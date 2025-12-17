# FAQ

## General

### What is VEIL?

VEIL is a privacy layer that adds end-to-end encryption to your messages with plausible deniability. Your encrypted messages appear as normal conversation to anyone without your key.

### Is VEIL free?

VEIL offers a free tier with basic features. Premium tiers unlock additional capabilities like priority support and advanced features.

### Is VEIL open source?

The architecture and documentation are public. The core implementation is proprietary to prevent unauthorized modifications and ensure security standards.

---

## Security

### How secure is VEIL?

VEIL uses AES-256-GCM encryption with PBKDF2 key derivation (310,000 iterations). This is industry-standard cryptography used by banks and governments.

### Can Discord read my encrypted messages?

No. Messages are encrypted on your device before being sent. Discord only sees the cover message, never your actual content.

### What if someone gets my passphrase?

If your passphrase is compromised:
1. Stop using that passphrase immediately
2. Agree on a new passphrase with your contact
3. Old messages remain protected by their unique salt/IV
4. New messages use the new key

### Can VEIL be detected?

VEIL is designed to be undetectable. Encrypted messages appear as normal conversation. There are no visible markers, special characters, or unusual patterns.

### Is VEIL legal?

Encryption is legal in most countries. However, laws vary by jurisdiction. Users are responsible for compliance with local laws.

---

## Usage

### How do I share my passphrase safely?

Never share passphrases through the same platform you're protecting. Use:
- In-person meeting
- Phone call
- Different secure messaging app
- Physical note

### Why isn't my contact receiving decrypted messages?

Check that:
1. Both have the exact same passphrase (case-sensitive)
2. Both have VEIL enabled
3. Passphrase meets minimum length (8 characters)
4. Plugin is active and configured

### Can I use different passphrases for different people?

Yes, and this is recommended. Use unique passphrases for each conversation to limit exposure if one is compromised.

### What happens if I type the wrong passphrase?

You'll see the cover message instead of the encrypted content. There's no error message - this is by design for plausible deniability.

### Do both parties need VEIL?

Yes. Both sender and receiver need VEIL with the same passphrase to exchange encrypted messages.

---

## Technical

### What encryption does VEIL use?

- **Algorithm**: AES-256-GCM
- **Key derivation**: PBKDF2-SHA256 (310,000 iterations)
- **IV**: 12 bytes, unique per message
- **Salt**: 16 bytes, unique per message

### How does the cover message work?

VEIL analyzes your conversation to generate contextually appropriate cover messages. The cover matches:
- Language (French/English)
- Conversation theme
- Message mood
- Typical length

### Where is my passphrase stored?

Your passphrase is stored locally on your device in encrypted form. It never leaves your device and is never sent to any server.

### Does VEIL slow down Discord?

No noticeable impact. Encryption/decryption happens in milliseconds using hardware-accelerated cryptography.

### What are zero-width characters?

Zero-width Unicode characters are invisible formatting characters. VEIL uses them to embed encrypted data within cover messages without being visible.

---

## Troubleshooting

### Messages aren't encrypting

1. Check that VEIL is enabled in settings
2. Verify passphrase is entered
3. Check passphrase length (minimum 8 characters)
4. Try disabling and re-enabling the plugin

### Cover messages look generic

1. Let context build over several messages
2. Check language setting matches conversation
3. Context analysis improves with more messages

### Plugin not loading

1. Check for client updates
2. Verify installation is correct
3. Check for conflicts with other plugins
4. Try reinstalling

### Performance issues

1. Disable random delay feature
2. Check system resources
3. Report persistent issues to support

---

## Privacy

### Does VEIL collect data?

VEIL operates entirely locally. No message content, passphrases, or personal data is collected or transmitted.

### Are there analytics?

License validation requires periodic server contact. No message content or encryption keys are ever transmitted.

### Can I verify the security?

Technical documentation is available in our [How It Works](how-it-works.md) and [Security](security.md) guides. The cryptographic approach is transparent and based on well-audited standards.

---

## Support

### How do I report a bug?

Contact support through the official channels with:
- Description of the issue
- Steps to reproduce
- Client version
- Any error messages

### How do I request a feature?

Feature requests are welcome through official support channels. Popular requests are prioritized for development.

### Is there a community?

Community channels are available for users to discuss usage, share tips, and get help from other users.
