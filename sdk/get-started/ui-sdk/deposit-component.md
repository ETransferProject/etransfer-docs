# Deposit Component

## Introduction

If you want to quickly access the ETransfer deposit function, please use this UI component. You will get the same UI display and deposit function as the [ETransfer app](https://app.etransfer.exchange).

### Feature

#### Deposit functions and UIs are as follows:

* **Select tokens:** Select the deposit token and the received token.
* **Select networks:** Select the from network and the to network.
* **Calculator:** If the deposit token is different from the received token, the calculator function will be displayed. You can use the calculator to calculate the exchange rate and estimate how many tokens you will receive.
* **Minimum deposit limit:** You will see the minimum deposit limit. The amount you deposit needs to be greater than the minimum value.
* **From network contract address:** You can see the from network contract address.
* **Deposit tips:** You will see the deposit tips and you can read these tips to answer your operational questions.
* **Automatically obtain the deposit address:** After you select the tokens and networks, you will receive the deposit QR code and deposit address.
* **Deposit assets:** You can scan the QR code or copy the deposit address to complete the deposit.

<figure><img src="../../../.gitbook/assets/image (2).png" alt="" width="186"><figcaption><p>ComponentStyle.Mobile</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (1).png" alt="" width="563"><figcaption><p>ComponentStyle.Web</p></figcaption></figure>

## How to use

### Installation

See More: [Installation | ETransfer](https://etransfer.gitbook.io/docs/sdk/get-started/installation)

```bash
npm install @etransfer/ui-react
# OR
yarn add @etransfer/ui-react
```

### Config

For the `ETransferConfig`, `ETransferStyleProvider` and `ETransferDepositProvider` configuration used in the following examples, please refer to the [ETransfer UI SDK Config](configuration.md)

### Example

```typescript
import React from 'react';
import {
  ComponentStyle,
  Deposit,
  ETransferConfig,
  ETransferDepositProvider,
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
        <ETransferDepositProvider>
          <Deposit
            containerClassName={'xxx-deposit'}
            className={'xxx-deposit-body'}
            componentStyle={ComponentStyle.Mobile}
            isShowErrorTip={true}
            isShowMobilePoweredBy={false}
          />
        </ETransferDepositProvider>
      </ETransferLayoutProvider>
    </ETransferStyleProvider>
  );
}
```

#### Component properties

<table data-header-hidden><thead><tr><th width="171"></th><th width="109"></th><th width="100"></th><th></th></tr></thead><tbody><tr><td><strong>Field</strong></td><td><strong>Type</strong></td><td><strong>Required</strong></td><td><strong>Remarks</strong></td></tr><tr><td>containerClassName</td><td>string</td><td>false</td><td>The additional class to Deposit.</td></tr><tr><td>className</td><td>string</td><td>false</td><td>The additional class to Deposit body.</td></tr><tr><td>componentStyle</td><td>ComponentStyle<br></td><td>false</td><td>Component style configuration items.<code>ComponentStyle.Mobile</code> is a UI that is better adapted to mobile size.<code>ComponentStyle.Web</code> is a UI that is better adapted to web size.If you want to configure responsiveness, please switch the UI style at the appropriate time.Default is <code>ComponentStyle.Web</code></td></tr><tr><td>isShowErrorTip</td><td>boolean</td><td>true</td><td>Whether to automatically pop up error prompt.</td></tr><tr><td>isShowMobilePoweredBy</td><td>boolean</td><td>false</td><td>Whether to display the mobile <strong>Powered By ETransfer</strong> logo.</td></tr></tbody></table>

#### Notes

* Ensure that the network configuration (`networkType`) , service URL (`etransferUrl`) and authorization (`jwt`) are accurate.
* Use a valid JWT token to ensure proper functionality.
* To get `ETransferConfig authorization.jwt`, you can read [ETransfer SDK Auth](../auth.md)

#### More Example

For more details and use cases, check out the [github example code](https://github.com/ETransferProject/etransfer-toolkit/blob/master/packages/example/src/app/deposit/page.tsx).\


## Contact Us

For any questions, please reach out to **contact@etransfer.exchange**.

