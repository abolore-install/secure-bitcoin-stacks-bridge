# Secure Bitcoin-Stacks Bridge Protocol (SBSP)

A high-performance cross-chain bridge enabling trustless asset transfers between Bitcoin and Stacks Layer 2. This smart contract implements a robust multi-validator consensus system for secure bi-directional asset transfers.

## Features

- **Multi-Validator Consensus**: Secure transaction validation through distributed validator network
- **Real-time Settlement**: Fast and efficient cross-chain transfers
- **Atomic Transactions**: Ensures transaction completeness and consistency
- **Emergency Controls**: Built-in failsafe mechanisms for enhanced security
- **Layer 2 Optimized**: Designed for high throughput on Stacks Layer 2
- **Dynamic Validator Management**: Flexible validator addition and removal
- **Comprehensive Security Checks**: Robust validation for all operations

## Technical Specifications

### Transaction Limits

- Minimum Deposit: 0.001 BTC (100,000 satoshis)
- Maximum Deposit: 10 BTC (1,000,000,000 satoshis)
- Required Bitcoin Confirmations: 6

### Security Features

- Multi-signature validation
- Pausable bridge operations
- Emergency withdrawal mechanism
- Strict input validation
- Comprehensive error handling

## Smart Contract Functions

### Administrative Functions

#### `initialize-bridge`

- Initializes the bridge state
- Access: Contract deployer only

#### `pause-bridge`

- Temporarily halts all bridge operations
- Access: Contract deployer only

#### `resume-bridge`

- Resumes bridge operations
- Access: Contract deployer only

#### `add-validator`

- Adds a new validator to the bridge
- Access: Contract deployer only
- Parameters:
  - `validator`: Principal address of the new validator

#### `remove-validator`

- Removes a validator from the bridge
- Access: Contract deployer only
- Parameters:
  - `validator`: Principal address of the validator to remove

### Core Bridge Operations

#### `initiate-deposit`

- Initiates a Bitcoin to Stacks transfer
- Access: Validators only
- Parameters:
  - `tx-hash`: Bitcoin transaction hash
  - `amount`: Amount in satoshis
  - `recipient`: Stacks recipient address
  - `btc-sender`: Bitcoin sender address

#### `confirm-deposit`

- Confirms a deposit with validator signature
- Access: Validators only
- Parameters:
  - `tx-hash`: Bitcoin transaction hash
  - `signature`: Validator signature

#### `withdraw`

- Initiates a Stacks to Bitcoin withdrawal
- Access: Any user with sufficient balance
- Parameters:
  - `amount`: Amount in satoshis
  - `btc-recipient`: Bitcoin recipient address

#### `emergency-withdraw`

- Performs emergency withdrawal
- Access: Contract deployer only
- Parameters:
  - `amount`: Amount to withdraw
  - `recipient`: Recipient address

### Read-Only Functions

#### `get-deposit`

- Retrieves deposit information
- Parameters:
  - `tx-hash`: Bitcoin transaction hash

#### `get-bridge-status`

- Returns current bridge operational status

#### `get-validator-status`

- Checks if a principal is an active validator
- Parameters:
  - `validator`: Principal address to check

#### `get-bridge-balance`

- Returns user's bridge balance
- Parameters:
  - `user`: Principal address

### Validation Functions

- `is-valid-principal`: Validates Stacks addresses
- `is-valid-btc-address`: Validates Bitcoin addresses
- `is-valid-tx-hash`: Validates transaction hashes
- `is-valid-signature`: Validates validator signatures
- `validate-deposit-amount`: Validates deposit amounts

## Error Handling

The contract includes comprehensive error handling with specific error codes:

- `ERROR-NOT-AUTHORIZED` (u1000): Unauthorized access attempt
- `ERROR-INVALID-AMOUNT` (u1001): Invalid transaction amount
- `ERROR-INSUFFICIENT-BALANCE` (u1002): Insufficient funds
- `ERROR-INVALID-BRIDGE-STATUS` (u1003): Invalid bridge state
- `ERROR-INVALID-SIGNATURE` (u1004): Invalid validator signature
- `ERROR-ALREADY-PROCESSED` (u1005): Duplicate transaction
- `ERROR-BRIDGE-PAUSED` (u1006): Bridge is paused
- `ERROR-INVALID-VALIDATOR-ADDRESS` (u1007): Invalid validator address
- `ERROR-INVALID-RECIPIENT-ADDRESS` (u1008): Invalid recipient address
- `ERROR-INVALID-BTC-ADDRESS` (u1009): Invalid Bitcoin address
- `ERROR-INVALID-TX-HASH` (u1010): Invalid transaction hash
- `ERROR-INVALID-SIGNATURE-FORMAT` (u1011): Invalid signature format

## Data Storage

### Maps

- `deposits`: Tracks all bridge deposits
- `validators`: Stores validator information
- `validator-signatures`: Records validator signatures
- `bridge-balances`: Maintains user balances

### Variables

- `bridge-paused`: Bridge operational status
- `total-bridged-amount`: Total amount in bridge
- `last-processed-height`: Last processed block height

## Security Considerations

1. **Multi-Validator Consensus**

   - Multiple validators must confirm transactions
   - Prevents single point of failure
   - Enhances security through distributed validation

2. **Amount Limits**

   - Enforced minimum and maximum deposit amounts
   - Prevents dust attacks and limits exposure

3. **Confirmation Requirements**

   - 6 Bitcoin confirmations required
   - Ensures transaction finality

4. **Emergency Controls**

   - Bridge can be paused in emergencies
   - Emergency withdrawal mechanism
   - Protected administrative functions

5. **Input Validation**
   - Strict validation for all inputs
   - Format checking for addresses and hashes
   - Amount range validation

## Implementation Notes

1. **Layer 2 Optimization**

   - Designed for Stacks Layer 2 scalability
   - Optimized data structures
   - Efficient validation process

2. **Transaction Processing**

   - Atomic operations ensure consistency
   - Clear state transitions
   - Comprehensive event logging

3. **Balance Management**
   - Safe arithmetic operations
   - Accurate balance tracking
   - Protected withdrawal process

## Best Practices

1. Always verify transaction confirmations
2. Monitor bridge status before operations
3. Validate all input parameters
4. Maintain secure validator keys
5. Regular security audits recommended
6. Monitor bridge balances and operations
