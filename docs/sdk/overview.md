---
title: Overview
---

The Aztec SDK is the gateway for developers to access the Aztec network and benefit from low gas fees and privacy on Ethereum. The SDK connects to Ethereum and our zk-rollup service and can be integrated with a few lines code.

The SDK is designed to abstract away the complexities of zero-knowledge proofs from the developer and end users. It provides a simple API for creating accounts, depositing and withdrawing tokens anonymously. The core transfer inside the SDK is private by default.

Under the hood the SDK keeps track of a users private balances across multiples assets and provides easy to use helper methods to the developer to create seamless private UI's.

The SDK is written in Typescript and requires a Javascript context (web browser, web view or Node.js). This makes it well suited for developing web interfaces for maximum accessibility.

## What can you do with the SDK?

The Aztec SDK has many capabilities, many of which are associated with the following user actions:

- Connect to the Aztec network
- Add user accounts to decrypt notes and show user balances
- Register new accounts
- Handle signing key to spend notes or withdraw assets to Ethereum
- Query Aztec transaction fees and specify settlement time
- Lookup user aliases associated with spending account to make transfering assets easier
- Migrate accounts to a new public key
- Recover accounts for which a spending key was lost

## Controllers

Most of the above capabilities are possible through the use of `Controllers`. Controllers make it easy to prompt users for relevant transactions when an action requires an Ethereum transaction and create proofs / send transactions to the Aztec network.

Some of examples of common controllers are the `RegisterController` for registering accounts, the `DepositController` for sending Ether or tokens to an Aztec account from an Ethereum account and the `TransferController` for spending notes on the Aztec network.

## SDK Flavours

The SDK comes in 3 flavours. The users environment will typically automatically determine which flavour is used, but it is good to be aware of them because they do have tradeoffs.

The SDK is set up in browsers in an iframe. This allows for additional protection of users keys by creating a nested browsing context that isn't accessible to the application directly (when using the `HOSTED` flavour of the SDK).

### Hosted

The `HOSTED` flavour is dependent on being able to access the SDK via a URL endpoint. In the case of zk.money, the endpoint is `https://sdk.aztec.network` where the Aztec team hosts an instance of the SDK.

When accessing the SDK via this method, users are trusting the provider at that URL with proper management of their Aztec keys. The host also chooses which rollup provider the SDK talks to.

This is the most common way to connect to the network with the SDK right now. This may change as the number of users and applications on the network increases.

### Shared worker

An application can make the SDK availble to users via `SHARED_WORKER` if the SDK at the `HOSTED` endpoint is unavailable.

This option is preferred over `PLAIN` because it allows similar work to be shared. For example, if you were using `PLAIN` in multiple tabs, each tab would be doing the same work. The `SHARED_WORKER` is more efficient in terms of networking and storage.
### Plain

`PLAIN` is used with a node backend or gets used in the iframe if shared workers are not supported in the execution context.
