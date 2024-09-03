# Configuration

## Config Provider

This provider supports you to configure the business environment and the scope of business support, which is one of the means for you to flexibly build ETranfer.

### **Example**

```typescript
import { ETransferConfig } from '@etransfer/ui-react';
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
  
ETransferConfig.setConfig({
  networkType: 'MAINNET', // 'MAINNET' | 'TESTNET'
  etransferUrl: 'etransfer service url',
  etransferAuthUrl: 'etransfer authorization service url' , 
  storage: new Store(),
  authorization: {
    jwt: 'Bearer xxx', // ETransfer authorization token
  },
  depositConfig: {
    defaultDepositToken: 'ELF',
    supportDepositTokens: ['USDT', 'ELF'],
    defaultReceiveToken: 'ELF',
    supportReceiveTokens: ['USDT', 'ELF'],
    defaultChainId: 'tDVW',
    supportChainIds: ['tDVW'],
    defaultNetwork: 'ETH',
    supportNetworks: ['ETH'],
  },
  withdrawConfig: {
    defaultToken: 'ELF',
    supportTokens: ['ELF', 'USDT'],
    defaultChainId: 'AELF',
    supportChainIds: ['tDVW', 'AELF'],
    defaultNetwork: 'BSC',
    supportNetworks: ['ETH', 'BSC'],
  },
});
```

### **Method Parameters**

<table><thead><tr><th width="158">Field</th><th width="140">Type</th><th width="106">Required</th><th>Remarks</th></tr></thead><tbody><tr><td>networkType</td><td>'MAINNET' | 'TESTNET'</td><td>true</td><td>Portkey network type.</td></tr><tr><td>etransferUrl</td><td>string</td><td>true</td><td>ETransfer server URL.See more: ETransfer SDK Configuration.</td></tr><tr><td>etransferAuthUrl</td><td>string</td><td>false</td><td>ETransfer auth server URL.See more: <a href="../configuration.md">ETransfer SDK Configuration</a></td></tr><tr><td>storage</td><td>IStorageSuite</td><td>false</td><td>See more: <a href="../configuration.md">ETransfer SDK Configuration</a></td></tr><tr><td>authorization</td><td>{ jwt : string }<br></td><td>true</td><td>ETransfer auth token.See More: <a href="https://etransfer.gitbook.io/docs/sdk/get-started/auth">ETransfer SDK Auth</a></td></tr><tr><td>depositConfig</td><td><br></td><td>false</td><td>Configuration of the deposit component.</td></tr><tr><td>depositConfig.defaultDepositToken</td><td>string</td><td>false</td><td><p>The deposit token is selected by default when the deposit component is initialized.</p><ul><li>Q: How to configure valid values?</li><li>A: Get value from <code>eTransferCore.services.getTokenOption</code></li></ul></td></tr><tr><td>depositConfig.supportDepositTokens</td><td>string[]</td><td>false</td><td><p>Deposit function optional deposit tokens.</p><ul><li>Q: How to configure valid values?</li><li>A: Get value from <code>eTransferCore.services.getTokenOption</code></li></ul></td></tr><tr><td>depositConfig.defaultReceiveToken</td><td>string</td><td>false</td><td><p>The receive token selected by default when the deposit component is initialized.</p><ul><li>Q: How to configure valid values?</li><li>A: Get value from <code>eTransferCore.services.getTokenOption</code></li></ul></td></tr><tr><td>depositConfig.supportReceiveTokens</td><td>string[]</td><td>false</td><td><p>Deposit function optional receive tokens.</p><ul><li>Q: How to configure valid values?</li><li>A: Get value from <code>eTransferCore.services.getTokenOption</code></li></ul></td></tr><tr><td>depositConfig.defaultChainId</td><td>ChainId</td><td>false</td><td>The aelf chain selected by default when the deposit component is initialized.</td></tr><tr><td>depositConfig.supportChainIds</td><td>ChainId[]</td><td>false</td><td>Deposit function optional chains.</td></tr><tr><td>depositConfig.defaultNetwork</td><td>string</td><td>false</td><td><p>The network selected by default when the deposit component is initialized.</p><ul><li>Q: How to configure valid values?</li><li>A: Get value from <code>eTransferCore.services.getNetworkList</code></li></ul></td></tr><tr><td>depositConfig.supportNetworks<br></td><td>string[]</td><td>false</td><td><p>Deposit function optional networks.</p><ul><li>Q: How to configure valid values?</li><li>A: Get value from <code>eTransferCore.services.getNetworkList</code></li></ul></td></tr><tr><td>withdrawConfig</td><td><br></td><td>false</td><td>Configuration of the withdraw component.</td></tr><tr><td>withdrawConfig.defaultToken</td><td>string</td><td>false</td><td><p>The withdrawal token selected by default when the withdraw component is initialized.</p><ul><li>Q: How to configure valid values?</li><li>A: Get value from <code>eTransferCore.services.getTokenList</code></li></ul></td></tr><tr><td>withdrawConfig.supportTokens</td><td>string[]</td><td>false</td><td><p>Withdrawal function optional tokens.</p><ul><li>Q: How to configure valid values?</li><li>A: Get value from <code>eTransferCore.services.getTokenList</code></li></ul></td></tr><tr><td>withdrawConfig.defaultChainId</td><td>ChainId</td><td>false</td><td>The aelf chain selected by default when the withdraw component is initialized.</td></tr><tr><td>withdrawConfig.supportChainIds</td><td>ChainId[]</td><td>false</td><td>Withdrawal function optional chains.</td></tr><tr><td>withdrawConfig.defaultNetwork</td><td>string</td><td>false</td><td><p>The network selected by default when the withdraw component is initialized.</p><ul><li>Q: How to configure valid values?</li><li>A: Get value from <code>eTransferCore.services.getNetworkList</code></li></ul></td></tr><tr><td>withdrawConfig.supportNetworks</td><td>string[]</td><td>false</td><td><p>Withdrawal function optional networks.</p><ul><li>Q: How to configure valid values?</li><li>A: Get value from <code>eTransferCore.services.getNetworkList</code></li></ul></td></tr></tbody></table>

## Style Provider

If you want to use the ETransfer style, please wrap the `ETransferStyleProvider` and css file.

```typescript
import { ETransferStyleProvider } from '@etransfer/ui-react';
import '@etransfer/ui-react/dist/assets/index.css';

export default function ETransferLayout({ children }: { children: React.ReactNode }) {
  return (
    <ETransferStyleProvider>
      {children}
    </ETransferStyleProvider>
  );
}
```

## Layout Provider

If you want to display global loading, please configure `ETransferLayoutProvider`.

```typescript
import { ETransferLayoutProvider } from '@etransfer/ui-react';

export default function ETransferLayout({ children }: { children: React.ReactNode }) {
  return (
    <ETransferLayoutProvider>
      {children}
    </ETransferLayoutProvider>
  );
}
```

## Deposit Provider

`ETransferDepositProvider` provides a way to pass data through the component tree without having to pass props down manually at every level.

```typescript
import { ComponentStyle, Deposit, ETransferDepositProvider } from '@etransfer/ui-react';

export default function DepositPage() {
  return (
    <ETransferDepositProvider>
      <Deposit componentStyle={ComponentStyle.Mobile} />
    </ETransferDepositProvider>
  );
}
```

### **Method Parameters**

<table data-header-hidden><thead><tr><th width="171"></th><th width="162"></th><th width="109"></th><th></th></tr></thead><tbody><tr><td><strong>Field</strong></td><td><strong>Type</strong></td><td><strong>Required</strong></td><td><strong>Remarks</strong></td></tr><tr><td>componentStyle</td><td>ComponentStyle</td><td>false</td><td>Component style configuration items.<code>ComponentStyle.Mobile</code> is a UI that is better adapted to mobile size.<code>ComponentStyle.Web</code> is a UI that is better adapted to web size.If you want to configure responsiveness, please switch the UI style at the appropriate time.Default is <code>ComponentStyle.Web</code></td></tr></tbody></table>

## Withdraw Provider

`ETransferWithdrawProvider` provides a way to pass data through the component tree without having to pass props down manually at every level.

```typescript
import { ComponentStyle, Withdraw, ETransferWithdrawProvider } from '@etransfer/ui-react';

export default function WithdrawPage() {
  return (
    <ETransferWithdrawProvider>
      <Withdraw componentStyle={ComponentStyle.Mobile} />
    </ETransferWithdrawProvider>
  );
}
```

### **Method Parameters**

<table data-header-hidden><thead><tr><th width="170"></th><th width="159"></th><th width="103"></th><th></th></tr></thead><tbody><tr><td><strong>Field</strong></td><td><strong>Type</strong></td><td><strong>Required</strong></td><td><strong>Remarks</strong></td></tr><tr><td>componentStyle</td><td>ComponentStyle</td><td>false</td><td>Component style configuration items.<code>ComponentStyle.Mobile</code> is a UI that is better adapted to mobile size.<code>ComponentStyle.Web</code> is a UI that is better adapted to web size.If you want to configure responsiveness, please switch the UI style at the appropriate time.Default is <code>ComponentStyle.Web</code></td></tr></tbody></table>



