# SilverToken Smart Contract

## Overview

The `SilverToken` smart contract is an ERC20-compliant token built on the Ethereum blockchain using the OpenZeppelin library. It includes several features such as minting, burning, and transferring tokens. Additionally, it incorporates access control mechanisms to ensure that certain functions can only be executed by the contract owner.

## Features

- **Minting**: The owner can mint new tokens.
- **Burning**: Token holders can burn their own tokens.
- **Transfer**: Tokens can be transferred between addresses.
- **Access Control**: Only the contract owner can mint new tokens or increase the total supply.

## Prerequisites

Before deploying the `SilverToken` contract, ensure that you have the following installed:

- Node.js
- npm (Node Package Manager)
- Truffle or Hardhat
- MetaMask (or any Ethereum wallet)

## Dependencies

This contract utilizes OpenZeppelin's library. Ensure you have the OpenZeppelin contracts installed:

```bash
npm install @openzeppelin/contracts
```

## Contract Details

### Constructor

```solidity
constructor(
    string memory tokenName,
    string memory tokenSymbol,
    uint256 initialSupply,
    address initialOwner
) ERC20(tokenName, tokenSymbol) Ownable(initialOwner) {
    _mint(msg.sender, initialSupply);
}
```

- **Parameters**:
  - `tokenName`: The name of the token.
  - `tokenSymbol`: The symbol of the token.
  - `initialSupply`: The initial supply of tokens.
  - `initialOwner`: The address of the initial owner of the contract.

### Functions

#### Mint Tokens

```solidity
function mintTokens(address recipient, uint256 amount) external onlyOwner {
    require(recipient != address(0), "Mint: recipient is the zero address");
    require(amount > 0, "Mint: amount must be greater than zero");
    _mint(recipient, amount);
}
```

- Mints new tokens to a specified address.
- Only callable by the contract owner.

#### Burn Tokens

```solidity
function burnTokens(uint256 amount) external {
    require(amount > 0, "Burn: amount must be greater than zero");
    _burn(msg.sender, amount);
}
```

- Burns a specified amount of tokens from the caller's account.

#### Increase Total Supply

```solidity
function increaseTotalSupply(uint256 additionalSupply) external onlyOwner {
    require(additionalSupply > 0, "Increase Supply: additional supply must be greater than zero");
    _mint(owner(), additionalSupply);
}
```

- Increases the total supply of tokens.
- Only callable by the contract owner.

#### Transfer Tokens

```solidity
function transferTokens(address recipient, uint256 amount) public virtual returns (bool) {
    require(recipient != address(0), "Transfer: recipient is the zero address");
    require(amount > 0, "Transfer: amount must be greater than zero");
    _transfer(_msgSender(), recipient, amount);
    return true;
}
```

- Transfers tokens from the caller to a specified recipient.


Contributions are welcome!
