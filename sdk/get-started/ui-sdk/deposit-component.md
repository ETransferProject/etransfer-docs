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
* **Notification:** You can see the processing transaction tip and the transaction completion notification.

<figure><img src="../../../.gitbook/assets/image (2) (1).png" alt="" width="371"><figcaption><p>ComponentStyle.Mobile</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>ComponentStyle.Web</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (16).png" alt="" width="375"><figcaption><p>Processing Transaction tip</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (17).png" alt="" width="352"><figcaption><p>Chrome notification</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (18).png" alt="" width="332"><figcaption><p>Transaction completion notifications</p></figcaption></figure>

## How to use

### Installation

See More: [Installation | ETransfer](../installation.md)

```bash
npm install @etransfer/ui-react
# OR
yarn add @etransfer/ui-react
```

### Config

For the `ETransferConfig`, `ETransferStyleProvider` ,`ETransferLayoutProvider` and `ETransferDepositProvider` configuration used in the following examples, please refer to the [ETransfer UI SDK Config](configuration.md)

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
    etransferAuthUrl: 'etransfer authorization service url',
    etransferSocketUrl: 'etransfer socket service url',
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
            isListenNoticeAuto={true}
            isShowProcessingTip={true}
            onClickProcessingTip={() => {
              // your logic
            }}
          />
        </ETransferDepositProvider>
      </ETransferLayoutProvider>
    </ETransferStyleProvider>
  );
}
```

#### Component properties

<table data-header-hidden><thead><tr><th width="171"></th><th width="121"></th><th width="100"></th><th></th></tr></thead><tbody><tr><td><strong>Field</strong></td><td><strong>Type</strong></td><td><strong>Required</strong></td><td><strong>Remarks</strong></td></tr><tr><td>containerClassName</td><td><code>string</code></td><td><code>false</code></td><td>The additional class to Deposit.</td></tr><tr><td>className</td><td><code>string</code></td><td><code>false</code></td><td>The additional class to Deposit body.</td></tr><tr><td>componentStyle</td><td><code>ComponentStyle</code><br></td><td><code>false</code></td><td><p>Component style configuration items.</p><p><code>ComponentStyle.Mobile</code> is a UI that is better adapted to mobile size.</p><p><code>ComponentStyle.Web</code> is a UI that is better adapted to web size.</p><p>If you want to configure responsiveness, please switch the UI style at the appropriate time.</p><p>Default is <code>ComponentStyle.Web</code></p></td></tr><tr><td>isShowErrorTip</td><td><code>boolean</code></td><td><code>false</code></td><td>Whether to automatically pop up error prompt.</td></tr><tr><td>isShowMobilePoweredBy</td><td><code>boolean</code></td><td><code>false</code></td><td>Whether to display the mobile <strong>Powered By ETransfer</strong> logo.</td></tr><tr><td>isListenNoticeAuto</td><td><code>boolean</code></td><td><code>false</code></td><td><p>Whether to establish a socket connection to listen for deposit transaction notifications.</p><p>The default value is <code>true</code>.</p></td></tr><tr><td>isShowProcessingTip</td><td><code>boolean</code></td><td><code>false</code></td><td><p>Whether to display a prompt for ongoing deposit transactions.</p><p>The default value is <code>true</code>.</p></td></tr><tr><td>onClickProcessingTip</td><td><code>()=>void</code></td><td><code>false</code></td><td>The click event for the processing transaction tip.</td></tr></tbody></table>

#### Notes

* Ensure that the network configuration (`networkType`) , service URL (`etransferUrl`) , authorization URL (`etransferAuthUrl`) , socket URL (`etransferSocketUrl`) and authorization (`jwt`) are accurate.
* Use a valid JWT token to ensure proper functionality.
* To get `ETransferConfig authorization.jwt`, you can read [ETransfer SDK Auth](../auth.md)

#### More Example

For more details and use cases, check out the [github example code](https://github.com/ETransferProject/etransfer-toolkit/blob/master/packages/example/src/app/deposit/page.tsx).\


## Contact Us

For any questions, please reach out to **contact@etransfer.exchange**.

