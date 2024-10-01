
### On-Chain Data

#### 1. **Transaction Data**

- **Transactions**: Every transaction made on the Ethereum network is recorded on-chain. This includes the sender’s and receiver’s addresses, the amount of Ether or tokens transferred, and transaction fees (gas).
- **Transaction Receipts**: These include details about the transaction’s execution, such as whether it was successful, any logs generated (events), and gas usage.

#### 2. **Contract Code**

- **Smart Contract Bytecode**: When a smart contract is deployed, its compiled bytecode is stored on-chain. This bytecode is immutable and can be executed by the EVM.
- **Precompiled Contracts**: Certain built-in functions provided by the EVM are also part of the on-chain data.

#### 3. **Contract State**

- **Storage Data**: Smart contracts can store data persistently in the Ethereum state. This includes variables and mappings used by the contract. This data is stored on-chain and persists between transactions.

#### 4. **Account Information**

- **Account Balances**: The Ether balance of each account (both externally owned accounts and smart contracts) is recorded on-chain.
- **Account Nonces**: The nonce (transaction count) of an account is also stored on-chain. It helps prevent double-spending and ensures transaction order.

#### 5. **Logs and Events**

- **Event Logs**: Smart contracts can emit events, which are recorded on-chain. These logs are not directly part of the contract’s storage but are included in the transaction receipts.