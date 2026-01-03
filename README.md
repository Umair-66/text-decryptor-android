# Text Decryptor Android App

A clean, user-friendly Android application that decrypts encrypted text using various cipher methods. Built with Java and follows MVVM architecture pattern.

## Features

### Supported Cipher Types
- **Caesar Cipher**: Shifts letters by a specified number (0-25)
- **ROT13**: Special case of Caesar cipher with fixed shift of 13
- **Atbash Cipher**: Replaces each letter with its mirror in the alphabet (A↔Z, B↔Y, etc.)
- **Base64 Decode**: Decodes Base64 encoded text
- **XOR Cipher**: XOR decryption with user-provided key

### User Interface
- Clean, Material Design 3 interface
- Dropdown selector for cipher types
- Input field for encrypted text
- Conditional key input field (appears only for ciphers that require it)
- Decrypt and Clear buttons
- Output area with copy-to-clipboard functionality
- Error handling with user-friendly messages
- Light/Dark mode support (automatic based on system settings)

### Technical Features
- **Architecture**: MVVM (Model-View-ViewModel) pattern
- **Language**: Java
- **Minimum SDK**: API 21 (Android 5.0)
- **Target SDK**: API 34 (Android 14)
- **Offline**: No internet dependency required
- **Data Privacy**: No user data is stored or transmitted

## How Decoding Works

### Caesar Cipher
- Shifts each letter backward by the specified number
- Example: "Khoor Zruog" with shift 3 → "Hello World"
- Non-alphabetic characters remain unchanged

### ROT13
- Fixed rotation of 13 positions
- Self-inverse: applying ROT13 twice returns original text
- Example: "Uryyb Jbeyq" → "Hello World"

### Atbash Cipher
- Each letter is replaced with its mirror position
- A↔Z, B↔Y, C↔X, etc.
- Example: "Svool Dliow" → "Hello World"

### Base64 Decode
- Decodes Base64 encoded strings
- Example: "SGVsbG8gV29ybGQ=" → "Hello World"

### XOR Cipher
- XORs each character with the key (repeating if necessary)
- Example: Encrypted text XOR key → Original text

## Project Structure

```
app/src/main/java/com/decryptor/app/
├── MainActivity.java              # Main UI controller
├── model/
│   ├── CipherType.java           # Enum for cipher types
│   └── DecryptionResult.java     # Result wrapper class
├── cipher/
│   ├── CipherInterface.java      # Common interface for all ciphers
│   ├── CaesarCipher.java        # Caesar cipher implementation
│   ├── Rot13Cipher.java         # ROT13 cipher implementation
│   ├── AtbashCipher.java        # Atbash cipher implementation
│   ├── Base64Cipher.java        # Base64 decoder implementation
│   ├── XorCipher.java           # XOR cipher implementation
│   └── CipherFactory.java       # Factory for creating cipher instances
└── viewmodel/
    └── DecryptorViewModel.java   # ViewModel for business logic
```

## Building the Project

1. **Prerequisites**:
   - Android Studio (latest stable version)
   - Java 8 or higher
   - Android SDK with API 21+

2. **Setup**:
   ```bash
   git clone <repository-url>
   cd DecryptorApp
   ```

3. **Build**:
   - Open project in Android Studio
   - Sync Gradle files
   - Build → Make Project
   - Run on device/emulator

## Extending the App

### Adding New Ciphers

1. **Create cipher class**:
   ```java
   public class NewCipher implements CipherInterface {
       @Override
       public DecryptionResult decrypt(String encryptedText, String key) {
           // Implementation here
           return DecryptionResult.success(decryptedText);
       }
   }
   ```

2. **Add to CipherType enum**:
   ```java
   NEW_CIPHER("New Cipher Name", requiresKey)
   ```

3. **Update CipherFactory**:
   ```java
   case NEW_CIPHER:
       return new NewCipher();
   ```

### Error Handling Guidelines
- Always validate input parameters
- Return `DecryptionResult.error(message)` for failures
- Use descriptive error messages for users
- Handle edge cases (empty strings, invalid keys, etc.)

## Example Usage

1. **Caesar Cipher Example**:
   - Input: "Khoor Zruog"
   - Cipher: Caesar Cipher
   - Key: 3
   - Output: "Hello World"

2. **ROT13 Example**:
   - Input: "Uryyb Jbeyq"
   - Cipher: ROT13
   - Output: "Hello World"

3. **Base64 Example**:
   - Input: "SGVsbG8gV29ybGQ="
   - Cipher: Base64 Decode
   - Output: "Hello World"

## Testing

The app includes comprehensive input validation and error handling:
- Empty input validation
- Invalid key format detection
- Malformed Base64 handling
- XOR key requirement validation

## License

This project is created for educational purposes. Feel free to use and modify as needed.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Implement your changes
4. Add appropriate tests
5. Submit a pull request

## Future Enhancements

- Auto-detection of cipher types
- Simple Substitution cipher implementation
- Batch processing of multiple texts
- Export/import functionality
- Additional cipher algorithms (Vigenère, Playfair, etc.)