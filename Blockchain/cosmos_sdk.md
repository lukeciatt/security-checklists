# Cosmos SDK Security Checklist

## Overview
This checklist provides security considerations for developing applications on the Cosmos SDK blockchain framework.

| Category | Item | Description | Status |
|----------|------|-------------|--------|
| **1. General Blockchain Application Considerations** |
| **Determinism** | Transaction Logic | Ensure all transaction-processing logic is deterministic. No use of time-based, random, or external state in transaction logic. | ⬜ |
| | Floating-point Calculations | Avoid floating-point calculations; use integer math instead. | ⬜ |
| | Data Structure Iteration | Avoid map or unordered data structure iteration in state-changing code. | ⬜ |
| | Standard Library Functions | Review use of non-deterministic standard library functions. | ⬜ |
| **Panic Handling** | Explicit Panic Calls | Never use explicit panic calls for error handling. | ⬜ |
| | Error Logging | ALWAYS log errors and handle edge cases gracefully, especially in Rust's unwrap()/expect() and Go's array/mapping dereferencing. | ⬜ |
| | Error Handling | Always handle returned errors from standard and custom functions — unhandled errors are bugs. | ⬜ |
| **Error Handling** | Error Return Values | Confirm every error return value is checked. | ⬜ |
| | Silent Error Handling | Avoid silent error handling, especially in EndBlocker and module callbacks. | ⬜ |
| | Error Suppression | Check that non-expected errors/conditions are never suppressed. | ⬜ |
| **2. Cosmos Protocol/SDK-Specific Considerations** |
| **ABCI Methods** | No Panics in ABCI | ABCI methods (CheckTx, DeliverTx, BeginBlock, EndBlock, Commit, Query, PrepareProposal, ProcessProposal) must catch and log all panics, with no chain-stopping exceptions. | ⬜ |
| **BeginBlocker/EndBlocker** | Deterministic Logic | Ensure logic is deterministic and not computationally expensive (gas limits do not apply). | ⬜ |
| | Resource Abuse Vectors | Heuristically evaluate for resource abuse vectors (DoS potential). | ⬜ |
| **CheckTx** | Lightweight Checks | Only lightweight, deterministic checks allowed. | ⬜ |
| | Resource-Intensive Validation | Avoid resource-intensive validation not constrained by gas. | ⬜ |
| **PrepareProposal/ProcessProposal** | Constraints | Respect MaxGas and MaxBytes constraints. | ⬜ |
| | PrepareProposal Non-determinism | PrepareProposal (run only by proposer) may be non-deterministic, so take care that all effects are only candidate state. | ⬜ |
| | ProcessProposal Validation | ProcessProposal should only validate, not alter persistent state, and must be deterministic. | ⬜ |
| **InitChain** | Gas Meter Reset | Gas meter must be reset at initialization. If not, ensure the first block after InitChain is empty to prevent gas calculation mismatches. | ⬜ |
| **Broadcast in Commit** | Mempool Operations | Never call mempool operations (broadcast_tx_sync, etc.) from within the Commit handler to avoid deadlocks. | ⬜ |
| **Queries** | Protobuf Query Safety | For Cosmos SDK ≥v0.47: Use module_query_safe for state-machine-safe queries. | ⬜ |
| | Deterministic Results | Ensure deterministic results and proper gas accounting for potentially expensive queries. | ⬜ |
| **State Management** | State Change Policy | State must only change inside FinalizeBlock and persist in Commit. Any state mutation elsewhere is a red flag. | ⬜ |
| | External API Calls | No calls in external APIs or hooks can mutate consensus state. | ⬜ |
| **3. Module Security** |
| **Ante Handlers** | Custom Ante Handler Review | Ensure proper fee payment logic (no bypass/vulnerabilities). | ⬜ |
| | Gas Accounting | Check for gas accounting on nested/cross-module calls. | ⬜ |
| | Authz Protection | Guard against Authz (authorization) manipulation or message wrapping that skips checks. | ⬜ |
| **Errors and Codes** | Module Error Codes | Each module must register errors with unique codespace and codes > 1. | ⬜ |
| | Code Reuse | Avoid code reuse between modules. | ⬜ |
| **Token & Address Handling** | Module Address Protection | Blacklist internal/module addresses as token recipients via the x/bank module. | ⬜ |
| | Transfer Validation | Validate all transfers, especially bulk transfers. | ⬜ |
| | Bulk Coin Sends | Prefer transferring coins one-by-one and verify each transfer. Avoid SendCoins batch functions that mask failure of individual sends. | ⬜ |
| | Vesting Accounts | Ensure vesting logic can't halt chain on malformed accounts. | ⬜ |
| **4. Staking and IBC** |
| **Staking Module** | MsgCreateValidator Validation | Validate all fields in MsgCreateValidator (e.g., unique operator address, public keys, proper denom, valid commission rates). | ⬜ |
| | Front-running Protection | Defend against front-running on validator creation. | ⬜ |
| **Inter-Blockchain Communication (IBC)** | Packet Source Verification | Always verify source of IBC packets and validate message data before acting on it. | ⬜ |
| | Privileged Operations | Only trust privileged operations from known channels. | ⬜ |
| | Solo Machine Clients | Consider Solo Machine clients and how they impact trust and permissions. | ⬜ |
| **5. Vote Extensions (ABCI++)** |
| **Implementation** | State Alteration | Never allow vote extension processing or validation to alter app state. | ⬜ |
| | Extension Validation | Validate extensions on both proposal build (PrepareProposal) and vote verification (VerifyVoteExtension). | ⬜ |
| | Non-determinism Watch | Watch for non-determinism and excessive size/latency in extensions. | ⬜ |
| **6. Miscellaneous (Latest Versions)** |
| **sdk.Context Deprecation** | Global State Usage | Avoid use of sdk.Context global state in v0.52+; use appmodule.Environment. | ⬜ |
| **Gas and Consensus Parameters** | Gas Rules Enforcement | Always enforce gas rules in both mempool and consensus. | ⬜ |
| | Consensus Parameter Validation | Validate updates to consensus parameters (no accidental disabling of protections). | ⬜ |

## Notes
- This checklist should be reviewed before each major release
- Pay special attention to items marked as critical for chain security
- Consider this checklist in conjunction with your specific use case requirements
- Regular audits should include verification of these security measures
