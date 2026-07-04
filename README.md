# CryptBrau

> **[Read the Cryptbrau Documentation](https://fable-retold.github.io/cryptbrau/)** - interactive docs with the full API reference.

Simple symmetric encryption for Node.js and the browser. Wraps the [simple-encryptor](https://www.npmjs.com/package/simple-encryptor) library with a key+salt configuration pattern and lazy encryptor initialization.

[cryptbrau on npm](https://www.npmjs.com/package/cryptbrau) | [MIT License](LICENSE)

---

## Features

- **Symmetric Encryption** - Encrypt and decrypt messages with a shared key and salt
- **Lazy Initialization** - The encryptor is created on first use, not at construction time
- **Key + Salt Pattern** - Concatenates a key and salt string to build the full encryption key, with automatic minimum-length padding
- **Browser Compatible** - Works in both Node.js and browser environments via the bundled browser shim

## Installation

```bash
npm install cryptbrau
```

## Quick Start

```javascript
const cryptBrau = require('cryptbrau');

let encryptor = cryptBrau({ Key: 'MySecretKey', Salt: 'MySaltValue' });

let encrypted = encryptor.encrypt('Hello, World!');
console.log('Encrypted:', encrypted);

let decrypted = encryptor.decrypt(encrypted);
console.log('Decrypted:', decrypted); // "Hello, World!"
```

## Usage

### Object Configuration

Pass an options object with `Key` and `Salt` properties:

```javascript
let encryptor = cryptBrau({ Key: 'SomeVerySecureKeyReally', Salt: 'SomeKindOfSalt' });
```

### String Shorthand

Pass a string directly and it will be used as the key with a default salt:

```javascript
let encryptor = cryptBrau('MySecretKey');
```

### Browser Usage

Include the browser bundle and access via `window.cryptBrau`:

```html
<script src="lib/cryptbrau.js"></script>
<script>
    var encryptor = cryptBrau({ Key: 'BrowserKey', Salt: 'BrowserSalt' });
    var encrypted = encryptor.encrypt('Secret message');
</script>
```

## API

### `cryptBrau(pOptions)`

Create an encryptor instance.

| Parameter | Type | Description |
|-----------|------|-------------|
| `pOptions` | `Object` or `String` | Configuration object with `Key` and `Salt`, or a string used as the key |

Returns an encryptor object with `encrypt` and `decrypt` methods.

**Options:**

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `Key` | `String` | `'ThisIsNotSecureEnough.'` | The encryption key |
| `Salt` | `String` | `'0000000000000000'` | Salt appended to the key |

The key and salt are concatenated to form the full encryption key. If the combined string is shorter than 16 characters, it is padded automatically.

### `encryptor.encrypt(pMessage)`

Encrypt a message string. Returns the encrypted string.

### `encryptor.decrypt(pMessage)`

Decrypt an encrypted message string. Returns the original plaintext.

## Part of the Retold Framework

CryptBrau is used in the Pict ecosystem for client-side encryption:

- [pict](https://github.com/fable-retold/pict) - UI framework
- [fable](https://github.com/fable-retold/fable) - Application services framework

## Related Packages

- [fable](https://github.com/fable-retold/fable) - Application services framework

## License

MIT

## Contributing

Pull requests are welcome. For details on our code of conduct, contribution process, and testing requirements, see the [Retold Contributing Guide](https://github.com/fable-retold/retold/blob/main/docs/contributing.md).
