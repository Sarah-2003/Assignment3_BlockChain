# Blockchain Implementation Assignment

## Overview
This repository contains an implementation of a blockchain-based distributed consensus protocol from the Coursera course "Bitcoin and Cryptocurrency Technologies". The project focuses on building a node that processes incoming transactions and blocks while maintaining an updated blockchain.

## Prerequisites
- Java Development Kit (JDK)
- [Assignment 1 - ScroogeCoin](https://github.com/Sarah-2003/Assignment1_ScroogeCoin)
- Understanding of blockchain fundamentals and UTXOs

## Project Files

### Core Components
- **`BlockChain.java`**
  - Main implementation file
  - Maintains blockchain structure
  - Handles memory-efficient block storage
  - Implements consensus rules

- **`Block.java`**
  - Defines block data structure
  - Stores transaction data
  - Manages block headers

- **`BlockHandler.java`**
  - Processes newly received blocks
  - Creates new blocks
  - Handles incoming transactions

- **`Transaction.java`**
  - Enhanced version from Assignment 1
  - Includes coinbase transaction functionality
  - Manages transaction inputs/outputs

- **`TransactionPool.java`**
  - Implements transaction pool management
  - Required for new block creation
  - Handles pending transactions

### Utility Components
- **`ByteArrayWrapper.java`**
  - Utility for byte array handling
  - Enables hash function key usage
  - Supports TransactionPool operations

### Required from Assignment 1
- **`TxHandler.java`**
  - Transaction validation logic
  - UTXO pool management
  - Must include new `getUTXOPool()` method

- **`UTXO.java` & `UTXOPool.java`**
  - Unspent transaction output handling
  - Maintains UTXO collections

## Implementation Details

### BlockChain Class API
```java
public class BlockChain {
    public static final int CUT_OFF_AGE = 10;
    
    // Constructor
    public BlockChain(Block genesisBlock)
    
    // Core functionality
    public Block getMaxHeightBlock()
    public UTXOPool getMaxHeightUTXOPool()
    public TransactionPool getTransactionPool()
    public boolean addBlock(Block block)
    public void addTransaction(Transaction tx)
}
```

### Key Features
1. **Memory Efficiency**
   - Maintains limited block nodes
   - Implements CUT_OFF_AGE mechanism
   - Prevents memory overflow

2. **Fork Handling**
   - Supports multiple chain forks
   - Maintains tree structure
   - Handles chain reorganization

3. **Transaction Management**
   - Global transaction pool
   - UTXO tracking per block
   - Coinbase transaction support

## Implementation Requirements

### Blockchain Management
- Store only recent blocks within CUT_OFF_AGE
- Maintain UTXO pools for potential new blocks
- Handle blockchain forks appropriately

### Validation Rules
1. Genesis block handling
   - Reject new genesis blocks
   - Return false for null parent hash

2. Height requirements
   - Block height > (maxHeight - CUT_OFF_AGE)
   - Support new blocks at height 2 if chain height ≤ CUT_OFF_AGE + 1

3. Transaction validation
   - Verify all transactions in new blocks
   - No proof-of-work verification required
   - Support immediate coinbase spending

### Special Considerations
- Return oldest block when multiple blocks exist at max height
- Coinbase value fixed at 25 bitcoins
- Accept valid transaction sets without maximality requirement
- Handle transaction loss during chain reorganization

## Usage

### Setup
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd blockchain-implementation
   ```

2. Copy required files from Assignment 1
   ```bash
   # Add getUTXOPool() to TxHandler.java
   # Copy TxHandler.java, UTXO.java, and UTXOPool.java
   ```

3. Compile the project:
   ```bash
   javac *.java
   ```

### Testing
- Verify block addition functionality
- Test transaction pool management
- Ensure fork handling works correctly
- Validate memory management implementation

## Assumptions
- Coinbase transactions spendable in next block
- No proof-of-work verification needed
- Transaction sets need not be maximal
- Single global transaction pool
- Fixed coinbase reward (25 BTC)

## Notes
- Maintain efficient data structures
- Consider edge cases in fork handling
- Implement proper memory management
- Follow blockchain consensus rules
- Handle reorganization scenarios properly