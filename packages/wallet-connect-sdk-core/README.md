# WalletConnect SDK Core Documentation

Welcome to the **WalletConnect SDK Core** guide. This document provides comprehensive instructions to help you integrate and utilize the SDK in your applications seamlessly.

---

## Table of Contents

- [Introduction](#introduction)
- [Installation](#installation)
- [Setup](#setup)
  - [Creating a WalletConnect Project](#creating-a-walletconnect-project)
  - [Initializing the SDK](#initializing-the-sdk)
  - [Session Management](#session-management)
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

The **WalletConnect SDK Core** by EpicChain Labs is your gateway to secure and user-friendly wallet connections. This SDK simplifies the integration process, ensuring that your application can interact with wallets efficiently and effectively. Whether you're building a DeFi platform, NFT marketplace, or any other blockchain-enabled application, this SDK is tailored to meet your needs.

With features like real-time session management, customizable metadata, and robust connection protocols, the WalletConnect SDK Core empowers developers to focus on their core functionality while ensuring a seamless user experience.

---

## Installation

Installing the SDK is the first step toward integrating WalletConnect functionality into your application. The SDK supports both NPM and Yarn package managers, making it compatible with a wide range of development environments.

### Using NPM

```bash
npm install @epicchain/wallet-connect-sdk-core
```

### Using YARN

```bash
yarn add @epicchain/wallet-connect-sdk-core
```

Ensure that your project environment meets the following prerequisites:

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

The initialization process involves configuring the SDK with your project details. The SDK provides flexibility, allowing you to customize metadata to align with your application's branding.

```javascript
import WcSdk from '@epicchain/wallet-connect-sdk-core';
import SignClient from '@walletconnect/sign-client';

const wcSdk = await WcSdk.init({
    projectId: '<your wc project id>', // The unique project ID from WalletConnect
    relayUrl: 'wss://relay.walletconnect.com', // WalletConnect relay server URL
    metadata: {
        name: 'MyApplicationName', // Application name to display in wallets
        description: 'My Application description', // Description shown in wallets
        url: 'https://myapplicationdescription.app/', // Application website URL
        icons: ['https://myapplicationdescription.app/myappicon.png'] // App icon URL
    }
});
```

#### Metadata Customization

The `metadata` object allows you to personalize the user experience by specifying application-specific details. Each parameter serves a distinct purpose:

- **name**: The name of your application as displayed in wallets.
- **description**: A brief description that conveys your app's purpose.
- **url**: A clickable link to your application's website.
- **icons**: An array of URLs pointing to your app's icon assets.

By providing clear and visually appealing metadata, you enhance user trust and engagement.

### Session Management

Efficient session management is critical for a smooth user experience. The `manageSession` method automates session restoration and event subscription.

```javascript
await wcSdk.manageSession();
```

This method:

1. Restores any active user sessions.
2. Subscribes to `disconnect` events to handle session termination gracefully.
3. Ensures seamless reconnection during subsequent user interactions.

---

## Advanced Usage

The WalletConnect SDK Core includes several advanced features to meet diverse application requirements.

### Debugging Tips

To facilitate debugging, enable verbose logging during development:

```javascript
WcSdk.enableDebugging(true);
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

By following this comprehensive guide, you can unlock the full potential of the WalletConnect SDK Core, enhancing your application's functionality and user engagement. Dive into the world of seamless wallet connectivity today!

