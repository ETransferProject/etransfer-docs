# TransferDetail Component

## Introduction

If you want to quickly integrate the transaction details viewing feature, please use this UI component. You will get the same UI display and querying historical records function as the [ETransfer app](https://app.etransfer.exchange).

### Feature

#### Transfer Detail functions and UIs are as follows:

* Display transaction steps and status.
* Show transaction hash, address, token and amount.
* Update the transaction progress in real-time while staying on the page.

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

## How to use

### Installation

See More: [Installation | ETransfer](../installation.md)

```bash
npm install @etransfer/ui-react
# OR
yarn add @etransfer/ui-react
```

### Config

For the `ETransferConfig`, `ETransferStyleProvider` ,`ETransferLayoutProvider` configuration used in the following examples, please refer to the [ETransfer UI SDK configuration](configuration.md).

### Example

```typescript
import React from 'react';
import {
  ComponentStyle,
  TransferDetail,
  ETransferConfig,
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
        <TransferDetail
          className={'xxx-transfer-detail'}
          componentStyle={ComponentStyle.Mobile} // or ComponentStyle.Web
          orderId={'detailId'}
          isShowBackElement={true}
          isShowMobilePoweredBy={false}
          onBack={() => {
            // your logic
          }}
        />
      </ETransferLayoutProvider>
    </ETransferStyleProvider>
  );
}
```

#### Component properties

<table data-header-hidden><thead><tr><th width="152"></th><th width="121"></th><th width="106"></th><th></th></tr></thead><tbody><tr><td><strong>Field</strong></td><td><strong>Type</strong></td><td><strong>Required</strong></td><td><strong>Remarks</strong></td></tr><tr><td>className</td><td>string</td><td>false</td><td>The additional class to TransferDetail.</td></tr><tr><td>componentStyle</td><td>ComponentStyle<br></td><td>false</td><td><p>Component style configuration items.</p><p><code>ComponentStyle.Mobile</code> is a UI that is better adapted to mobile size.</p><p><code>ComponentStyle.Web</code> is a UI that is better adapted to web size.</p><p>If you want to configure responsiveness, please switch the UI style at the appropriate time.</p><p>Default is <code>ComponentStyle.Web</code></p></td></tr><tr><td>orderId</td><td>string</td><td>true</td><td>Transaction order ID.</td></tr><tr><td>isShowBackElement</td><td>boolean</td><td>false</td><td><p>Whether to display the back element.</p><p>Default is <code>true</code>.</p></td></tr><tr><td>isShowMobilePoweredBy</td><td>boolean</td><td>false</td><td>Whether to display the mobile <strong>Powered By ETransfer</strong> logo.</td></tr><tr><td>onBack</td><td>()=void</td><td>false</td><td>The click event for the back icon.</td></tr></tbody></table>

### Notes

* Ensure that the network configuration (`networkType`) , service URL (`etransferUrl`) , authorization URL (`etransferAuthUrl`) and authorization (`jwt`) are accurate.
* Use a valid JWT token to ensure proper functionality.
* To get `ETransferConfig authorization.jwt`, you can read [ETransfer SDK Auth](../auth.md)

#### More Example

If you want to use the `History` and `TransferDetail` components together, please refer to the [ETransfer UI SDK History Component](history-comonent.md) and [github example code](https://github.com/ETransferProject/etransfer-toolkit/blob/master/packages/example/src/app/history/page.tsx) .\


## Contact Us

For any questions, please reach out to **contact@etransfer.exchange**.\
\
