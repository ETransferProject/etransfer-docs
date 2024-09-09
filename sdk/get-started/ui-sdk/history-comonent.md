# History Comonent

## Introduction

If you want to quickly access the querying history function, please use this UI component. You will get the same UI display and querying historical records function as the [ETransfer app](https://app.etransfer.exchange).

### Feature

#### History functions and UIs are as follows:

* You can view transaction history.
* You can filter transaction records by transaction type, status, and date.
* You can view more transaction details by entering your address and transaction hash.

<figure><img src="../../../.gitbook/assets/image (3).png" alt="" width="375"><figcaption><p>ComponentStyle.Mobile</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption><p>ComponentStyle.Web</p></figcaption></figure>

## How to use

### Installation

See More: [Installation | ETransfer](../installation.md)

```bash
npm install @etransfer/ui-react
# OR
yarn add @etransfer/ui-react
```

### Config

For the `ETransferConfig`, `ETransferStyleProvider`, `ETransferLayoutProvider` configuration used in the following examples, please refer to the [ETransfer UI SDK Config](configuration.md)

### Example

```typescript
import React from 'react';
import {
  ComponentStyle,
  History,
  ETransferConfig,
  ETransferLayoutProvider
  ETransferStyleProvider,
} from '@etransfer/ui-react';
import '@etransfer/ui-react/dist/assets/index.css';

export default function ETransferLayout({ children }: { children: React.ReactNode }) {
  ETransferConfig.setConfig({
    networkType: 'MAINNET', // 'MAINNET' | 'TESTNET'
    etransferUrl: 'etransfer service url',
    etransferAuthUrl: 'etransfer authorization service url',
    authorization: {
      jwt: 'Bearer xxx', // ETransfer authorization token
    },
  });

  return (
    <ETransferStyleProvider>
     <ETransferLayoutProvider>
        <History
          className={'xxx-history'}
          componentStyle={ComponentStyle.Mobile}
          isUnreadHistory={false}
          isShowMobilePoweredBy={true}
          onClickHistoryItem={(id:string) => {
            // your logic
          }}
        />
      </ETransferLayoutProvider>
    </ETransferStyleProvider>
  );
}
```

#### Component properties

<table data-header-hidden><thead><tr><th width="134"></th><th width="128"></th><th width="107"></th><th></th></tr></thead><tbody><tr><td><strong>Field</strong></td><td><strong>Type</strong></td><td><strong>Required</strong></td><td><strong>Remarks</strong></td></tr><tr><td>className</td><td><code>string</code></td><td><code>false</code></td><td>The additional class to History.</td></tr><tr><td>componentStyle</td><td><code>ComponentStyle</code><br></td><td><code>false</code></td><td><p>Component style configuration items.</p><p><code>ComponentStyle.Mobile</code> is a UI that is better adapted to mobile size.</p><p><code>ComponentStyle.Web</code> is a UI that is better adapted to web size.</p><p>If you want to configure responsiveness, please switch the UI style at the appropriate time.</p><p>Default is <code>ComponentStyle.Web</code></p></td></tr><tr><td>isUnreadHistory</td><td><code>boolean</code></td><td><code>false</code></td><td>Does the user have unread messages</td></tr><tr><td>isShowMobilePoweredBy</td><td><code>boolean</code></td><td><code>false</code></td><td>Whether to display the mobile <strong>Powered By ETransfer</strong> logo.</td></tr><tr><td>onClickHistoryItem</td><td><code>(id:string)=void</code></td><td><code>false</code></td><td><p>The click event for the history item.</p><p>id: transaction order ID.</p><p>You can use this id and <code>eTransferCore.services.getRecordDetail('orderId')</code> to get more infomations.</p></td></tr></tbody></table>

### Notes

* Ensure that the network configuration (`networkType`) , service URL (`etransferUrl`) , authorization URL (`etransferAuthUrl`) and authorization (`jwt`) are accurate.
* Use a valid JWT token to ensure proper functionality.
* To get `ETransferConfig authorization.jwt`, you can read [ETransfer SDK Auth](../auth.md)

#### More Example

If you want to use the `History` and `TransferDetail` components together, please refer to the [ETransfer UI SDK Transfer Detail Comonent](transferdetail-component.md) and [github example code](https://github.com/ETransferProject/etransfer-toolkit/blob/master/packages/example/src/app/history/page.tsx).\


## Contact Us

For any questions, please reach out to **contact@etransfer.exchange**.\


