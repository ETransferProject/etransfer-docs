# 💰 Withdraw Digital Assets

## Introduction

**Withdraw Digital Assets**

Transfer assets from the aelf chain to other chains.

{% content-ref url="../../readme/business-process/withdraw-process.md" %}
[withdraw-process.md](../../readme/business-process/withdraw-process.md)
{% endcontent-ref %}

**SDK - Withdraw Assets**

Based on the token, network and other information selected by the user, generate TransactionRaw and submit it to the server to complete the creation of the withdrawal order.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

## How to use

{% hint style="info" %}
First, init the ETransferCore instance. You can find it in [ETransfer SDK Quick Start](quick-start.md#init-the-etransfercore-instance).
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

#### Get supported assets

Acquire the list of assets supported by ETransfer.You can find which assets are supported for withdrawal.

**Example**

```javascript
import { eTransferCore } from '@etransfer/core';
import { BusinessType } from '@etransfer/types';

const result = await eTransferCore.services.getTokenList({
  type: BusinessType.Withdraw,
  chainId: 'AELF',
});
```

**Http Headers**

<table><thead><tr><th width="155">Header</th><th width="104">Type</th><th width="104">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>Authorization</td><td><code>string</code></td><td><code>true</code></td><td><p>The authorization token is the result returned by /connect/token.</p><p>How to acquire: <a href="auth.md">ETransfer SDK Auth</a>.</p></td></tr></tbody></table>

**Method Parameters**

<table><thead><tr><th width="116">Field</th><th width="162">Type</th><th width="115">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>type</td><td><code>BusinessType</code></td><td><code>true</code></td><td>Business type: <code>'Deposit'</code></td></tr><tr><td>chainId</td><td><code>ChainId</code></td><td><code>true</code></td><td><code>'AELF' | 'tDVV'</code></td></tr></tbody></table>

**Method return value**

<table><thead><tr><th width="119">Field</th><th width="162">Type</th><th>Remarks</th></tr></thead><tbody><tr><td>tokenList</td><td><code>TTokenItem[]</code></td><td>Crypto array</td></tr></tbody></table>

**`TTokenItem` type**

<table><thead><tr><th width="187">Field</th><th width="137">Type</th><th>Remarks</th></tr></thead><tbody><tr><td>name</td><td><code>string</code></td><td>Crypto name</td></tr><tr><td>symbol</td><td><code>string</code></td><td>Crypto symbol</td></tr><tr><td>icon</td><td><code>string</code></td><td>Crypto logo url</td></tr><tr><td>contractAddress</td><td><code>string</code></td><td>ETransfer contract address</td></tr><tr><td>decimals</td><td><code>number</code></td><td>Crypto decimals</td></tr></tbody></table>

#### Get supported networks

Acquire the list of networks supported by ETransfer.You can find which networks are supported for withdrawal.You can get the basic information and the block confirmations of the network, etc.

**Example**

```javascript
import { eTransferCore } from '@etransfer/core';
import { BusinessType } from '@etransfer/types';

const result = await eTransferCore.services.getNetworkList({
  type: BusinessType.Withdraw,
  chainId: 'AELF',
  symbol: 'USDT',
  address: '0x...',
});
```

**Http Headers**

<table><thead><tr><th width="155">Header</th><th width="104">Type</th><th width="104">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>Authorization</td><td><code>string</code></td><td><code>true</code></td><td><p>The authorization token is the result returned by /connect/token.</p><p>How to acquire: <a href="auth.md">ETransfer SDK Auth</a>.</p></td></tr></tbody></table>

**Method Parameters**

<table><thead><tr><th width="131">Field</th><th width="160">Type</th><th width="104">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>type</td><td><code>BusinessType</code></td><td><code>true</code></td><td>Business type: <code>'Withdraw'</code></td></tr><tr><td>chainId</td><td><code>ChainId</code></td><td><code>true</code></td><td><code>'AELF' | 'tDVV'</code></td></tr><tr><td>symbol</td><td><code>string</code></td><td><code>false</code></td><td>Get data from eTransferCore.services.getTokenList</td></tr><tr><td>address</td><td><code>string</code></td><td><code>false</code></td><td>Withdrawal address. Please remove the prefix and suffix of the ELF-DID address.</td></tr></tbody></table>

**Method return value**

<table><thead><tr><th width="192">Field</th><th width="178">Type</th><th>Remarks</th></tr></thead><tbody><tr><td>network</td><td><code>string</code></td><td>Network</td></tr><tr><td>name</td><td><code>string</code></td><td>Network name</td></tr><tr><td>multiConfirm</td><td><code>string</code></td><td>Network block confirmations</td></tr><tr><td>multiConfirmTime</td><td><code>string</code></td><td>Network block confirmation time</td></tr><tr><td>contractAddress</td><td><code>string</code></td><td>Network contract address</td></tr><tr><td>explorerUrl</td><td><code>string</code></td><td>Network explorer address</td></tr><tr><td>status</td><td><code>NetworkStatus</code></td><td>Network health status <code>'Health' | 'Congesting' | 'Offline'</code></td></tr><tr><td>withdrawFee</td><td><code>string</code></td><td>Network withdrawal fee</td></tr><tr><td>withdrawFeeUnit</td><td><code>string</code></td><td>Network withdrawal fee unit</td></tr></tbody></table>

#### Get withdraw information

Acquire the withdrawal information and transaction fee.

{% hint style="danger" %}
Please check the minimum withdrawal limit and remaining limit.
{% endhint %}

**Example**

```javascript
import { eTransferCore } from '@etransfer/core';
import { PortkeyVersion } from '@etransfer/types';

const result = await eTransferCore.services.getWithdrawInfo({
  chainId: 'AELF',
  network: 'ETH',
  symbol: 'USDT',
  amount: '100',
  address: '0x...',
  version: PortkeyVersion.v2,
});
```

**Http Headers**

<table><thead><tr><th width="155">Header</th><th width="104">Type</th><th width="104">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>Authorization</td><td><code>string</code></td><td><code>true</code></td><td><p>The authorization token is the result returned by /connect/token.</p><p>How to acquire: <a href="auth.md">ETransfer SDK Auth</a>.</p></td></tr></tbody></table>

**Method Parameters**

<table data-header-hidden><thead><tr><th width="125"></th><th width="181"></th><th width="107"></th><th></th></tr></thead><tbody><tr><td><strong>Field</strong></td><td><strong>Type</strong></td><td><strong>Required</strong></td><td><strong>Remarks</strong></td></tr><tr><td>chainId</td><td><code>ChainId</code></td><td><code>true</code></td><td><code>'AELF' | 'tDVV'</code></td></tr><tr><td>network</td><td><code>string</code></td><td><code>false</code></td><td>Get data from eTransferCore.services.getNetworkList</td></tr><tr><td>symbol</td><td><code>string</code></td><td><code>false</code></td><td>Get data from eTransferCore.services.getTokenList</td></tr><tr><td>amount</td><td><code>string</code></td><td><code>false</code></td><td>Withdrawal amount, without decimals</td></tr><tr><td>address</td><td><code>string</code></td><td><code>false</code></td><td>Withdrawal address. Please remove the prefix and suffix of the ELF-DID address</td></tr><tr><td>version</td><td><code>PortkeyVersion</code></td><td><code>false</code></td><td><p><code>'v1' | 'v2'</code>.</p><p>Recommend using <code>'v2'</code></p></td></tr></tbody></table>

**Method return value**

<table data-header-hidden><thead><tr><th width="211"></th><th width="131"></th><th></th></tr></thead><tbody><tr><td><strong>Field</strong></td><td><strong>Type</strong></td><td><strong>Remarks</strong></td></tr><tr><td>amountUsd</td><td><code>string</code></td><td>Withdrawal amount in USD</td></tr><tr><td>maxAmount</td><td><code>string</code></td><td>Maximum withdrawal amount</td></tr><tr><td>minAmount</td><td><code>string</code></td><td>Minimum withdrawal amount</td></tr><tr><td>receiveAmount</td><td><code>string</code></td><td>Estimated amount to be received</td></tr><tr><td>receiveAmountUsd</td><td><code>string</code></td><td>Estimated USD received</td></tr><tr><td>limitCurrency</td><td><code>string</code></td><td>Withdrawal crypto</td></tr><tr><td>totalLimit</td><td><code>string</code></td><td>Total limit</td></tr><tr><td>remainingLimit</td><td><code>string</code></td><td>Remaining Limit</td></tr><tr><td>transactionFee</td><td><code>string</code></td><td>Transaction fee</td></tr><tr><td>transactionUnit</td><td><code>string</code></td><td>Transaction fee unit</td></tr><tr><td>aelfTransactionFee</td><td><code>string</code></td><td>Aelf transaction fee</td></tr><tr><td>aelfTransactionUnit</td><td><code>string</code></td><td>Aelf transaction fee unit</td></tr><tr><td>feeUsd</td><td><code>string</code></td><td>Total transaction fees in USD</td></tr><tr><td>expiredTimestamp</td><td><code>string</code></td><td>The expiration time of this response</td></tr></tbody></table>

#### Create a withdrawal order

There are two ways to create an order：

* **Create a withdrawal order, including additional business logic.**

Before generating TransactionRaw, a series of transaction strategies such as balance judgment, allowance judgment, and approval are required, and finally TransactionRaw is generated and submitted to the ETransfer server.This method includes the above series of verification processes.

**Example**

```javascript
import { eTransferCore } from '@etransfer/core';

const result = await eTransferCore.sendWithdrawOrder({
  tokenContractAddress: '',
  endPoint: 'https://xxx.xx',
  symbol: 'USDT',
  decimals: 6,
  amount: '100',
  toAddress: '0x...',
  caContractAddress: '',
  eTransferContractAddress: '',
  caHash: '',
  network: 'ETH',
  chainId: 'AELF',
  managerAddress: '',
  accountAddress: '',
  getSignature: async (ser: any) => {
    // Some code
  },
  tokenContractCallSendMethod: async (ser: any) => {
    // Some code
  },
});
```

**Http Headers**

<table><thead><tr><th width="155">Header</th><th width="104">Type</th><th width="104">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>Authorization</td><td><code>string</code></td><td><code>true</code></td><td><p>The authorization token is the result returned by /connect/token.</p><p>How to acquire: <a href="auth.md">ETransfer SDK Auth</a>.</p></td></tr></tbody></table>

**Method Parameters**

<table><thead><tr><th width="194">Field</th><th width="234">Type</th><th width="104">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>tokenContractAddress</td><td><code>string</code></td><td><code>true</code></td><td>Token contract address</td></tr><tr><td>endPoint</td><td><code>string</code></td><td><code>true</code></td><td>End point url</td></tr><tr><td>symbol</td><td><code>string</code></td><td><code>true</code></td><td>Withdrawal crypto, Get data from eTransferCore.services.getTokenList</td></tr><tr><td>decimals</td><td><code>string | number</code></td><td><code>true</code></td><td>Withdrawal crypto decimals</td></tr><tr><td>amount</td><td><code>string</code></td><td><code>true</code></td><td>Withdrawal amount, without decimals</td></tr><tr><td>accountAddress</td><td><code>string</code></td><td><code>true</code></td><td>Aelf chain account address</td></tr><tr><td>eTransferContractAddress</td><td><code>string</code></td><td><code>true</code></td><td>ETransfer contract address</td></tr><tr><td>toAddress</td><td><code>string</code></td><td><code>true</code></td><td>Withdrawal address</td></tr><tr><td>caContractAddress</td><td><code>string</code></td><td><code>true</code></td><td>Aelf ca contract address</td></tr><tr><td>caHash</td><td><code>string</code></td><td><code>true</code></td><td>User 's ca hash</td></tr><tr><td>network</td><td><code>string</code></td><td><code>true</code></td><td>Withdrawal network, Get data from eTransferCore.services.getNetworkList</td></tr><tr><td>chainId</td><td><code>ChainId</code></td><td><code>true</code></td><td><code>'AELF' | 'tDVV</code>'</td></tr><tr><td>managerAddress</td><td><code>string</code></td><td><code>true</code></td><td>User 's manager address</td></tr><tr><td>getSignature</td><td><code>TGetSignatureFunc</code></td><td><code>true</code></td><td>Get wallet signature method</td></tr><tr><td>tokenContractCallSendMethod</td><td><code>(params: CallContractParams&#x3C;T>, sendOptions?: SendOptions): Promise&#x3C;R &#x26; {transactionId: string;}> | undefined</code></td><td><code>true</code></td><td>Send token contract method</td></tr></tbody></table>

**Method return value**

<table><thead><tr><th width="164">Field</th><th width="119">Type</th><th>Remarks</th></tr></thead><tbody><tr><td>orderId</td><td><code>string</code></td><td>Order id</td></tr><tr><td>transactionId</td><td><code>string</code></td><td>Transaction id. You can use this transactionId to view transaction details in the browser.</td></tr></tbody></table>

* **Only create orders, no additional business logic required.**

This method does not include a series of verification processes.

**Example**

```javascript
import { eTransferCore } from '@etransfer/core';

const result = await eTransferCore.services.createWithdrawOrder({
  network: 'ETH',
  symbol: 'USDT',
  amount: '100',
  fromChainId: 'AELF',
  toAddress: 'withdrawal address',
  rawTransaction: 'transaction raw',
});
```

**Http Headers**

<table><thead><tr><th width="155">Header</th><th width="104">Type</th><th width="104">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>Authorization</td><td><code>string</code></td><td><code>true</code></td><td><p>The authorization token is the result returned by /connect/token.</p><p>How to acquire: <a href="auth.md">ETransfer SDK Auth</a>.</p></td></tr></tbody></table>

**Method Parameters**

<table data-header-hidden><thead><tr><th width="164"></th><th width="118"></th><th width="111"></th><th></th></tr></thead><tbody><tr><td><strong>Field</strong></td><td><strong>Type</strong></td><td><strong>Required</strong></td><td><strong>Remarks</strong></td></tr><tr><td>network</td><td><code>string</code></td><td><code>true</code></td><td>Get data from eTransferCore.services.getNetworkList</td></tr><tr><td>symbol</td><td><code>string</code></td><td><code>true</code></td><td>Get data from eTransferCore.services.getTokenList</td></tr><tr><td>amount</td><td><code>string</code></td><td><code>true</code></td><td>Withdrawal amount, without decimals</td></tr><tr><td>fromChainId</td><td><code>ChainId</code></td><td><code>true</code></td><td><code>'AELF' | 'tDVV'</code></td></tr><tr><td>toAddress</td><td><code>string</code></td><td><code>true</code></td><td>Withdrawal address. Please remove the prefix and suffix of the ELF-DID address</td></tr><tr><td>rawTransaction</td><td><code>string</code></td><td><code>true</code></td><td>Transaction raw</td></tr></tbody></table>

**Method return value**

<table data-header-hidden><thead><tr><th width="167"></th><th width="117"></th><th></th></tr></thead><tbody><tr><td><strong>Field</strong></td><td><strong>Type</strong></td><td><strong>Remarks</strong></td></tr><tr><td>orderId</td><td><code>string</code></td><td>Order id</td></tr><tr><td>transactionId</td><td><code>string</code></td><td>Transaction id. You can use this transactionId to view transaction details in the browser.</td></tr></tbody></table>
