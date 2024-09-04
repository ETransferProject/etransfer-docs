# 🔐 Auth

## Introduction

To request the token, network, and other interface data for deposit and withdrawal services, you need to mount the authorization token to the HTTP request header.

## How to use

For the configuration items used in the following examples, please refer to:

{% content-ref url="configuration.md" %}
[configuration.md](configuration.md)
{% endcontent-ref %}

{% hint style="info" %}
* Normally, you only need one `ETransferCore` instance initialized.
  * For example:
    * [Get the authorization token from the interface, and cache the data.](auth.md#get-the-authorization-token-from-the-interface-and-cache-the-data)
    * [Get the authorization token from the storage or interface, and cache the data.](auth.md#get-the-authorization-token-from-the-storage-or-interface-and-cache-the-data)
    * [Get the authorization token from the storage.](auth.md#get-the-authorization-token-from-the-storage)
* If you want to get a new token without any additional business logic.
  * For example:
    * [Only getting authorization tokens from the interface.](auth.md#only-getting-authorization-tokens-from-the-interface)
{% endhint %}

### Installation

{% content-ref url="installation.md" %}
[installation.md](installation.md)
{% endcontent-ref %}

```bash
npm install @etransfer/core
# OR
yarn add @etransfer/core
```

### Usage

{% hint style="info" %}
First, init the ETransferCore instance. You can find it in [ETransfer SDK Quick Start](quick-start.md#init-the-etransfercore-instance).
{% endhint %}

#### Get the authorization token from the interface, and cache the data.

After getting the token, mount it to the request header and set it to storage.

**Example**

```javascript
import { eTransferCore } from '@etransfer/core';

eTransferCore.setAuthUrl('etransfer auth url');
const token = await eTransferCore.getAuthTokenFromApi(methodParameters);
```

**Method Parameters**

<table><thead><tr><th width="180">Field</th><th width="139">Type</th><th width="91">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>pubkey</td><td><code>string</code></td><td><code>true</code></td><td>user account pubkey</td></tr><tr><td>plain_text</td><td><code>string</code></td><td><code>true</code></td><td>signed textThe format of the signature text is: <code>Nonce:&#x3C;current timestamp></code></td></tr><tr><td>signature</td><td><code>string</code></td><td><code>true</code></td><td>user signature</td></tr><tr><td>version</td><td><code>PortkeyVersion</code></td><td><code>true</code></td><td>Portkey version: <code>'v1' | 'v2</code>'. Recommend using v2</td></tr><tr><td>source</td><td><code>AuthTokenSource</code></td><td><code>true</code></td><td>Wallet type: <code>'portkey' | 'nightElf'</code></td></tr><tr><td>ca_hash</td><td><code>string</code></td><td><code>false</code></td><td>user ca hashIf source=<code>'portkey'</code>, you must set this parameter.</td></tr><tr><td>chain_id</td><td><code>ChainId</code></td><td><code>false</code></td><td><code>'AELF' | 'tDVV'</code>If source=<code>'portkey'</code>, you must set this parameter.</td></tr><tr><td>managerAddress</td><td><code>string</code></td><td><code>false</code></td><td>user manager address.</td></tr><tr><td>recaptchaToken</td><td><code>string</code></td><td><code>false</code></td><td>Recaptcha result.If source=<code>'portkey'</code>, you do not need to set this parameter.If source=<code>'nightElf'</code>, you need to query the interface <code>etransferCore.services.checkEOARegistration</code> first. If it returns true, you do not need to set this parameter; if it returns false, set the obtained verification result through human-machine verification.You can directly call the <code>etransferCore.getReCaptcha</code> method to help you quickly implement the above logic</td></tr></tbody></table>

**Method return value**

<table><thead><tr><th width="185">Field</th><th width="175">Type</th><th>Remarks</th></tr></thead><tbody><tr><td>token</td><td><code>string</code></td><td>The authorization token.</td></tr></tbody></table>

#### Get the authorization token from the storage or interface, and cache the data.

Get data from the cache first. If the data in the storage has expired, it will get a new token from the interface.After getting the token, mount it to the request header and set it to storage.

**Example**

```javascript
import { eTransferCore } from '@etransfer/core';

eTransferCore.setAuthUrl('etransfer auth url');
const token = await eTransferCore.getAuthToken(methodParameters);
```

**Method Parameters**

<table><thead><tr><th width="178">Field</th><th width="142">Type</th><th width="118">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>pubkey</td><td><code>string</code></td><td><code>true</code></td><td>user account pubkey</td></tr><tr><td>plainText</td><td><code>string</code></td><td><code>true</code></td><td>signed text</td></tr><tr><td>signature</td><td><code>string</code></td><td><code>true</code></td><td>user signature</td></tr><tr><td>version</td><td><code>PortkeyVersion</code></td><td><code>true</code></td><td>Portkey version: <code>'v1' | 'v2</code>'. Recommend using v2</td></tr><tr><td>managerAddress</td><td><code>string</code></td><td><code>true</code></td><td>user manager address</td></tr><tr><td>caHash</td><td><code>string</code></td><td><code>true</code></td><td>user ca hash</td></tr><tr><td>chainId</td><td><code>ChainId</code></td><td><code>true</code></td><td><code>'AELF' | 'tDVV</code>'</td></tr><tr><td>source</td><td><code>AuthTokenSource</code></td><td><code>false</code></td><td>Wallet type: <code>'portkey' | 'nightElf'</code>Default is <code>'portkey'</code></td></tr><tr><td>recaptchaToken</td><td><code>string</code></td><td><code>false</code></td><td>Recaptcha result.If source=<code>'portkey'</code>, you do not need to set this parameter.If source=<code>'nightElf'</code>, you need to query the interface <code>etransferCore.services.checkEOARegistration</code> first. If it returns true, you do not need to set this parameter; if it returns false, set the obtained verification result through human-machine verification.You can directly call the <code>etransferCore.getReCaptcha</code> method to help you quickly implement the above logic</td></tr></tbody></table>

**Method return value**

| Field | Type   | Remarks                  |
| ----- | ------ | ------------------------ |
| token | string | The authorization token. |

#### Get the authorization token from the storage.

Get the authorization token from the storage.

{% hint style="info" %}
The premise is that authorization token has been obtained from the interface before.
{% endhint %}

If the authorization token is expired, return `undefined`.

**Example**

```javascript
import { eTransferCore } from '@etransfer/core';

const token = await eTransferCore.getAuthTokenFromStorage(methodParameters);
```

**Method Parameters**

<table><thead><tr><th width="175">Field</th><th width="185">Type</th><th width="100">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>walletType</td><td>TWalletType</td><td><code>true</code></td><td><code>'portkey' | 'nightElf'</code></td></tr><tr><td>managerAddress</td><td><code>string</code></td><td><code>true</code></td><td>user manager address</td></tr><tr><td>caHash</td><td><code>string</code></td><td><code>false</code></td><td>user ca hash</td></tr></tbody></table>

**Method return value**

| Field | Type                  | Remarks                  |
| ----- | --------------------- | ------------------------ |
| token | `string \| undefined` | The authorization token. |

#### Only getting authorization tokens from the interface.

Get a new token without any additional business logic.

**Example**

```javascript
import { eTransferCore } from '@etransfer/core';

const result = await eTransferCore.services.getAuthToken(methodParameters, { baseURL: 'etransfer auth url' });

// Combination token
const token = result.token_type + result.access_token;

// Token expiration time, unit is seconds
const tokenExpired = result.expires_in;
```

**Method Parameters**

<table><thead><tr><th width="176">Field</th><th width="121">Type</th><th width="121">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>pubkey</td><td><code>string</code></td><td><code>true</code></td><td>user account pubkey</td></tr><tr><td>plain_text</td><td><code>string</code></td><td><code>true</code></td><td>signed text</td></tr><tr><td>signature</td><td><code>string</code></td><td><code>true</code></td><td>user signature</td></tr><tr><td>version</td><td><code>PortkeyVersion</code></td><td><code>true</code></td><td>Portkey version: <code>'v1' | 'v2</code>'. Recommend using v2</td></tr><tr><td>managerAddress</td><td><code>string</code></td><td><code>true</code></td><td>user manager address</td></tr><tr><td>source</td><td><code>AuthTokenSource</code></td><td><code>true</code></td><td>Wallet type: <code>'portkey' | 'nightElf'</code></td></tr><tr><td>ca_hash</td><td><code>string</code></td><td><code>false</code></td><td>user ca hashIf source=<code>'portkey'</code>, you must set this parameter.</td></tr><tr><td>chain_id</td><td><code>ChainId</code></td><td><code>false</code></td><td><code>'AELF' | 'tDVV'</code>If source=<code>'portkey'</code>, you must set this parameter.</td></tr><tr><td>recaptchaToken</td><td><code>string</code></td><td><code>false</code></td><td>Recaptcha result.If source=<code>'portkey'</code>, you do not need to set this parameter.If source=<code>'nightElf'</code>, you need to query the interface <code>etransferCore.services.checkEOARegistration</code> first. If it returns true, you do not need to set this parameter; if it returns false, set the obtained verification result through human-machine verification.You can directly call the <code>etransferCore.getReCaptcha</code> method to help you quickly implement the above logic</td></tr></tbody></table>

**Method return value**

<table><thead><tr><th width="179">Field</th><th width="184">Type</th><th>Remarks</th></tr></thead><tbody><tr><td>token_type</td><td><code>string</code></td><td>The return token type, such as <code>Bearer</code>.</td></tr><tr><td>access_token</td><td><code>string</code></td><td>The return token body.</td></tr><tr><td>expires_in</td><td><code>number</code></td><td>Token expiration time, unit is seconds.</td></tr></tbody></table>

