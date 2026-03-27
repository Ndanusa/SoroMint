# Metadata Updates

This document outlines the protocol for updating token metadata (Name and Symbol) in the SoroMint contract.

## Overview

The SoroMint contract allows the administrator to update the token's name and symbol after deployment. This ensures the token can evolve or correct naming errors without requiring a full redeployment or affecting user balances.

## Requirements

1. **Administrative Access**: Only the address currently designated as the `Admin` of the contract can initiate metadata updates.
2. **Immutability of Decimals**: The `decimals` value of the token is fixed at deployment and cannot be changed. This ensures consistency for calculations and integrations.
3. **Event Emissions**: Every update to the name or symbol emits a corresponding event, ensuring transparency for all participants.

## Functions

### `set_name`

Updates the display name of the token.

- **Parameters**: `name: String`
- **Authorization**: Requires `Admin` signature.
- **Events**: Emits `name_upd(old_name, new_name)`.

### `set_symbol`

Updates the ticker symbol of the token.

- **Parameters**: `symbol: String`
- **Authorization**: Requires `Admin` signature.
- **Events**: Emits `sym_upd(old_symbol, new_symbol)`.

## Security Considerations

- **Authorization**: The contract uses `admin.require_auth()` to ensure only the authorized administrator can change these values.
- **Integrity**: Changing Name/Symbol does not impact `balance`, `supply`, or any existing transaction history.

## Example Usage (CLI)

```bash
soroban contract invoke \
  --id [CONTRACT_ID] \
  --source [ADMIN_SECRET] \
  --network [NETWORK] \
  -- \
  set_name --name "New Token Name"
```
