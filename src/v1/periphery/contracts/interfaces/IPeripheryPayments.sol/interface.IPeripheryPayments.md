# IPeripheryPayments
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/6ce65434509972d6f67aeab3e318f9db63a09fe0/contracts/interfaces/IPeripheryPayments.sol)

Functions to ease deposits and withdrawals of ETH


## Functions
### unwrapWETH9

Unwraps the contract's WETH9 balance and sends it to recipient as ETH.

*The amountMinimum parameter prevents malicious contracts from stealing WETH9 from users.*


```solidity
function unwrapWETH9(uint256 amountMinimum, address recipient) external payable;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountMinimum`|`uint256`|The minimum amount of WETH9 to unwrap|
|`recipient`|`address`|The address receiving ETH|


### refundETH

Refunds any ETH balance held by this contract to the `msg.sender`

*Useful for bundling with mint or increase liquidity that uses ether, or exact output swaps
that use ether for the input amount*


```solidity
function refundETH() external payable;
```

### sweepToken

Transfers the full amount of a token held by this contract to recipient

*The amountMinimum parameter prevents malicious contracts from stealing the token from users*


```solidity
function sweepToken(address token, uint256 amountMinimum, address recipient) external payable;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|The contract address of the token which will be transferred to `recipient`|
|`amountMinimum`|`uint256`|The minimum amount of token required for a transfer|
|`recipient`|`address`|The destination address of the token|


### sweepETH

Transfers the full amount of ETH held by this contract to recipient

*The amountMinimum parameter prevents malicious contracts from stealing the ETH from users*


```solidity
function sweepETH(uint256 amountMinimum, address recipient) external payable;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountMinimum`|`uint256`|The minimum amount of ETH required for a transfer|
|`recipient`|`address`|The destination address of the ETH|


