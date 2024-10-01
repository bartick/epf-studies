
# Nonce

In Ethereum, the **nonce** is a crucial part of an account's activity, and it serves two main purposes depending on the account type:

1. **Externally Owned Accounts (EOAs)**: For an EOA (controlled by a private key), the nonce represents the **number of transactions sent** from that account. Every time you send a transaction from an EOA, the nonce is incremented by one. It starts at 0 for the first transaction and increases with each subsequent transaction.
    
2. **Contract Accounts**: For a contract account, the nonce indicates the **number of contracts created** by that contract. Each time a contract account creates a new contract, its nonce is incremented.
    

### Importance of Nonce in Ethereum

The nonce plays a vital role in ensuring that:

- **Transactions are processed in the correct order**: Each new transaction must have a nonce exactly one higher than the previous one. If a transaction with a wrong nonce is sent (e.g., skipped or repeated), it will be rejected by the network.
- **Prevents replay attacks**: Since every transaction requires a unique nonce, a previously broadcasted transaction cannot be replayed, as its nonce will have already been used. This prevents malicious actors from re-sending the same signed transaction.

# balance

# CodeHash

This hash refers to the _code_ of an account on the Ethereum virtual machine (EVM). Contract accounts have code fragments programmed in that can perform different operations. This EVM code gets executed if the account gets a message call.

**codeHash** is a critical component of **contract accounts** that relates to the EVM (Ethereum Virtual Machine) code associated with them. To understand the concept in detail, let’s break it down:

 **What is `codeHash`?**

The `codeHash` is a cryptographic hash (using `KECCAK256`) of the code associated with a contract account on the Ethereum blockchain. This hash represents the code stored in the account and helps identify the unique bytecode that is associated with that particular contract.

The code of a contract account is stored in the **Ethereum state database**, under its **codeHash**. The state database is essentially a key-value store, where the code is mapped to its `codeHash`

The actual bytecode of the contract is not directly stored in the account itself but is instead retrieved using the `codeHash` from the state database when needed. The use of a hash (codeHash) allows Ethereum to efficiently manage and retrieve contract code, ensuring that it remains immutable and can be reused without duplicating data.

## Storage root

A 256-bit hash of the root node of a Merkle Patricia trie that encodes the storage contents of the account (a mapping between 256-bit integer values), encoded into the trie as a mapping from the Keccak 256-bit hash of the 256-bit integer keys to the RLP-encoded 256-bit integer values. This trie encodes the hash of the storage contents of this account, and is empty by default.

The `storageRoot` points to the root node of this trie, which stores the contract's internal state as key-value pairs. The key-value mapping is encoded as a mapping between:

- A **Keccak-256 hash** of a 256-bit integer key.
- An **RLP-encoded 256-bit integer value**.

### **What is Stored in a Contract’s Storage?**

- The storage of a smart contract holds the persistent data it needs, such as variables, balances, mappings, and other contract-specific information.
- Each contract has a storage area that maps **256-bit keys to 256-bit values**. These keys and values correspond to the data the contract stores.
- For example, if a contract stores variables like user balances, addresses, or state variables, these will be mapped in storage.



![[Screenshot 2024-09-18 at 4.07.36 PM.png]]


In Ethereum, the **`storageRoot`**, also known as the **storage hash**, is a crucial component of **contract accounts** that refers to the root of a data structure called a **Merkle Patricia Trie**. This data structure is used to store the contract’s internal state (storage). Let’s break it down in detail:

### 1. **What is `storageRoot`?**
- The `storageRoot` is a **256-bit hash** that represents the root of a **Merkle Patricia trie**, which encodes the entire storage contents of a smart contract account.
- **Merkle Patricia Trie**: This is a specialized data structure used in Ethereum to efficiently and securely store large sets of key-value pairs. It combines the benefits of both a **Merkle tree** (for cryptographic proof) and a **Patricia trie** (for compactness and efficient lookup).
- The `storageRoot` points to the root node of this trie, which stores the contract's internal state as key-value pairs. The key-value mapping is encoded as a mapping between:
  - A **Keccak-256 hash** of a 256-bit integer key.
  - An **RLP-encoded 256-bit integer value**.

### 2. **What is Stored in a Contract’s Storage?**
- The storage of a smart contract holds the persistent data it needs, such as variables, balances, mappings, and other contract-specific information.
- Each contract has a storage area that maps **256-bit keys to 256-bit values**. These keys and values correspond to the data the contract stores.
- For example, if a contract stores variables like user balances, addresses, or state variables, these will be mapped in storage.

### 3. **How is the Storage Structured?**
- Ethereum uses a **Merkle Patricia Trie** to store the state efficiently. This trie is a key-value store that encodes the contract's storage.
- Every **256-bit integer key** (a specific storage slot) maps to a **256-bit integer value** (the actual data stored in that slot). 
- Each key is hashed using the **Keccak-256** hash function, and the resulting hash is used in the Merkle Patricia Trie to identify the storage slot.
  
  - **Keys**: These represent specific storage slots. In Solidity, the storage layout of a contract defines how variables and mappings are allocated to specific keys.
  - **Values**: These are the actual stored data (e.g., integers, addresses, or the result of complex mappings).

### 4. **Role of `storageRoot`**
- The `storageRoot` is the hash of the **root node** of the Merkle Patricia Trie that represents the contract’s storage. 
- This means that the `storageRoot` effectively "summarizes" the entire contents of a contract’s storage in one compact 256-bit hash.
  
  - If the contract’s storage changes (e.g., a variable is updated), the structure of the trie will change, leading to a new `storageRoot`.
  - This allows Ethereum to keep track of and verify changes to a contract's storage using just this hash, without needing to store the entire state.

### 5. **Merkle Patricia Trie and `storageRoot`**
The Merkle Patricia Trie is a combination of two data structures:
- **Merkle Tree**: Provides cryptographic guarantees that allow efficient proofs of inclusion or exclusion of an element. This is important for light clients, which only store the `storageRoot` and not the entire state.
- **Patricia Trie**: A compact trie (prefix tree) used to efficiently store mappings of keys to values, reducing the overall size of the stored data.

The `storageRoot` hash enables efficient:
- **State verification**: Instead of comparing the entire storage, only the `storageRoot` needs to be compared to verify if two contracts have the same storage state.
- **Efficient updates**: When the contract’s storage is updated (e.g., a variable is modified), the trie is updated incrementally. The structure changes only along the path from the modified node to the root.

### 6. **How Does Ethereum Use the `storageRoot`?**
- **Smart Contract Execution**: During contract execution, whenever a variable or state in the contract’s storage is updated, the changes are propagated through the Merkle Patricia Trie. As a result, the `storageRoot` is recalculated.
- **Block State**: Each block in Ethereum contains a **state trie**, which contains all the account states (both EOAs and contract accounts). For contract accounts, the `storageRoot` is part of this state and is used to represent the contract’s internal state.
  
  - If a contract interacts with other contracts or stores data, the storage trie will be updated, and the `storageRoot` will reflect those changes.
  
- **Light Clients**: Ethereum’s light clients (which don’t store the full blockchain) use the `storageRoot` to verify the integrity of contract storage. Light clients only need the `storageRoot` to verify that a given value is part of the contract’s storage without needing to download the entire storage data.

### 7. **Storage Layout and Slot Allocation**
In Solidity and other EVM-based languages, storage is laid out in **storage slots**. Each storage slot is mapped to a 256-bit key (as the EVM’s native word size is 256 bits). Solidity’s compiler decides how variables are mapped to these storage slots:
- **Simple Variables**: Each variable occupies a full 256-bit slot.
- **Complex Types (like Mappings or Arrays)**: Solidity computes the key for these using hash functions. For mappings, the key for each element in the mapping is derived by hashing the original key (e.g., an address or integer) and a base slot.
  
This slot-based storage layout ensures efficient storage and retrieval, and changes in any variable will lead to changes in the trie structure, updating the `storageRoot`.

### 8. **Example Workflow**
1. **Contract Deployment**: When a contract is deployed, its storage starts empty, and its `storageRoot` is the hash of an empty trie (i.e., the Keccak-256 hash of an empty string).
2. **Contract Storage Update**: As the contract runs and updates variables or mappings, the contract’s storage changes. Each change results in the recalculation of the Merkle Patricia Trie, and a new `storageRoot` is computed.
3. **State Updates**: Each new block that includes a transaction interacting with the contract will reflect the updated `storageRoot` in the global state trie for Ethereum.

### 9. **Summary of `storageRoot` in Ethereum**
- **Purpose**: The `storageRoot` is the cryptographic hash of the root of a Merkle Patricia Trie that stores the contract’s internal state.
- **Structure**: The trie encodes mappings between 256-bit keys and 256-bit values, where the keys are hashed using Keccak-256.
- **Efficiency**: The `storageRoot` provides a compact representation of the entire storage, allowing Ethereum to efficiently update and verify contract states.
- **Immutability**: Like other elements of Ethereum’s state, the `storageRoot` changes only when the contract’s storage is updated, and each change can be cryptographically verified.

The `storageRoot` is a fundamental part of how Ethereum manages smart contract state, providing both efficient storage and cryptographic security.


## Validator keys

These are 'BLS' keys and they are used to identify validators. These keys can be efficiently aggregated to reduce the bandwidth required for the network to come to consensus. Without this key aggregation the minimum stake for a validator would be much higher.