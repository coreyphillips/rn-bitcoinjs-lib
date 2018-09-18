# BitcoinJS (bitcoinjs-lib)
[![Build Status](https://travis-ci.org/bitcoinjs/bitcoinjs-lib.png?branch=master)](https://travis-ci.org/bitcoinjs/bitcoinjs-lib)
[![NPM](https://img.shields.io/npm/v/bitcoinjs-lib.svg)](https://www.npmjs.org/package/bitcoinjs-lib)

[![js-standard-style](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://github.com/feross/standard)

This is a React Native compatible version of [bitcoinjs-lib](https://github.com/bitcoinjs/bitcoinjs-lib), a javascript Bitcoin library for node.js and browsers.

Released under the terms of the [MIT LICENSE](LICENSE).

### You shouldn't trust or rely on this repo for anything other than testing. To setup bitcoinjs-lib (4.0.2) in your RN project, please follow the how-to below:
[RN BitcoinJS-Lib (4.0.2) Setup](https://gist.github.com/coreyphillips/928ae27ccea69cd0b494d13ad2b3f27d)

## Can I trust this code?
> Don't trust. Verify.

You shouldn't trust or rely on this repo for anything other than testing. To setup bitcoinjs-lib (4.0.2) in your RN project, please follow the how-to below:

[RN BitcoinJS-Lib (4.0.2) Setup](https://gist.github.com/coreyphillips/928ae27ccea69cd0b494d13ad2b3f27d)


We recommend every user of this library and the [bitcoinjs](https://github.com/bitcoinjs) ecosystem audit and verify any underlying code for its validity and suitability.

Mistakes and bugs happen, but with your help in resolving and reporting [issues](https://github.com/bitcoinjs/bitcoinjs-lib/issues), together we can produce open source software that is:

- Easy to audit and verify,
- Tested, with test coverage >95%,
- Advanced and feature rich,
- Standardized, using [standard](http://github.com/standard/standard) and Node `Buffer`'s throughout, and
- Friendly, with a strong and helpful community, ready to answer questions.

## Documentation
Presently,  we do not have any formal documentation other than our [examples](#examples), please [ask for help](https://github.com/bitcoinjs/bitcoinjs-lib/issues/new) if our examples aren't enough to guide you.


## Installation
``` bash
yarn add rn-bitcoinjs-lib
```

## Setup

### React Native
Install the following dependencies:
``` bash
yarn add buffer-reverse react-native-randombytes crypto buffer@5
yarn add --dev rn-nodeify
react-native link react-native-randombytes
```
Add the following to your script in package.json: 

``` javascript
"postinstall": "rn-nodeify --install buffer,stream,assert,events,crypto,vm --hack"
```

Install any remaining dependencies and run postinstall.
 NOTE: (If you receive an error about "shim.js" not existing just run `yarn install` again): 

``` bash
yarn install
```

Add the following to shim.js:
``` javascript
if (typeof Buffer.prototype.reverse === 'undefined') {
  var bufferReverse = require('buffer-reverse');

  Buffer.prototype.reverse = function () {
    return bufferReverse(this);
  };
}
```

Add/Uncomment "require('crypto')" at the bottom of shim.js: 

``` javascript
require('crypto')
```

Finally:

``` bash
yarn install
```

**Usage**
``` javascript
import "./shim";
const bitcoin = require("rn-bitcoinjs-lib");
const keyPair = bitcoin.ECPair.makeRandom();
const { address } = bitcoin.payments.p2pkh({ pubkey: keyPair.publicKey });
console.log(address);
```

### Node.js
Use [bitcoinjs-lib](https://github.com/bitcoinjs/bitcoinjs-lib)

### Browser
Use [bitcoinjs-lib](https://github.com/bitcoinjs/bitcoinjs-lib)

## Examples
The below examples are implemented as integration tests, they should be very easy to understand.
Otherwise, pull requests are appreciated.
Some examples interact (via HTTPS) with a 3rd Party Blockchain Provider (3PBP).

- [Generate a random address](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/addresses.js#L22)
- [Generate an address from a SHA256 hash](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/addresses.js#L29)
- [Import an address via WIF](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/addresses.js#L40)
- [Generate a 2-of-3 P2SH multisig address](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/addresses.js#L47)
- [Generate a SegWit address](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/addresses.js#L60)
- [Generate a SegWit P2SH address](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/addresses.js#L67)
- [Generate a SegWit 3-of-4 multisig address](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/addresses.js#L76)
- [Generate a SegWit 2-of-2 P2SH multisig address](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/addresses.js#L90)
- [Support the retrieval of transactions for an address (3rd party blockchain)](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/addresses.js#L104)
- [Generate a Testnet address](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/addresses.js#L123)
- [Generate a Litecoin address](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/addresses.js#L133)
- [Create a 1-to-1 Transaction](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/transactions.js#L13)
- [Create a 2-to-2 Transaction](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/transactions.js#L28)
- [Create (and broadcast via 3PBP) a typical Transaction](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/transactions.js#L47)
- [Create (and broadcast via 3PBP) a Transaction with an OP\_RETURN output](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/transactions.js#L83)
- [Create (and broadcast via 3PBP) a Transaction with a 2-of-4 P2SH(multisig) input](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/transactions.js#L105)
- [Create (and broadcast via 3PBP) a Transaction with a SegWit P2SH(P2WPKH) input](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/transactions.js#L143)
- [Create (and broadcast via 3PBP) a Transaction with a SegWit P2WPKH input](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/transactions.js#L174)
- [Create (and broadcast via 3PBP) a Transaction with a SegWit P2PK input](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/transactions.js#L218)
- [Create (and broadcast via 3PBP) a Transaction with a SegWit 3-of-4 P2SH(P2WSH(multisig)) input](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/transactions.js#L263)
- [Verify a Transaction signature](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/transactions.js#L304)
- [Import a BIP32 testnet xpriv and export to WIF](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/bip32.js#L12)
- [Export a BIP32 xpriv, then import it](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/bip32.js#L20)
- [Export a BIP32 xpub](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/bip32.js#L31)
- [Create a BIP32, bitcoin, account 0, external address](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/bip32.js#L40)
- [Create a BIP44, bitcoin, account 0, external address](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/bip32.js#L55)
- [Create a BIP49, bitcoin testnet, account 0, external address](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/bip32.js#L71)
- [Use BIP39 to generate BIP32 addresses](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/bip32.js#L86)
- [Create (and broadcast via 3PBP) a Transaction where Alice can redeem the output after the expiry (in the past)](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/cltv.js#L43)
- [Create (and broadcast via 3PBP) a Transaction where Alice can redeem the output after the expiry (in the future)](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/cltv.js#L88)
- [Create (and broadcast via 3PBP) a Transaction where Alice and Bob can redeem the output at any time](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/cltv.js#L144)
- [Create (but fail to broadcast via 3PBP) a Transaction where Alice attempts to redeem before the expiry](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/cltv.js#L190)
- [Recover a private key from duplicate R values](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/crypto.js#L14)
- [Recover a BIP32 parent private key from the parent public key, and a derived, non-hardened child private key](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/crypto.js#L68)
- [Generate a single-key stealth address](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/stealth.js#L72)
- [Generate a single-key stealth address (randomly)](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/stealth.js#L91)
- [Recover parent recipient.d, if a derived private key is leaked (and nonce was revealed)](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/stealth.js#L107)
- [Generate a dual-key stealth address](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/stealth.js#L124)
- [Generate a dual-key stealth address (randomly)](https://github.com/bitcoinjs/bitcoinjs-lib/blob/master/test/integration/stealth.js#L147)

If you have a use case that you feel could be listed here, please [ask for it](https://github.com/bitcoinjs/bitcoinjs-lib/issues/new)!


## Contributing
See [CONTRIBUTING.md](CONTRIBUTING.md).


### Running the test suite

``` bash
npm test
npm run-script coverage
```

## Complementing Libraries
- [BIP21](https://github.com/bitcoinjs/bip21) - A BIP21 compatible URL encoding library
- [BIP38](https://github.com/bitcoinjs/bip38) - Passphrase-protected private keys
- [BIP39](https://github.com/bitcoinjs/bip39) - Mnemonic generation for deterministic keys
- [BIP32-Utils](https://github.com/bitcoinjs/bip32-utils) - A set of utilities for working with BIP32
- [BIP66](https://github.com/bitcoinjs/bip66) - Strict DER signature decoding
- [BIP68](https://github.com/bitcoinjs/bip68) - Relative lock-time encoding library
- [BIP69](https://github.com/bitcoinjs/bip69) - Lexicographical Indexing of Transaction Inputs and Outputs
- [Base58](https://github.com/cryptocoinjs/bs58) - Base58 encoding/decoding
- [Base58 Check](https://github.com/bitcoinjs/bs58check) - Base58 check encoding/decoding
- [Bech32](https://github.com/bitcoinjs/bech32) - A BIP173 compliant Bech32 encoding library
- [coinselect](https://github.com/bitcoinjs/coinselect) - A fee-optimizing, transaction input selection module for bitcoinjs-lib.
- [merkle-lib](https://github.com/bitcoinjs/merkle-lib) - A performance conscious library for merkle root and tree calculations.
- [minimaldata](https://github.com/bitcoinjs/minimaldata) - A module to check bitcoin policy: SCRIPT_VERIFY_MINIMALDATA


## Alternatives
- [BCoin](https://github.com/indutny/bcoin)
- [Bitcore](https://github.com/bitpay/bitcore)
- [Cryptocoin](https://github.com/cryptocoinjs/cryptocoin)


## LICENSE [MIT](LICENSE)
