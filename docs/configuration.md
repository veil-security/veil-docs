# Configuration

## Settings

### Passphrase

Your encryption key. Requirements:
- Minimum 8 characters
- Recommended: 12+ characters with mixed case, numbers, symbols

**Important**: Share passphrases through a secure channel (in person, phone call), never through the platform you're protecting.

### Language

- **Auto-detect** (default): Analyzes conversation to choose FR or EN
- **French**: Force French cover messages
- **English**: Force English cover messages

### Hide Typing Indicator

When enabled, suppresses the "typing..." indicator while composing messages.

Default: **Enabled**

### Random Send Delay

Adds a random delay (300-1500ms) before sending. Makes message timing less predictable.

Default: **Enabled**

## Best Practices

### Passphrase Management

- Use unique passphrases for different conversations
- Don't reuse passphrases from other services
- Consider using a password manager

### Key Rotation

Periodically change your passphrase for added security:
1. Agree on new passphrase with your contact
2. Both update settings at the same time
3. Old messages remain readable with old key (if cached)

### Multi-Context Usage

For different security levels:
- **Casual**: Simple shared passphrase
- **Sensitive**: Strong passphrase, regular rotation
- **Critical**: Unique passphrase per conversation, frequent rotation

## Troubleshooting

### "Passphrase too short"

Increase to at least 8 characters.

### Cover messages don't match context

1. Wait for a few messages to build context
2. Check language setting
3. Context analysis improves over time

### Performance issues

1. Disable random delay
2. Check browser/client performance
3. Report persistent issues

## Advanced

### Environment Variables

For advanced users deploying custom builds:

```
VEIL_KDF_ITERATIONS=310000  # PBKDF2 iterations
VEIL_MIN_PASSPHRASE=8       # Minimum passphrase length
```

### Debug Mode

Not available in production builds for security reasons.
