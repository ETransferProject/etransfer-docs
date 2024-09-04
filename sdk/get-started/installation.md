# 📥 Installation

## Node Version

{% hint style="info" %}
**Node Version Requirement**

ETransfer SDK requires [Node.js](https://nodejs.org/) version 18 or above (v20 recommended). You can manage multiple versions of Node.js on the same machine with [n](https://github.com/tj/n), [nvm](https://github.com/creationix/nvm).
{% endhint %}

## Install

### @etransfer/core

{% hint style="info" %}
If you want to use the packaged authorization and withdrawal functions directly, please install the package as follows.
{% endhint %}

#### Commands

To install the package, use one of the following commands.

```bash
npm install @etransfer/core
# OR
yarn add @etransfer/core
```

#### Project Dependencies

`@etransfer/core`'s peer dependencies are listed below, they need to be installed together.

```json
{
  "@portkey/types": "2.4.0",
  "aelf-sdk": "^3.4.7",
  "bignumber.js": "^9.1.0",
  "query-string": "^7.1.1"
}
```

### @etransfer/utils

{% hint style="info" %}
If you want to use common methods, such as operating contracts, formatting error messages, etc, please install the package as follows.
{% endhint %}

#### Commands

To install the package, use one of the following commands.

```bash
npm install @etransfer/utils
# OR
yarn add @etransfer/utils
```

#### Project Dependencies

`@etransfer/utils`'s peer dependencies are listed below, they need to be installed together.

```json
{
  "@portkey/contracts": "^2.4.0",
  "@portkey/types": "^2.4.0",
  "@portkey/utils": "^2.4.0",
  "aelf-sdk": "^3.4.7",
  "bignumber.js": "^9.1.0",
  "query-string": "^7.1.1"
}
```
