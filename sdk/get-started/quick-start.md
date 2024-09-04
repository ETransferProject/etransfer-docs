# ⌨️ Quick Start

## Installation

{% content-ref url="installation.md" %}
[installation.md](installation.md)
{% endcontent-ref %}

## Demo

{% embed url="https://github.com/ETransferProject/etransfer-toolkit/tree/master/packages/example" %}

## How to use

For the configuration items used in the following examples, please refer to:

{% content-ref url="configuration.md" %}
[configuration.md](configuration.md)
{% endcontent-ref %}

### Init the ETransferCore instance

```javascript
import { eTransferCore } from '@etransfer/core';
import { IStorageSuite } from '@etransfer/types';

class Store implements IStorageSuite {
  async getItem(key: string) {
    return localStorage.getItem(key);
  }
  async setItem(key: string, value: string) {
    return localStorage.setItem(key, value);
  }
  async removeItem(key: string) {
    return localStorage.removeItem(key);
  }
}

eTransferCore.init({
  etransferUrl: 'etransfer service url',
  etransferAuthUrl: 'etransfer authorization service url' , 
  storage: new Store()
});
```

### Features

#### Acquire authorization token

```javascript
import { eTransferCore } from '@etransfer/core';

const result = await eTransferCore.services.getAuthToken(
  {
    chain_id: 'AELF', // AELF or tDVV
    ca_hash: 'user ca hash',
    managerAddress: 'user manager address',
    pubkey: 'user account pubkey',
    plain_text: 'signed text',
    signature: 'user signature',
    version: PortkeyVersion.v2,
  },
  { baseURL: 'etransfer auth url' },
);
```

#### Check the transaction status of an EOA address

```typescript
import { eTransferCore } from '@etransfer/core';

const result = await eTransferCore.services.checkEOARegistration(
  {
    address: 'your account address',
  }
);
```

#### Acquire supported cryptos

```javascript
import { eTransferCore } from '@etransfer/core';

// Acquire deposit cryptos
const result = await eTransferCore.services.getTokenOption({ type: 'Deposit' });

// Acquire withdraw cryptos
const result = await eTransferCore.services.getTokenList({
  type: 'Withdraw',
  chainId: 'AELF', // or 'tDVV'
});
```

#### Acquire token price

<pre class="language-typescript"><code class="lang-typescript">import { eTransferCore } from '@etransfer/core';

// Get the price of a token
const result = await eTransferCore.services.getTokenPrices({ symbols: 'USDT' });

// Get the prices of several tokens
const result = await eTransferCore.services.getTokenPrices({
<strong>  symbols: 'USDT,SGR-1,ELF',
</strong><strong>});
</strong></code></pre>

#### Acquire supported networks

```javascript
import { eTransferCore } from '@etransfer/core';

const result = await eTransferCore.services.getNetworkList({
  type: 'Deposit', // or 'Withdraw'
  chainId: 'AELF', // or 'tDVV'
  symbol: 'USDT', // Get data from eTransferCore.services[getTokenOption|getTokenList]
});
```

#### Acquire deposit information

```javascript
import { eTransferCore } from '@etransfer/core';

const result = await eTransferCore.services.getDepositInfo({
  chainId: 'AELF', // or 'tDVV'
  network: 'ETH', // get data from eTransferCore.services.getNetworkList
  symbol: 'USDT', // get data from eTransferCore.services.getTokenOption
  toSymbol: 'USDT', // get data from eTransferCore.services.getTokenOption
});
```

#### Calculate crypto exchange rates

```javascript
import { eTransferCore } from '@etransfer/core';

const result = await eTransferCore.services.getDepositCalculate({
  fromSymbol: 'USDT', // get data from eTransferCore.services.getTokenOption
  fromAmount: '100', // without decimals
  toSymbol: 'USDT', // get data from eTransferCore.services.getTokenOption
  toChainId: 'AELF', // or 'tDVV'
});
```

#### Acquire withdraw information

```javascript
import { eTransferCore } from '@etransfer/core';
import { PortkeyVersion } from '@etransfer/types';

const result = await eTransferCore.services.getWithdrawInfo({
  chainId: 'AELF', // or 'tDVV'
  network: 'ETH', // get data from eTransferCore.services.getNetworkList
  symbol: 'USDT', // get data from eTransferCore.services.getTokenList
  amount: '100', // withdrawal amount, without decimals
  address: 'withdrawal address', // Please remove the prefix and suffix of the ELF-DID address
  version: PortkeyVersion.v2,
});
```

#### Create withdraw order

```javascript
import { eTransferCore } from '@etransfer/core';

const result = await eTransferCore.services.createWithdrawOrder({
  network: 'ETH', // get data from eTransferCore.services.getNetworkList
  symbol: 'USDT', // get data from eTransferCore.services.getTokenList
  amount: '100', // withdrawal amount, without decimals
  fromChainId: 'AELF', // or 'tDVV'
  toAddress: 'withdrawal address', // Please remove the prefix and suffix of the ELF-DID address
  rawTransaction: rawTransaction,
});
```

#### Acquire transaction records

```javascript
import { eTransferCore } from '@etransfer/core';

const result = await eTransferCore.services.getRecordsList({
  type: 0, // ALL = 0, Deposits = 1, Withdraws = 2
  status: 0, // ALL = 0, Processing = 1, Succeed = 2, Failed = 3
  skipCount: 0,
  maxResultCount: 100,
});
```

#### Acquire transaction details

```typescript
import { eTransferCore } from '@etransfer/core';

const result = await eTransferCore.services.getRecordDetail('orderId');
```

#### If there are any unread messages

```javascript
import { eTransferCore } from '@etransfer/core';

const result = await eTransferCore.services.getRecordStatus();
```
