# T3rn Executor Node Setup Guide

This guide provides step-by-step instructions on how to set up the T3rn Executor node on Ubuntu. Follow these instructions to configure and start your node.

## Prerequisites

- **Operating System**: Ubuntu 22.04 or later
- **System Requirements**: Minimum 4 CPU cores, 8 GB RAM, 80 GB SSD
- **Rust Installed**: Required for the build environment

If you haven't installed Rust yet, use the following commands:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
```

## Step-by-Step Setup

### Step 1: Download and Extract the Latest Executor Binary

To download the latest version of T3rn Executor binary, run the following commands:

```bash
LATEST_VERSION=$(curl -s https://api.github.com/repos/t3rn/executor-release/releases/latest | grep 'tag_name' | cut -d\" -f4)
wget https://github.com/t3rn/executor-release/releases/download/${LATEST_VERSION}/executor-linux-${LATEST_VERSION}.tar.gz
tar -xzvf executor-linux-${LATEST_VERSION}.tar.gz
cd executor/executor/bin
```

### Step 2: Set Up Environment Variables

Before running the executor, configure the necessary environment variables:

```bash
export NODE_ENV=testnet
export LOG_LEVEL=debug
export LOG_PRETTY=false
export PRIVATE_KEY_LOCAL=<replace_with_your_private_key>
export ENABLED_NETWORKS='arbitrum-sepolia,base-sepolia,optimism-sepolia,l1rn'
```

### Explanation of Environment Variables:

- **NODE_ENV**: Sets the network environment. Use `testnet` for testing or `mainnet` for live networks.
- **LOG_LEVEL**: Controls the log output detail. `debug` gives more information.
- **PRIVATE_KEY_LOCAL**: This is the private key of your executor's wallet. **Replace this with your actual key**.
- **ENABLED_NETWORKS**: Define which networks the executor will operate on.

### Step 3: Start the Executor

To start the executor, run:

```bash
./executor
```

If you want to see detailed warnings, use:

```bash
./executor --trace-warnings
```

### Step 4: Verify the Setup

To monitor the logs and ensure the node is running correctly, use:

```bash
journalctl -u t3rn-executor -f
```

This command will display real-time log information so you can verify the node's status.

## Conclusion

Following these steps will successfully set up your T3rn Executor node. Make sure to replace the placeholder values such as the private key with your actual values.

For further details, refer to the [T3rn documentation](https://docs.t3rn.io/executor/become-an-executor/binary-setup).
