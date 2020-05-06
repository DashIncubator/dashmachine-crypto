# Dashmachine crypto utility library

Cryptographic helper functions for use in Dash Platform Web Dapp Sample Messaging.

> Note: this is an experimental library to support the web dapp sample investigation of Dash Platform usage - not for production use.

## Browser usage

Include the `dashmachine-crypto-lib.js` script file available from the [releases page](https://github.com/dashmachine/dashmachine-crypto/releases).

## Nodejs usage

    npm i dashmachine-crypto

### Documentation

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

##### Table of Contents

-   [DashmachineCrypto](#dashmachinecrypto)
    -   [Examples](#examples)
-   [encrypt](#encrypt)
    -   [Parameters](#parameters)
-   [decrypt](#decrypt)
    -   [Parameters](#parameters-1)
-   [hash](#hash)
    -   [Parameters](#parameters-2)
-   [verify](#verify)
    -   [Parameters](#parameters-3)

#### DashmachineCrypto

DashmachineCrypto performs ECIES encryption & decryption and Double SHA256 Hashing. Note the class contains only static methods so you do not have to call the contructor, i.e. use DashmachineCrypto.encrypt, not new DashmachineCrypto()

##### Examples

```javascript
<!-- Usage in HTML file -->
<script src="dashmachine-crypto-lib.js" type="text/javascript"></script>
<script>
const vendorPrivateKey = '40148175614f062fb0b4e5c519be7b6f57b872ebb55ea719376322fd12547bff'
const message = 'hello';
const userPubicKey = 'A7GGInyvn7ExXkSVg+OFhbhVjEMhIFv0oyeJl03gFDRo'
const userPrivateKey = '219c8a8f9376750cee9f06e0409718f2a1b88df4acc61bf9ed9cf252c8602768'
const vendorPublicKey = 'A0/qSE6tis4l6BtQlTXB2PHW+WV+Iy0rpF5hAvX8hDRz'
console.log(`Encrypting message "${message}"...`);
const encrypted = DashmachineCrypto.encrypt(vendorPrivateKey, message, userPubicKey);
console.dir(encrypted.data);
console.log(`Decrypting result message "${message}"...`);
const decrypted = DashmachineCrypto.decrypt(userPrivateKey, encrypted.data, vendorPublicKey);
console.dir(decrypted);
console.log(`Hashing message "${message}"...`);
const digest = DashmachineCrypto.hash(message);
console.dir(digest.data);
console.log(`Verifying hash...`);
const verifies = DashmachineCrypto.verify(message, digest.data);
console.dir(verifies.success)
</script>
```

```javascript
//use in nodejs
const DashmachineCrypto = require("dashmachine-crypto")

const vendorPrivateKey = '40148175614f062fb0b4e5c519be7b6f57b872ebb55ea719376322fd12547bff'
const message = 'hello';
const userPubicKey = 'A7GGInyvn7ExXkSVg+OFhbhVjEMhIFv0oyeJl03gFDRo'
const userPrivateKey = '219c8a8f9376750cee9f06e0409718f2a1b88df4acc61bf9ed9cf252c8602768'
const vendorPublicKey = 'A0/qSE6tis4l6BtQlTXB2PHW+WV+Iy0rpF5hAvX8hDRz'
console.log(`Encrypting message "${message}"...`);
const encrypted = DashmachineCrypto.encrypt(vendorPrivateKey, message, userPubicKey);
console.dir(encrypted.data);
console.log(`Decrypting result message "${message}"...`);
const decrypted = DashmachineCrypto.decrypt(userPrivateKey, encrypted.data, vendorPublicKey);
console.dir(decrypted);
console.log('decrypted', decrypted.data);
```

#### encrypt

##### Parameters

-   `senderPrivateKey` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** The base64 repesentation of the HD private key of the Dash User sending the message, the result of calling client.account.getIdentityHDKey(0, 'user').privateKey where client is an instance of Dash.Client
-   `message` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** message to encrypt
-   `recipientPublicKey` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** The base64 repesentation of the public key for the Identity of the Dash User receiveing the message

Returns **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Either {success: true, data: [encrypted message]} or {error: true, message: [error message]}

#### decrypt

##### Parameters

-   `recipientPrivateKey` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** The base64 repesentation of the HD private key of the Dash User receiving the message, the result of calling client.account.getIdentityHDKey(0, 'user').privateKey where client is an instance of Dash.Client
-   `encryptedMessage` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** message to decrypt as a hex representation of the stringified JSON of the encryption result buffer
-   `senderPublicKey` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** The base64 repesentation of the public key for the Identity of the Dash User sending the message

Returns **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Either {success: true, data: [decrypted message]} or {error: true, message: [error message]}

#### hash

##### Parameters

-   `message` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** full message to be hashed

Returns **[Object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Either {success: true, data: [digest]} or {error: true, message: [error message]}

#### verify

##### Parameters

-   `message` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** full message to be hashed
-   `digest` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** digest to compare

### License

[MIT License](LICENSE)

# Development

To develop this library:

-   clone the repository and change to project directory 


    git clone  https://github.com/dashmachine/dashmachine-crypto.git && cd dashmachine-crypto

The source file is `src/crypto.service.js`

-   build output


    npm run build

-   test with webpack dev server


    npm start

-   update documentation (requires npm documentation package installed globally:  `npm i -g documentation`)

Update the Documentation section of the README.md file  

    npm run docs:readme
