# Bitcoin Core v29 — Local Installation, Configuration, and RPC Interaction (Assignment Report)

## Overview
This assignment demonstrates the process of installing, configuring, and running **Bitcoin Core v29.0** locally inside a terminal (without global installation).  
The goal was to set up a **Bitcoin Core node in regtest mode**, interact with it using RPC (Remote Procedure Call) commands, and verify that blockchain, wallet, and network features function correctly.

---

## Objective
The main objectives of this assignment were to:

1. Download and run Bitcoin Core **locally** inside a custom folder (no system install).  
2. Start the **Bitcoin daemon (`bitcoind`)** in **regtest mode** for testing.  
3. Create a wallet and generate test coins by mining blocks.  
4. Run multiple **RPC commands** and save their outputs.  
5. Demonstrate understanding of how Bitcoin Core nodes and RPC communication work.

---

## Environment Setup
- **System:** Local terminal session (non-root user)
- **OS Environment:** Linux-based terminal  
- **Bitcoin Core Version:** 29.0  
- **Mode:** Regtest (Private blockchain for testing)
- **Tools Used:** `bitcoind`, `bitcoin-cli`, `bash`

---

## Step-by-Step Implementation

### Step 1: Create a Working Directory
A dedicated folder was created for this assignment.
```bash
mkdir ~/Bitcon-Assingments
cd ~/Bitcon-Assingments
mkdir bitcon-Assigments1
cd bitcon-Assigments1
Step 2: Download Bitcoin Core v29.0
Bitcoin Core was downloaded directly from the official website.

bash
Copy code
wget https://bitcoincore.org/bin/bitcoin-core-29.0/bitcoin-29.0-x86_64-linux-gnu.tar.gz
Step 3: Extract Bitcoin Core Files
The downloaded archive was extracted to reveal the binaries.

bash
Copy code
tar -xvf bitcoin-29.0-x86_64-linux-gnu.tar.gz
After extraction, the bin directory contained the main executables:

bitcoind — Bitcoin Daemon

bitcoin-cli — Command line tool for RPC commands

bitcoin-wallet — Wallet management

bitcoin-tx, bitcoin-util, etc.

Step 4: Create a Regtest Data Directory
A separate folder for blockchain and wallet data was created.

bash
Copy code
mkdir -p ~/bitcoin-regtest
Step 5: Start Bitcoin Core Daemon (Local Node)
Bitcoin Core was started in regtest mode (for private testing).

bash
Copy code
cd bitcoin-29.0/bin
./bitcoind -regtest -daemon -datadir=~/bitcoin-regtest -rpcuser=rpcuser -rpcpassword=rpcpass -fallbackfee=0.0002
✅ The message “Bitcoin Core starting” confirmed the daemon was running.

Step 6: Check Node Status
You can check the blockchain information using:

bash
Copy code
./bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass getblockchaininfo
This confirmed the node was initialized with 0 blocks on the regtest chain.

Step 7: Create a New Wallet
A wallet was created to store mined coins.

bash
Copy code
./bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass createwallet "mywallet"
Step 8: Generate New Address and Mine Blocks
A new wallet address was generated, and 101 blocks were mined to earn test coins.

bash
Copy code
ADDR=$(./bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass getnewaddress)
./bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass generatetoaddress 101 $ADDR
This produced the first set of transactions and a balance of 5100 BTC (test coins).

Step 9: Run RPC Commands and Save Outputs
Multiple RPC commands were executed to verify the node’s behavior, and their outputs were saved as .txt files.

bash
Copy code
./bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass getnetworkinfo      > rpc-getnetworkinfo.txt
./bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass getblockchaininfo   > rpc-getblockchaininfo.txt
./bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass getwalletinfo       > rpc-getwalletinfo.txt
./bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass getbalance          > rpc-getbalance.txt
./bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass listtransactions    > rpc-listtransactions.txt
To check a specific transaction:

bash
Copy code
./bitcoin-cli -regtest -rpcuser=rpcuser -rpcpassword=rpcpass gettransaction c72ecbfd4e65ae65aaca9b17d60882669c19fd76a89161c8daa130cc2520253f > rpc-gettransaction.txt
Step 10: Verify Output Files
All files were successfully created:

Copy code
rpc-getnetworkinfo.txt
rpc-getblockchaininfo.txt
rpc-getwalletinfo.txt
rpc-getbalance.txt
rpc-listtransactions.txt
rpc-gettransaction.txt
Output Summary
Blockchain Information
Chain: regtest

Blocks: 202

Headers: 202

Difficulty: 4.65e-10

Pruned: false

Wallet Information
Wallet Name: mywallet

Balance: 5100.00000000 BTC

Immature Balance: 3675.00000000 BTC

Transactions: 202

Example Transaction
json
Copy code
{
  "txid": "c72ecbfd4e65ae65aaca9b17d60882669c19fd76a89161c8daa130cc2520253f",
  "amount": 25.00000000,
  "confirmations": 10
}
Notes and Observations
Regtest Mode was ideal for testing since it allowed instant block generation without connecting to real peers.

The RPC interface worked perfectly and returned valid JSON responses.

gettransaction worked better than getrawtransaction since txindex was not enabled.

Outputs matched expected results, showing Bitcoin Core was installed and functioning locally.

Conclusion
This assignment demonstrates the complete process of:

Running Bitcoin Core locally in terminal mode

Configuring and launching it in regtest

Creating and managing wallets

Mining blocks and verifying balances

Using RPC commands to interact with the node

All RPC results were stored in .txt files as evidence of correct execution.
The project confirms a successful setup and operation of Bitcoin Core v29 without requiring system-wide installation.