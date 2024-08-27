# DevSToken

A custom ERC20 token contract implementing minting, burning, and transfer functionalities.

## Description

`DevSToken` is a Solidity smart contract that extends the ERC20 standard to include custom functionalities for minting and burning tokens. The contract allows the owner to mint new tokens and enables token holders to burn their own tokens. This contract demonstrates how to build and deploy a basic ERC20 token with added features.

## Getting Started

### Installing

No installation is required. Simply paste the provided code into a Solidity-compatible IDE like Remix Ethereum IDE.

### Executing Program

1. Open [Remix Ethereum IDE](https://remix.ethereum.org/).
2. Create a new file and paste the contract code into it.
3. Compile the contract by selecting the Solidity compiler and clicking the "Compile" button.
4. Deploy the contract by selecting the "Deploy" option from the "Deploy & Run Transactions" tab.
5. Interact with the contract using the provided functions (mint, burn, transfer) in the Remix interface.

```solidity

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract DevSToken is ERC20 {
    // Public variables here
    string public tokenName = "DevSToken";
    string public abbrv = "DST";
    address public owner;

    // Constructor to set the owner and initialize the ERC20 token
    constructor() ERC20(tokenName, abbrv) {
        owner = msg.sender;
    }

    // Modifier to check if the caller is the owner
    modifier onlyOwner() {
        require(msg.sender == owner, "Only the owner can perform this action");
        _;
    }

    // Modifier to check if the caller is the token holder
    modifier onlyHolder(address _add) {
        require(msg.sender == _add, "You can only burn your own tokens");
        _;
    }

    // Mint function
    function mint(address _add, uint _val) public onlyOwner {
        _mint(_add, _val);
    }

    // Burn function
    function burn(address _add, uint _val) public onlyHolder(_add) {
        require(balanceOf(_add) >= _val, "Insufficient balance");
        _burn(_add, _val);
    }

    // Transfer function
    function transfer(address _trans, uint _val) public override returns (bool) {
        require(_trans != address(0), "Invalid address");
        require(_val <= balanceOf(msg.sender), "Insufficient balance");
        
        _transfer(msg.sender, _trans, _val);
        return true;
    }
```

## Help

For any issues or questions, refer to the provided [code explanation video](https://www.loom.com/share/af2b1e61f1d742b196643d06ff62263e?sid=d816f83c-f7ac-4640-aa9c-84997b4068a6).

## Authors

Dev Sagar  
[@DevSGitub2](https://github.com/DevSGitub2)

## License

This project is licensed under the MIT License - see the [LICENSE.md]([LICENSE.md](https://github.com/DevSGitub2/ETH-AVAX-Module-3/blob/main/LICENSE)) file for details.










