# 💰 Deposit Digital Assets

## Introduction

**Deposit Assets**

Deposit assets from other chains to the aelf chain.

**SDK -** **Deposit Assets**

A deposit address is generated based on the token, network and other information selected by the user. The user transfers crypto to the deposit address, then the ETransfer server will send tokens to the user's aelf chain account.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

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

Acquire the list of assets supported by ETransfer.You can find which assets are supported for deposit and swap.

**Example**

```javascript
import { eTransferCore } from '@etransfer/core';
import { BusinessType } from '@etransfer/types';

const result = await eTransferCore.services.getTokenOption({ type: BusinessType.Deposit });
```

**Http Headers**

<table><thead><tr><th width="155">Header</th><th width="104">Type</th><th width="104">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>Authorization</td><td><code>string</code></td><td><code>true</code></td><td><p>The authorization token is the result returned by /connect/token.</p><p>How to acquire: <a href="auth.md">ETransfer SDK Auth</a>.</p></td></tr></tbody></table>

**Method Parameters**

<table><thead><tr><th width="100">Field</th><th width="159">Type</th><th width="101">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>type</td><td><code>BusinessType</code></td><td><code>true</code></td><td>Business type: <code>'Deposit'</code></td></tr></tbody></table>

**Method return value**

<table><thead><tr><th width="187">Field</th><th width="222">Type</th><th>Remarks</th></tr></thead><tbody><tr><td><code>...TTokenItem</code></td><td><code>Extends TTokenItem</code></td><td>From crypto information</td></tr><tr><td>toTokenList</td><td><code>TToTokenItem[]</code></td><td>To crypto information</td></tr></tbody></table>

**`TTokenItem` type**

<table><thead><tr><th width="187">Field</th><th width="223">Type</th><th>Remarks</th></tr></thead><tbody><tr><td>name</td><td><code>string</code></td><td>Crypto name</td></tr><tr><td>symbol</td><td><code>string</code></td><td>Crypto symbol</td></tr><tr><td>icon</td><td><code>string</code></td><td>Crypto logo url</td></tr><tr><td>contractAddress</td><td><code>string</code></td><td>ETransfer contract address</td></tr><tr><td>decimals</td><td><code>number</code></td><td>Crypto decimals</td></tr></tbody></table>

**`TToTokenItem` type**

<table><thead><tr><th width="191">Field</th><th width="221">Type</th><th>Remarks</th></tr></thead><tbody><tr><td><code>...TTokenItem</code></td><td><code>Extends TTokenItem</code></td><td></td></tr><tr><td>chainIdList</td><td><code>ChainId[]</code></td><td>Supported chain array</td></tr></tbody></table>

#### Get supported networks

Acquire the list of networks supported by ETransfer.You can find which networks are supported for deposit and swap.You can get the basic information and the block confirmations of the network, etc.

**Example**

```javascript
import { eTransferCore } from '@etransfer/core';
import { BusinessType } from '@etransfer/types';

const result = await eTransferCore.services.getNetworkList({
  type: BusinessType.Deposit,
  chainId: 'AELF',
  symbol: 'USDT',
});
```

**Http Headers**

<table><thead><tr><th width="155">Header</th><th width="104">Type</th><th width="104">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>Authorization</td><td><code>string</code></td><td><code>true</code></td><td><p>The authorization token is the result returned by /connect/token.</p><p>How to acquire: <a href="auth.md">ETransfer SDK Auth</a>.</p></td></tr></tbody></table>

**Method Parameters**

<table><thead><tr><th width="117">Field</th><th width="161">Type</th><th width="124">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>type</td><td><code>BusinessType</code></td><td><code>true</code></td><td>Business type: <code>'Deposit'</code></td></tr><tr><td>chainId</td><td><code>ChainId</code></td><td><code>true</code></td><td><code>'AELF' | 'tDVV'</code></td></tr><tr><td>symbol</td><td><code>string</code></td><td><code>false</code></td><td>Get data from eTransferCore.services.getTokenOption</td></tr></tbody></table>

**Method return value**

<table><thead><tr><th width="187">Field</th><th width="172">Type</th><th>Remarks</th></tr></thead><tbody><tr><td>network</td><td><code>string</code></td><td>Network</td></tr><tr><td>name</td><td><code>string</code></td><td>Network name</td></tr><tr><td>multiConfirm</td><td><code>string</code></td><td>Network block confirmations</td></tr><tr><td>multiConfirmTime</td><td><code>string</code></td><td>Network block confirmation time</td></tr><tr><td>contractAddress</td><td><code>string</code></td><td>Network contract address</td></tr><tr><td>explorerUrl</td><td><code>string</code></td><td>Network explorer address</td></tr><tr><td>status</td><td><code>NetworkStatus</code></td><td>Network health status<code>'Health' | 'Congesting' | 'Offline'</code></td></tr></tbody></table>

#### Get deposit address

Acquire the deposit information and deposit address. You can transfer assets to this address, and then your aelf account will receive aelf chain assets.

{% hint style="danger" %}
Please check the deposit tips and minimum deposit limit.
{% endhint %}

**Example**

```javascript
import { eTransferCore } from '@etransfer/core';

const result = await eTransferCore.services.getDepositInfo({
  chainId: 'AELF',
  network: 'ETH',
  symbol: 'USDT',
  toSymbol: 'SGR',
});
```

**Http Headers**

<table><thead><tr><th width="150">Header</th><th width="105">Type</th><th width="108">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>Authorization</td><td><code>string</code></td><td><code>true</code></td><td><p>The authorization token is the result returned by /connect/token.</p><p>How to acquire: <a href="auth.md">ETransfer SDK Auth</a>.</p></td></tr></tbody></table>

**Method Parameters**

<table><thead><tr><th width="150">Field</th><th width="109">Type</th><th width="107">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>chainId</td><td><code>ChainId</code></td><td><code>true</code></td><td><code>'AELF' | 'tDVV'</code></td></tr><tr><td>network</td><td><code>string</code></td><td><code>true</code></td><td>Get data from eTransferCore.services.getNetworkList</td></tr><tr><td>symbol</td><td><code>string</code></td><td><code>false</code></td><td>From crypto, get data from eTransferCore.services.getTokenOption</td></tr><tr><td>toSymbol</td><td><code>string</code></td><td><code>false</code></td><td>To Crypto, get data from eTransferCore.services.getTokenOption</td></tr></tbody></table>

**Method return value**

<table><thead><tr><th width="164">Field</th><th width="205">Type</th><th width="94">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>depositAddress</td><td><code>string</code></td><td><code>true</code></td><td>Deposit address</td></tr><tr><td>minAmount</td><td><code>string</code></td><td><code>true</code></td><td>Minimum deposit amount</td></tr><tr><td>minAmountUsd</td><td><code>string</code></td><td><code>true</code></td><td>Minimum deposit amount in USD</td></tr><tr><td>extraNotes</td><td><code>string[]</code></td><td><code>false</code></td><td>Deposit tips</td></tr><tr><td>extraInfo</td><td><code>TDepositExtraInfo</code></td><td><code>false</code></td><td>Additional deposit information</td></tr></tbody></table>

**`TDepositExtraInfo` type**

<table><thead><tr><th width="164">Field</th><th width="204">Type</th><th>Remarks</th></tr></thead><tbody><tr><td>slippage</td><td><code>string</code></td><td>Deposit slippage</td></tr></tbody></table>
