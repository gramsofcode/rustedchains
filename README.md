# Blockchain Implementation in Rust

A simple, educational blockchain implementation written in Rust that demonstrates core blockchain concepts including proof-of-work mining, transaction management, and chain validation.

## Features

- **Proof-of-Work Mining**: Configurable difficulty-based mining system
- **Transaction Management**: Support for inputs, outputs, and coinbase transactions
- **UTXO Model**: Unspent Transaction Output tracking similar to Bitcoin
- **Chain Validation**: Comprehensive block and transaction validation
- **SHA-256 Hashing**: Cryptographic hashing for block integrity

## How It Works

### Block Structure

Each block contains:
- **Index**: Position in the blockchain
- **Timestamp**: When the block was created
- **Hash**: SHA-256 hash of the block contents
- **Previous Block Hash**: Links to the previous block
- **Nonce**: Proof-of-work value
- **Transactions**: List of transactions in the block
- **Difficulty**: Mining difficulty target

### Transactions

Transactions follow the UTXO (Unspent Transaction Output) model:
- **Inputs**: Previously unspent outputs being consumed
- **Outputs**: New outputs being created with recipient addresses and values
- **Coinbase Transactions**: Special transactions that create new coins (mining rewards)

### Mining

The mining process uses proof-of-work:
1. The miner increments a nonce value
2. Computes the hash of the block
3. Checks if the hash meets the difficulty target
4. Repeats until a valid hash is found

### Validation

The blockchain validates:
- ✓ Sequential block indices
- ✓ Valid proof-of-work (hash meets difficulty)
- ✓ Chronological timestamps
- ✓ Correct previous block hash references
- ✓ Valid transaction inputs (must be unspent)
- ✓ Transaction value conservation (inputs ≥ outputs)
- ✓ Proper coinbase transaction format

## Installation

Make sure you have [Rust](https://www.rust-lang.org/tools/install) installed.

Clone the repository:
```bash
git clone https://github.com/gramsofcode/rustedchains.git
cd rustedchains
```

## Usage

Build and run the example:
```bash
cargo run
```

This will:
1. Create a genesis block with initial transactions
2. Mine the genesis block
3. Create a second block with new transactions
4. Mine the second block
5. Validate and add both blocks to the blockchain

### Example Output

```
Mined Genesis Block: Block[0]: 1358fd8db75267e71adf6d079123b2dfd95c5b4aafbccd4ca4ace333d8f30000 at: 1768330268038 with: 1 nonce: 59515
Mined Block: Block[1]: bf4809c3bbce9f1835c774e9df230ce40d52cb4ade992ef0d45a65eb297d0000 at: 1768330268184 with: 2 nonce: 252358
```
```
```

## Project Structure

```
src/
├── main.rs          # Example usage and demonstration
├── lib.rs           # Core utilities and type definitions
├── block.rs         # Block structure and mining logic
├── blockchain.rs    # Blockchain and validation logic
├── transaction.rs   # Transaction and output structures
└── hashable.rs      # Hashing trait implementation
```

## Code Example

```rust
use blockchainlib::*;

// Create a new blockchain
let mut blockchain = Blockchain::new();

// Create a genesis block
let mut genesis_block = Block::new(
    0,
    now(),
    vec![0; 32],
    vec![/* transactions */],
    0x0000ffffffffffffffffffffffffffff,
);

// Mine the block
genesis_block.mine();

// Add to blockchain
blockchain.update_with_block(genesis_block)
    .expect("Failed to add block");
```

## Dependencies

- `crypto-hash`: SHA-256 hashing
- `hex`: Hexadecimal encoding for display

## Technical Details

### Difficulty

The difficulty is represented as a 128-bit number. A block hash is valid if its numerical value is less than the difficulty target. Lower difficulty values make mining harder.

### UTXO Tracking

The blockchain maintains a set of unspent transaction outputs. When a transaction is processed:
- Input outputs are removed from the unspent set
- New outputs are added to the unspent set
- Double-spending is prevented by checking against this set

## Limitations & Educational Purpose

⚠️ **This is an educational implementation** designed to demonstrate blockchain concepts. It is **not production-ready** and lacks many features required for real-world use:

- No network/peer-to-peer functionality
- No persistence (blockchain only exists in memory)
- No wallet or key management
- No signature verification
- Simplified transaction model
- No consensus mechanism beyond proof-of-work
- Mining can potentially run indefinitely with very high difficulty

## Learning Resources

To understand this implementation better, you may want to read about:
- [Bitcoin's UTXO model](https://en.wikipedia.org/wiki/Unspent_transaction_output)
- [Proof-of-Work consensus](https://en.wikipedia.org/wiki/Proof_of_work)
- [SHA-256 hashing](https://en.wikipedia.org/wiki/SHA-2)
- [Blockchain fundamentals](https://en.wikipedia.org/wiki/Blockchain)

## License

MIT

## Contributing

Contributions are welcome! Feel free to open issues or submit pull requests.

## Author

Shlok Shukla

---

Built with 🦀 Rust
