# ETransferContent Comonent

## Introduction

If you want to quickly access the deposit, withdrawal and querying history functions, please use this UI component. You will get the same UI display and functions as the [ETransfer app](https://app.etransfer.exchange).\


### Feature

#### ETransferContent's functions and UIs are as follows:

* **Deposit assets:** The functionality is the same as [ETransfer UI SDK Deposit Component](deposit-component.md)
* **Withdrawal assets:** The functionality is the same as [ETransfer UI SDK Withdraw Comonent](withdraw-comonent.md)
* **Querying historical records:** The functionality is the same as [ETransfer UI SDK History Comonent](history-comonent.md)
* **Unread message reminder:** If you have unread transaction records, an unread record reminder will be displayed on the sidebar or navigation menu.
* **Display User account address:** Display the user's account address in the navigation header. You can also choose to hide it.
* **Jump to the ETransfer official website:** Click the logo in the navigation header to jump to the ETransfer official website.

<figure><img src="../../../.gitbook/assets/image (6).png" alt="" width="167"><figcaption><p>Deposit - ComponentStyle.Mobile</p></figcaption></figure>

<div align="center">

<figure><img src="../../../.gitbook/assets/image (7).png" alt="" width="167"><figcaption><p>Withdraw - ComponentStyle.Mobile</p></figcaption></figure>

</div>

<figure><img src="../../../.gitbook/assets/image (8).png" alt="" width="167"><figcaption><p>History - ComponentStyle.Mobile</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (9).png" alt="" width="563"><figcaption><p>Deposit - ComponentStyle.Web</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (10).png" alt="" width="563"><figcaption><p>Withdraw - ComponentStyle.Web</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (11).png" alt="" width="563"><figcaption><p>History - ComponentStyle.Web</p></figcaption></figure>

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
  ETransferContent,
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
        <ETransferContent
          className={'xxx-etransfer'}
          componentStyle={ComponentStyle.Mobile}
          isCanClickHeaderLogo={true}
          isShowHeaderUserProfile={true}
          isShowMobileFooter={false}
          isShowErrorTip={true}
          onClickHeaderLogo={() => {
            console.log('your function');
          }}
        />
      </ETransferLayoutProvider>
    </ETransferStyleProvider>
  );
}
```

#### Component properties

<table data-header-hidden><thead><tr><th width="137"></th><th width="107"></th><th width="103"></th><th></th></tr></thead><tbody><tr><td><strong>Field</strong></td><td><strong>Type</strong></td><td><strong>Required</strong></td><td><strong>Remarks</strong></td></tr><tr><td>className</td><td>string</td><td>false</td><td>The additional class to ETransferContent.</td></tr><tr><td>componentStyle</td><td>ComponentStyle<br></td><td>false</td><td>Component style configuration items.<code>ComponentStyle.Mobile</code> is a UI that is better adapted to mobile size.<code>ComponentStyle.Web</code> is a UI that is better adapted to web size.If you want to configure responsiveness, please switch the UI style at the appropriate time.Default is <code>ComponentStyle.Web</code></td></tr><tr><td>isCanClickHeaderLogo</td><td>boolean</td><td>false</td><td>Is the logo in the header clickable?Default is <code>true</code></td></tr><tr><td>isShowHeaderUserProfile</td><td>boolean</td><td>false</td><td>Whether to display user addresses in the mobile footer.Default is <code>true</code></td></tr><tr><td>isShowMobileFooter</td><td>boolean</td><td>false</td><td>Whether to display social media links in the mobile footer.Default is <code>false</code></td></tr><tr><td>isShowErrorTip</td><td>boolean</td><td>false</td><td>Whether to automatically pop up error prompt.Default is <code>true</code></td></tr><tr><td>onClickHeaderLogo</td><td>function</td><td>false</td><td>Click event of the page header logo.The default method is to open <a href="http://etransfer.exchange">ETransfer Official Website</a> in a new browser tab.</td></tr></tbody></table>

#### Notes

* Ensure that the network configuration (`networkType`) , service URL (`etransferUrl`) and authorization (`jwt`) are accurate.
* Use a valid JWT token to ensure proper functionality.
* To get `ETransferConfig authorization.jwt`, you can read [ETransfer SDK Auth](../auth.md)

#### More Example

For more details and use cases, check out the [github example code](https://github.com/ETransferProject/etransfer-toolkit/blob/master/packages/example/src/app/etransfer/page.tsx).\


## Contact Us

For any questions, please reach out to **contact@etransfer.exchange**.\


