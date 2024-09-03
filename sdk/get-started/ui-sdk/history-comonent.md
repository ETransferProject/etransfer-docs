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

See More: [Installation | ETransfer](https://etransfer.gitbook.io/docs/sdk/get-started/installation)

```bash
npm install @etransfer/ui-react
# OR
yarn add @etransfer/ui-react
```

### Config

For the `ETransferConfig`, `ETransferStyleProvider` configuration used in the following examples, please refer to the [ETransfer UI SDK Config](configuration.md)

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
        />
      </ETransferLayoutProvider>
    </ETransferStyleProvider>
  );
}
```

#### Component properties

<table data-header-hidden><thead><tr><th width="134"></th><th width="128"></th><th width="107"></th><th></th></tr></thead><tbody><tr><td><strong>Field</strong></td><td><strong>Type</strong></td><td><strong>Required</strong></td><td><strong>Remarks</strong></td></tr><tr><td>className</td><td>string</td><td>false</td><td>The additional class to History.</td></tr><tr><td>componentStyle</td><td>ComponentStyle<br></td><td>false</td><td>Component style configuration items.<code>ComponentStyle.Mobile</code> is a UI that is better adapted to mobile size.<code>ComponentStyle.Web</code> is a UI that is better adapted to web size.If you want to configure responsiveness, please switch the UI style at the appropriate time.Default is <code>ComponentStyle.Web</code></td></tr><tr><td>isUnreadHistory</td><td>boolean</td><td>false</td><td>Does the user have unread messages</td></tr><tr><td>isShowMobilePoweredBy</td><td>boolean</td><td>false</td><td>Whether to display the mobile <strong>Powered By ETransfer</strong> logo.</td></tr></tbody></table>

### Notes

* Ensure that the network configuration (`networkType`) , service URL (`etransferUrl`) and authorization (`jwt`) are accurate.
* Use a valid JWT token to ensure proper functionality.
* To get `ETransferConfig authorization.jwt`, you can read [ETransfer SDK Auth](../auth.md)

#### More Example

For more details and use cases, check out the [github example code](https://github.com/ETransferProject/etransfer-toolkit/blob/master/packages/example/src/app/history/page.tsx).\


## Contact Us

For any questions, please reach out to **contact@etransfer.exchange**.\


