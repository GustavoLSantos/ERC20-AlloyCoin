# AlloyCoin Smart Contract

This is a simple Solidity smart contract named AlloyCoin that represents a basic cryptocurrency. The contract allows for minting new coins and transferring them between addresses.
Table of Contents

## Overview

The AlloyCoin contract is designed to create a basic cryptocurrency with a designated minter who can mint new coins and distribute them to other addresses. The contract also enables users to check their balances and transfer coins to other addresses.

## Features

* Minting Coins:
  Only the designated minter (set during contract deployment) can mint new coins.
  The mint function is used to create new coins and assign them to a specified address.

* Checking Balances:
  Users can query their coin balances using the balances mapping.

* Transferring Coins:
  Users can send coins to other addresses using the send function.
  An insufficientBalance error is triggered if a user tries to send more coins than they have.

* Events:
  The contract emits a Sent event whenever coins are successfully transferred.

## Usage

* Minting Coins:
  Call the mint function, specifying the recipient's address and the amount to be minted.

~~~solidity
function mint(address receiver, uint amount) public {
    // Requires that the sender is the designated minter
    require(msg.sender == minter, "The sender is not the minter");

    // Mint new coins and assign them to the specified address
    balances[receiver] += amount;
}
~~~

* Transfering Coins: Call the send function, specifying the recipient's address and the amount to be transferred.

~~~solidity
    function send(address receiver, uint amount) public {
        // Check if the sender has sufficient balance
        if(amount > balances[msg.sender])
            revert insufficientBalance({
                requested: amount,
                available: balances[msg.sender]
            });

        // Transfer coins from the sender to the recipient
        balances[msg.sender] -= amount;
        balances[receiver] += amount;

        // Emit the Sent event
        emit Sent(msg.sender, receiver, amount);
    }
~~~

* Checking Balances: Use the balances mapping to query the balance of a specific address.

## License

This smart contract is released under the UNLICENSED license. See LICENSE for more details.
