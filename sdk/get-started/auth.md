# 🔐 Auth

## Introduction

To requesting the token, network, and other interface data for deposit and withdrawal services, you need to mount authorization token to the HTTP request header.

## How to use

For the configuration items used in the following examples, please refer to:

{% content-ref url="configuration.md" %}
[configuration.md](configuration.md)
{% endcontent-ref %}

{% hint style="info" %}
* Normally, you only need one `ETransferCore` instance already initialized.
  * For example:
    * [Get authorization token from the interface, and cache the data.](auth.md#get-authorization-token-from-the-interface-and-cache-the-data)
    * [Get authorization token from storage or interface, and cache the data.](auth.md#get-authorization-token-from-storage-or-interface-and-cache-the-data)
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

#### Get authorization token from the interface, and cache the data.

After getting the token, mount it to the request header and set it to storage.

**Example**

```javascript
import { eTransferCore } from '@etransfer/core';

eTransferCore.setAuthUrl('etransfer auth url');
const token = await eTransferCore.getAuthTokenFromApi(methodParameters);
```

**Method Parameters**

<table><thead><tr><th width="182">Field</th><th width="177">Type</th><th width="88">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>chain_id</td><td><code>ChainId</code></td><td><code>true</code></td><td><code>'AELF' | 'tDVV'</code></td></tr><tr><td>ca_hash</td><td><code>string</code></td><td><code>true</code></td><td>user ca hash</td></tr><tr><td>managerAddress</td><td><code>string</code></td><td><code>true</code></td><td>user manager address</td></tr><tr><td>pubkey</td><td><code>string</code></td><td><code>true</code></td><td>user account pubkey</td></tr><tr><td>plain_text</td><td><code>string</code></td><td><code>true</code></td><td>signed text</td></tr><tr><td>signature</td><td><code>string</code></td><td><code>true</code></td><td>user signature</td></tr><tr><td>version</td><td><code>PortkeyVersion</code></td><td><code>true</code></td><td><p><code>'v1' | 'v2'</code> .</p><p>Recommend using <code>'v2'</code></p></td></tr></tbody></table>

**Method return value**

<table><thead><tr><th width="185">Field</th><th width="175">Type</th><th>Remarks</th></tr></thead><tbody><tr><td>token</td><td><code>string</code></td><td>The authorization token.</td></tr></tbody></table>

#### Get authorization token from storage or interface, and cache the data.

Get data from the cache first. If the data in the storage has expired, it will get a new token from the interface.After getting the token, mount it to the request header and set it to storage.

**Example**

```javascript
import { eTransferCore } from '@etransfer/core';

eTransferCore.setAuthUrl('etransfer auth url');
const token = await eTransferCore.getAuthToken(methodParameters);
```

**Method Parameters**

<table><thead><tr><th width="175">Field</th><th width="185">Type</th><th width="100">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>chainId</td><td><code>ChainId</code></td><td><code>true</code></td><td><code>'AELF' | 'tDVV</code>'</td></tr><tr><td>caHash</td><td><code>string</code></td><td><code>true</code></td><td>user ca hash</td></tr><tr><td>managerAddress</td><td><code>string</code></td><td><code>true</code></td><td>user manager address</td></tr><tr><td>pubkey</td><td><code>string</code></td><td><code>true</code></td><td>user account pubkey</td></tr><tr><td>plainText</td><td><code>string</code></td><td><code>true</code></td><td>signed text</td></tr><tr><td>signature</td><td><code>string</code></td><td><code>true</code></td><td>user signature</td></tr><tr><td>version</td><td><code>PortkeyVersion</code></td><td><code>true</code></td><td><p><code>'v1' | 'v2'</code>.</p><p>Recommend using <code>'v2'</code></p></td></tr></tbody></table>

**Method return value**

| Field | Type   | Remarks                  |
| ----- | ------ | ------------------------ |
| token | string | The authorization token. |

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

<table><thead><tr><th width="180">Field</th><th width="179">Type</th><th width="102">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>chain_id</td><td><code>ChainId</code></td><td><code>true</code></td><td><code>'AELF' | 'tDVV'</code></td></tr><tr><td>ca_hash</td><td><code>string</code></td><td><code>true</code></td><td>user ca hash</td></tr><tr><td>managerAddress</td><td><code>string</code></td><td><code>true</code></td><td>user manager address</td></tr><tr><td>pubkey</td><td><code>string</code></td><td><code>true</code></td><td>user account pubkey</td></tr><tr><td>plain_text</td><td><code>string</code></td><td><code>true</code></td><td>signed text</td></tr><tr><td>signature</td><td><code>string</code></td><td><code>true</code></td><td>user signature</td></tr><tr><td>version</td><td><code>PortkeyVersion</code></td><td><code>true</code></td><td><p><code>'v1' | 'v2'</code>.</p><p>Recommend using <code>'v2'</code></p></td></tr></tbody></table>

**Method return value**

<table><thead><tr><th width="179">Field</th><th width="184">Type</th><th>Remarks</th></tr></thead><tbody><tr><td>token_type</td><td><code>string</code></td><td>The return token type, such as <code>Bearer</code>.</td></tr><tr><td>access_token</td><td><code>string</code></td><td>The return token body.</td></tr><tr><td>expires_in</td><td><code>number</code></td><td>Token expiration time, unit is seconds.</td></tr></tbody></table>

