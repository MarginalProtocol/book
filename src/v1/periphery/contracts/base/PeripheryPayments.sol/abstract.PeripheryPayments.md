# PeripheryPayments
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/d846d56fa6d1e439306e60a85e98fc298babb2f7/contracts/base/PeripheryPayments.sol)

**Inherits:**
[IPeripheryPayments](/contracts/interfaces/IPeripheryPayments.sol/interface.IPeripheryPayments.md), [PeripheryImmutableState](/contracts/base/PeripheryImmutableState.sol/abstract.PeripheryImmutableState.md)


## Functions
### receive


```solidity
receive() external payable;
```

### unwrapWETH9

Unwraps the contract's WETH9 balance and sends it to recipient as ETH.

*The amountMinimum parameter prevents malicious contracts from stealing WETH9 from users.*


```solidity
function unwrapWETH9(uint256 amountMinimum, address recipient) public payable override;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountMinimum`|`uint256`|The minimum amount of WETH9 to unwrap|
|`recipient`|`address`|The address receiving ETH|


### sweepToken

Transfers the full amount of a token held by this contract to recipient

*The amountMinimum parameter prevents malicious contracts from stealing the token from users*


```solidity
function sweepToken(address token, uint256 amountMinimum, address recipient) public payable override;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|The contract address of the token which will be transferred to `recipient`|
|`amountMinimum`|`uint256`|The minimum amount of token required for a transfer|
|`recipient`|`address`|The destination address of the token|


### refundETH

Refunds any ETH balance held by this contract to the `msg.sender`

*Useful for bundling with mint or increase liquidity that uses ether, or exact output swaps
that use ether for the input amount*


```solidity
function refundETH() public payable override;
```

### sweepETH

Transfers the full amount of ETH held by this contract to recipient

*The amountMinimum parameter prevents malicious contracts from stealing the ETH from users*


```solidity
function sweepETH(uint256 amountMinimum, address recipient) public payable;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountMinimum`|`uint256`|The minimum amount of ETH required for a transfer|
|`recipient`|`address`|The destination address of the ETH|


### wrapETH

Wraps balance of native (gas) token in contract to WETH9


```solidity
function wrapETH() internal;
```

### pay

Pay ERC20 token to recipient


```solidity
function pay(address token, address payer, address recipient, uint256 value) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|The token to pay|
|`payer`|`address`|The entity that must pay|
|`recipient`|`address`|The entity that will receive payment|
|`value`|`uint256`|The amount to pay|


### balance

Balance of ERC20 token held by this contract


```solidity
function balance(address token) internal view returns (uint256 value);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|The token to check|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`value`|`uint256`|The balance amount|


