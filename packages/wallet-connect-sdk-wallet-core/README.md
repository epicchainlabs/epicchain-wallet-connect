<p align="center">
  <img
    src="https://raw.githubusercontent.com/epicchain/wallet-connect-sdk/main/.github/resources/images/coz.png"
    width="200px;">
</p>

<p align="center">
  WalletConnect wallet-side Core SDK for EpicChain
  <br/> Made by <b>EpicChain Lab's</b>
</p>

- [Installation](#installation)
- [Setup](#setup)
- [Important Information](#important-information)
- [Code Examples](#code-examples)
- [Using with React.js](https://www.npmjs.com/package/@epicchain/wallet-connect-sdk-wallet-react)
- [Advanced Configuration](#advanced-configuration)
- [Troubleshooting](#troubleshooting)
- [Additional Resources](#additional-resources)
- [FAQ](#faq)

## Installation

To get started with the WalletConnect SDK for EpicChain, you’ll first need to install the necessary dependencies within your application. The SDK supports both NPM and Yarn for easy installation.

### NPM

If you are using NPM as your package manager, you can install the SDK with the following command:

```bash
npm i @epicchain/wallet-connect-sdk-wallet-core
```

### YARN

Alternatively, if you prefer Yarn, run the following command:

```bash
yarn add @epicchain/wallet-connect-sdk-core
```

Both installation methods will install the necessary dependencies for integrating the WalletConnect SDK into your application, allowing you to connect EpicChain to various wallets seamlessly.

## Setup

### Creating a WalletConnect Project

Before you can begin using the SDK, you need to create a project on the WalletConnect platform. This is a straightforward process:

1. Go to [Wallet Connect's official website](https://walletconnect.com/).
2. Sign up or log into your account.
3. Navigate to the "Projects" section and create a new project. Fill in the necessary fields, such as the project name and description.
4. Once the project is created, you will receive a `Project ID`, which you will use in your SDK configuration.

### Initialize the SDK Client

Once you have your `Project ID`, you can initialize the SDK within your application. Here’s how you can configure and initialize the SDK client:

```ts
import WcWalletSdk from '@epicchain/wallet-connect-sdk-wallet-core'

const sdk = new WcWalletSDK({
  clientOptions: {
    projectId: '<your wc project id>', // Your WalletConnect project ID
    relayUrl: 'wss://relay.walletconnect.com', // Using WalletConnect’s official relay server
    metadata: {
      name: 'MyEpicApplication', // Name displayed on the wallet
      description: 'A description of MyEpicApplication', // Short description to be shown on the wallet
      url: 'https://myepicapplication.com/', // URL linked from the wallet
      icons: ['https://myepicapplication.com/icon.png'], // Icon image shown on the wallet
    },
  },
})

await sdk.init()
```

This code will initialize the WalletConnect SDK, configure the project-specific settings, and set up metadata for how your application will be displayed on users' wallets.

## Important Information

### Adapter Registration

To interact with WalletConnect and communicate with users' wallets, it’s essential to register an adapter. This adapter allows the SDK to perform RPC (Remote Procedure Call) requests, manage sessions, and handle incoming proposals or requests.

You must extend the abstract adapter to use it with the SDK. To do this, you’ll need to use the `WalletConnectEpicChain3Adapter`.

There are two ways to assign your adapter to the SDK:

1. **Passing the adapter in the SDK constructor:**

   ```ts
   const sdk = new WcWalletSDK({
     clientOptions: {}, // SignClient options
     methods: ['methods', 'to', 'authorize'], // Define allowed methods
     adapter: new YourAdapter(), // Pass the adapter directly
   })
   ```

2. **Assigning the adapter after SDK initialization:**

   ```ts
   const sdk = new WcWalletSDK({
     clientOptions: {}, // SignClient options
     methods: ['methods', 'to', 'authorize'], // Define allowed methods
   })

   sdk.adapter = new YourAdapter() // Assign the adapter after SDK initialization
   ```

### Auto Accept Methods

By default, the SDK does not auto-approve any request methods. However, you can configure the SDK to automatically accept certain methods by specifying them in the `autoAcceptMethods` option.

```ts
const sdk = new WcWalletSDK({
  clientOptions: {}, // SignClient options
  autoAcceptMethods: ['your', 'auto', 'accept', 'methods'], // Automatically accept specific methods
})
```

### Listening to Property Changes

You can listen for changes in session status, requests, proposals, and other important events by registering listeners with the SDK's emitter.

```ts
const sdk = new WcWalletSDK({
  clientOptions: {}, // SignClient options
  methods: ['methods', 'to', 'authorize'],
})

sdk.emitter.on('proposals', items => {
  setProposals(items) // Handle changes in proposals
})

sdk.emitter.on('sessions', items => {
  setSessions(items) // Handle changes in sessions
})

sdk.emitter.on('requests', items => {
  setRequests(items) // Handle incoming requests
})

sdk.emitter.on('status', item => {
  setStatus(item) // Handle status updates
})

await sdk.init()
```

This allows you to react to updates in real time and take actions based on changes in the WalletConnect state.

## Code Examples

### Connect to the Dapp

To establish a new connection to a decentralized application (DApp), you can use the `connect` method, which will generate a new proposal that users need to accept or reject.

```ts
await sdk.connect(
  'wc:b3b01e4e9d0c7d2dcebe412687616b39a7020ae647133e95281bd21053bba6cb@2?relay-protocol=irn&symKey=ee83ff49a5374ed46dc07c2dc1242903aba9b28f60f1cf5f5e48540e5b40a7d6&wccv=2'
)
```

This method initiates the connection process and sends a proposal to the wallet.

### Disconnect from a Specific Dapp Session

To disconnect from a particular session, simply call the `disconnect` method with the specific session object.

```ts
const session = sdk.sessions[0]
await sdk.disconnect(session)
```

This will terminate the connection with the specified session.

### Approve a Connection Proposal

When a connection proposal is received, you can approve it by providing the account details. Here’s an example of how to approve a proposal:

```ts
const proposal = sdk.proposals[0]
await sdk.approveProposal(proposal, {
  account: {
    address: '0xAddressOfAccount', // Provide the account address
    chain: 'epicchain', // Specify the chain that the account belongs to
  },
})
```

### Reject a Connection Proposal

In some cases, you may wish to reject a proposal. This can be done easily with the following code:

```ts
const proposal = sdk.proposals[0]
await sdk.rejectProposal(proposal)
```

### Approve a Session Request

Once you’ve registered your adapter, you can approve a session request by calling the `approveRequest` method with the specific request.

```ts
const request = sdk.requests[0]
await sdk.approveRequest(request)
```

### Reject a Session Request

If you need to reject a request, you can use the following code snippet:

```ts
const request = sdk.requests[0]
await sdk.rejectRequest(request)
```

## Advanced Configuration

### Handling Multiple Sessions

In some cases, you may need to handle multiple sessions at once. The SDK allows you to manage multiple wallet connections and their respective sessions. To handle this:

- Listen to session changes using the `sessions` event emitter.
- Store session data in your app and use it when interacting with users’ wallets.
- Use `disconnect` to terminate specific sessions and `connect` to start new ones.

### Customizing WalletConnect UI

While the SDK handles most of the interaction, you might want to provide a custom user interface (UI) for WalletConnect. You can extend the functionality to allow users to initiate connections, approve/reject requests, and view sessions directly from your app.

- Customize the UI by embedding WalletConnect options into your application.
- Add wallet icons, descriptions, and links in a way that fits your application’s branding.

## Troubleshooting

Here are some common issues you might encounter when using the WalletConnect SDK with EpicChain:

- **Issue**: Unable to connect to the wallet.
  - **Solution**: Verify that your `Project ID` is correct and that the relay URL is accessible.
  
- **Issue**: Connection proposal is not being approved.
  - **Solution**: Ensure that you have implemented the adapter correctly and that your method signatures match the WalletConnect protocol.

- **Issue**: Session disconnects unexpectedly.
  - **Solution**: Check for network issues or relay server problems. Make sure that your session management logic is properly handling re-connections.

## Additional Resources

For more detailed documentation and advanced usage, visit the following links:

- [WalletConnect Documentation](https://walletconnect.com/docs/)
- [EpicChain SDK Documentation](https://epicchain.org/docs/)
- [React.js WalletConnect Example](https://www.npmjs.com/package/@epicchain/wallet-connect-sdk-wallet-react)

## FAQ

**Q: Can I use WalletConnect with other blockchains?**  
A: Yes, the WalletConnect SDK is compatible with multiple blockchains. You simply need to configure the correct chain details in your project setup.

**Q: How do I handle wallet authentication?**  
A: Authentication is handled through the WalletConnect protocol, where the user can approve or reject requests based on their wallet settings. You can customize the authentication flow to suit your application’s needs.

---

This expanded content offers comprehensive information and covers various advanced topics to make the documentation more thorough and informative.