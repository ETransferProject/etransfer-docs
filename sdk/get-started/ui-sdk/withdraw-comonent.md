# Withdraw Comonent

Introduction

If you want to quickly access the ETransfer withdrawal function, please use this UI component. You will get the same UI display and withdrawal function as the [ETransfer app](https://app.etransfer.exchange).

### Feature

#### Withdrawal functions and UIs are as follows:

* **Select chain:** Select the aelf chain from which you will withdraw tokens.
* **Select token**: Choose the token you wish to withdraw.
* **Input address:** Enter the address where you want the tokens to be delivered.
* **Select network:** Select the network where you want the tokens to be delivered.
* **Input amount:** Enter the amount of tokens you wish to withdraw.
* **Estimated received:** After entering the above information, detailed withdrawal information will be automatically retrieved. You will see the estimated amount received, fees, and gas costs.
* **Complete the withdrawal:** Click the _Withdraw_ button and follow the prompts to authorize the withdrawal, and you can complete the withdrawal.

<figure><img src="../../../.gitbook/assets/image.png" alt="" width="374"><figcaption><p>ComponentStyle.Mobile</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption><p>ComponentStyle.Web</p></figcaption></figure>

## How to use

### Installation

See More: [Installation | ETransfer](https://etransfer.gitbook.io/docs/sdk/get-started/installation)

```bash
npm install @etransfer/ui-react
# OR
yarn add @etransfer/ui-react
```

### Config

For the `ETransferConfig`, `ETransferStyleProvider` and `ETransferWithdrawProvider` configuration used in the following examples, please refer to the [ETransfer UI SDK Config](configuration.md)

### Example

```typescript
import React from 'react';
import {
  ComponentStyle,
  Withdraw,
  ETransferConfig,
  ETransferWithdrawProvider,
  ETransferLayoutProvider
  ETransferStyleProvider,
} from '@etransfer/ui-react';
import '@etransfer/ui-react/dist/assets/index.css';

export default function ETransferLayout({ children }: { children: React.ReactNode }) {
  ETransferConfig.setConfig({
    networkType: 'MAINNET', // 'MAINNET' | 'TESTNET'
    etransferUrl: 'etransfer service url',
    authorization: {
      jwt: 'Bearer xxx', // ETransfer authorization token
    },
  });

  return (
    <ETransferStyleProvider>
     <ETransferLayoutProvider>
        <ETransferWithdrawProvider>
          <Withdraw
            className={'xxx-withdraw'}
            chainClassName={'xxx-withdraw-chain'}
            fromClassName={'xxx-withdraw-from'}
            componentStyle={ComponentStyle.Mobile}
            isShowErrorTip={true}
            isShowMobilePoweredBy={false}
          />
        </ETransferWithdrawProvider>
      </ETransferLayoutProvider>
    </ETransferStyleProvider>
  );
}
```

#### Component properties

<table data-header-hidden><thead><tr><th width="150"></th><th width="107"></th><th width="82"></th><th></th></tr></thead><tbody><tr><td><strong>Field</strong></td><td><strong>Type</strong></td><td><strong>Required</strong></td><td><strong>Remarks</strong></td></tr><tr><td>className</td><td>string</td><td>false</td><td>The additional class to Withdraw.</td></tr><tr><td>chainClassName</td><td>string</td><td>false</td><td>The additional class to SelectChain.</td></tr><tr><td>fromClassName</td><td>string</td><td>false</td><td>The additional class to WithdrawFrom.</td></tr><tr><td>componentStyle</td><td>ComponentStyle<br></td><td>false</td><td>Component style configuration items.<code>ComponentStyle.Mobile</code> is a UI that is better adapted to mobile size.<code>ComponentStyle.Web</code> is a UI that is better adapted to web size.If you want to configure responsiveness, please switch the UI style at the appropriate time.Default is <code>ComponentStyle.Web</code></td></tr><tr><td>isShowErrorTip</td><td>boolean</td><td>true</td><td>Whether to automatically pop up error prompt.</td></tr><tr><td>isShowMobilePoweredBy</td><td>boolean</td><td>false</td><td>Whether to display the mobile <strong>Powered By ETransfer</strong> logo.</td></tr></tbody></table>

### Notes

* Ensure that the network configuration (`networkType`) , service URL (`etransferUrl`) and authorization (`jwt`) are accurate.
* Use a valid JWT token to ensure proper functionality.
* To get `ETransferConfig authorization.jwt`, you can read [ETransfer SDK Auth](../auth.md)

#### More Example

For more details and use cases, check out the [github example code](https://github.com/ETransferProject/etransfer-toolkit/blob/master/packages/example/src/app/withdraw/page.tsx).\


## Contact Us

For any questions, please reach out to **contact@etransfer.exchange**.\
