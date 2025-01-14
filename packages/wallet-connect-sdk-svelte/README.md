# WalletConnect SDK React Documentation

Welcome to the **WalletConnect SDK React** guide. This documentation is designed to help developers integrate the WalletConnect SDK React library seamlessly into their applications, providing a comprehensive walkthrough of setup, usage, and advanced features.

---

## Table of Contents

- [Introduction](#introduction)
- [Installation](#installation)
- [Setup](#setup)
  - [Creating a WalletConnect Project](#creating-a-walletconnect-project)
  - [Initializing the SDK](#initializing-the-sdk)
  - [Wrapping WalletConnectProvider](#wrapping-walletconnectprovider)
  - [Using the WalletConnect Instance](#using-the-walletconnect-instance)
- [Advanced Usage](#advanced-usage)
  - [Metadata Customization](#metadata-customization)
  - [Debugging Tips](#debugging-tips)
  - [Integration Best Practices](#integration-best-practices)
- [Examples](#examples)
- [Additional Resources](#additional-resources)
  - [Community Support](#community-support)
  - [Changelog](#changelog)

---

## Introduction

The **WalletConnect SDK React** by EpicChain Labs is a robust solution for building secure and user-friendly wallet integrations in React applications. Whether you're creating DeFi platforms, NFT marketplaces, or blockchain-enabled applications, this SDK simplifies the connection process while offering a customizable and scalable approach to wallet connectivity.

With features like automated session management, customizable metadata, and a user-centric design, this SDK ensures a seamless user experience while empowering developers to focus on their application's core functionality.

---

## Installation

Installing the SDK is the first step toward integrating WalletConnect functionality into your React application. The SDK supports both NPM and Yarn package managers, making it compatible with various development environments.

### Using NPM

```bash
npm install @epicchain/wallet-connect-sdk-react
```

### Using YARN

```bash
yarn add @epicchain/wallet-connect-sdk-react
```

### Prerequisites

Ensure your project environment meets the following requirements:

- **React Version**: v16.8 or higher.
- **Node.js Version**: v14 or higher.
- **Package Manager**: NPM v7+ or Yarn v1.22+.
- **Network Access**: Ensure your system can connect to `wss://relay.walletconnect.com`.

---

## Setup

### Creating a WalletConnect Project

To integrate WalletConnect, you first need to set up a project on the official WalletConnect platform. Follow these steps:

1. **Visit WalletConnect**: Navigate to the [WalletConnect website](https://walletconnect.com/).
2. **Sign Up/Log In**: Register for an account if you don't already have one.
3. **Create a New Project**:
   - Click on "Create Project."
   - Fill in details such as **Project Name**, **Description**, **Icon**, and other relevant fields.
4. **Obtain Project ID**: Once the project is created, copy the **Project ID** from your dashboard. This will be required for SDK initialization.

### Initializing the SDK

Before using the SDK in your application, initialize it with your project details and custom metadata:

```jsx
import { WalletConnectProvider } from "@epicchain/wallet-connect-sdk-react";

const wcOptions = {
    projectId: '<your wc project id>', // The unique project ID from WalletConnect
    relayUrl: 'wss://relay.walletconnect.com', // WalletConnect relay server URL
    metadata: {
        name: 'MyApplicationName', // Application name to display in wallets
        description: 'My Application description', // Description shown in wallets
        url: 'https://myapplicationdescription.app/', // Application website URL
        icons: ['https://myapplicationdescription.app/myappicon.png'] // App icon URL
    }
};

ReactDOM.render(
  <>
    <WalletConnectProvider autoManageSession={true} options={wcOptions}>
      <App />
    </WalletConnectProvider>
  </>,
  document.getElementById("root")
);
```

### Wrapping WalletConnectProvider

Wrap your React application's root component with the `WalletConnectProvider` and declare options as shown above. The `autoManageSession` option reloads the user's connected session and subscribes to the `disconnect` event. If you prefer manual session management, set this option to `false` and call the `manageSession` method at the appropriate time.

### Using the WalletConnect Instance

Access the WalletConnect instance anywhere in your React app using the `useWalletConnect` hook:

```tsx
import { useWalletConnect } from "@epicchain/wallet-connect-sdk-react";

export default function MyComponent() {
  const wcSdk = useWalletConnect();

  const connectWallet = async () => {
    const connection = await wcSdk.connectWallet();
    console.log('Connected Wallet Address:', connection.address);
  };

  return (
    <button onClick={connectWallet}>Connect Wallet</button>
  );
}
```

---

## Advanced Usage

### Metadata Customization

The `metadata` object allows you to personalize the user experience by specifying application-specific details. Each parameter serves a distinct purpose:

- **name**: The name of your application as displayed in wallets.
- **description**: A brief description that conveys your app's purpose.
- **url**: A clickable link to your application's website.
- **icons**: An array of URLs pointing to your app's icon assets.

By providing clear and visually appealing metadata, you enhance user trust and engagement.

### Debugging Tips

To facilitate debugging, enable verbose logging during development:

```javascript
wcSdk.enableDebugging(true);
```

This provides detailed logs of SDK activities, aiding in troubleshooting.

### Integration Best Practices

- **Secure Project ID**: Keep your WalletConnect Project ID confidential to prevent unauthorized access.
- **Network Stability**: Implement retry logic to handle network disruptions.
- **Responsive Design**: Ensure your app UI adapts to various device sizes for optimal user experience.

---

## Examples

### Establishing Wallet Connections

Below is a simple example of connecting to a wallet using the WalletConnect SDK:

```javascript
const connection = await wcSdk.connectWallet();
console.log('Connected Wallet Address:', connection.address);
```

### Handling Disconnects

Monitor and handle wallet disconnections to maintain session stability:

```javascript
wcSdk.on('disconnect', () => {
    console.log('Wallet disconnected.');
});
```

---

## Additional Resources

### Community Support

Join the discussion and connect with other developers:

- **Discord**: [WalletConnect Discord](https://discord.com/invite/u7PmNUpSGg)
- **Twitter**: [WalletConnect Twitter](https://x.com/epicchainlabs)

### Changelog

Stay updated with the latest SDK features and fixes:

- [SDK Changelog](https://github.com/epicchainlabs/epicchain-wallet-connect/blob/main/CHANGELOG.md)

---

By following this comprehensive guide, you can unlock the full potential of the WalletConnect SDK React, enhancing your application's functionality and user engagement. Dive into the world of seamless wallet connectivity today!

