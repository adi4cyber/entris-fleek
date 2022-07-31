---
date: 2022-07-31T04:00:04Z
hero_image: "/content/images/frontend-result.png"
title: Deploy a "Hello World" Dapp in 10 Minutes
author: Adi Prayitno

---
This is a quick tutorial to deploy a "Hello World" dapp to the Internet Computer (IC) in 10 minutes or less. Deployment of the dapp only requires basic knowledge of using a terminal.
Before starting, take a look at a version of this dapp running on-chain: [https://6lqbm-ryaaa-aaaai-qibsa-cai.ic0.app/](https://6lqbm-ryaaa-aaaai-qibsa-cai.ic0.app/)

In this tutorial, you will learn how to:

1. Install the Canister SDK
2. Build and deploy a dapp locally
3. Collect free cycles to power your dapp
4. Create a "cycles wallet" from which you can transfer cycles to any other dapps you want to power
5. Deploy a dapp on-chain

This simple `Hello` dapp is composed of two [canister smart contracts](https://wiki.internetcomputer.org/wiki/Glossary#C) (one for backend and one for frontend). The dapp accepts a text argument as input and returns a greeting. For example, if you call the `greet` method with the text argument `Everyone` on the command-line via the canister SDK (see instructions below on how to install the canister SDK), the dapp will return `Hello, Everyone!` either in your terminal:

    $ dfx canister call hello greet Everyone
    $ "Hello, Everyone"

Or via the dapp in a browser, a pop-up window will appear with the message: `Hello, Everyone!`

![](/content/images/frontend-result-1.png)

Note that the "Hello World" dapp consists of backend code written in [Motoko](https://internetcomputer.org/docs/current/developer-docs/build/languages/motoko/), a programming language specifically designed for interacting with the IC, and a simple webpack-based frontend.

This tutorial requires Linux, macOS 12.* Monterey or later, or Windows with a [Windows Subsystem for Linux (WSL)](https://internetcomputer.org/docs/current/developer-docs/quickstart/windows-wsl) installation.

## Topics Covered in this Tutorial[​](https://internetcomputer.org/docs/current/developer-docs/quickstart/hello10mins#topics-covered-in-this-tutorial "Direct link to heading")

* **Canisters** are the smart contracts installed on the IC. They contain the code to be run and a state, which is produced as a result of running the code. As is the case of the "Hello World" dapp, it is common for dapps to be composed of multiple canisters.
* [**Cycles**](https://internetcomputer.org/docs/current/concepts/tokens-cycles) refer to a unit of measurement for resource consumption, typically for processing, memory, storage, and network bandwidth consumed on the IC. For the sake of this tutorial, cycles are analogous to Ethereum’s gas: cycles are needed to run dapps, but unlike gas they are stable and less expensive. Every canister has a cycles account from which the resources consumed by the canister are charged. The IC’s utility token (ICP) can be converted to cycles and transferred to a canister. ICP can always be converted to cycles using the current price of ICP measured in [SDR](https://en.wikipedia.org/wiki/Special_drawing_rights) (a basket of currencies) using the convention that one trillion cycles correspond to one SDR. **Get free cycles from the cycles faucet.**
* A [**cycles wallet**](https://internetcomputer.org/docs/current/developer-docs/build/project-setup/cycles-wallet) is a canister that holds cycles and powers up dapps.

## 1. Installing Tools[​](https://internetcomputer.org/docs/current/developer-docs/quickstart/hello10mins#1-installing-tools "Direct link to heading")

To build and deploy the `Hello` dapp, you need to install the following tools.

### DFX[​](https://internetcomputer.org/docs/current/developer-docs/quickstart/hello10mins#dfx "Direct link to heading")

In this tutorial, we use a Canister SDK called `dfx`, which is the default SDK maintained by the DFINITY foundation.

To install `dfx`, run:

    sh -ci "$(curl -fsSL https://smartcontracts.org/install.sh)"

To verify that `dfx` properly installed, run:

    dfx --version

The terminal should show you the most recent version ([See SDK release notes](https://internetcomputer.org/docs/current/developer-docs/updates/release-notes/)).

More installation options and instructions for uninstalling `dfx` are covered in [Installing the SDK](https://internetcomputer.org/docs/current/developer-docs/build/install-upgrade-remove).

### Node.js[​](https://internetcomputer.org/docs/current/developer-docs/quickstart/hello10mins#nodejs "Direct link to heading")

Node.js is necessary for rendering the frontend assets and so is necessary to complete this tutorial. Note however that Node.js is not needed for canister development in general.

We support all stable versions of Node.js starting with 12. You can install 12, 14, or 16. Please note that Node 17 does not support Webpack’s api proxy tool, so `npm start` may not work correctly.

There are many ways of installing node.js. On Linux, we recommend using your system's package manager. On macOS, we recommend [Homebrew](https://brew.sh/). Alternatively, you find instructions on the [nodejs.org website](https://nodejs.org/en/download).

This tutorial works best with a node.js version higher than `16.*.*`.