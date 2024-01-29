# IUniswapV3StaticQuoter
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/252206c9465648eefefe7b978f4e865682332b87/contracts/interfaces/IUniswapV3StaticQuoter.sol)

Interface for the Eden network Uniswap v3 static quoter with public quote method

*Ref @eden-network/uniswap-v3-static-quoter/contracts/UniV3likeQuoterCore.sol*


## Functions
### quote

Quotes the swap on the Uniswap v3 pool


```solidity
function quote(address poolAddress, bool zeroForOne, int256 amountSpecified, uint160 sqrtPriceLimitX96)
    external
    view
    returns (int256 amount0, int256 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`poolAddress`|`address`|The address of the Uniswap v3 pool|
|`zeroForOne`|`bool`|Whether the swap is token0 in and token1 out|
|`amountSpecified`|`int256`|The amount to send or receive from pool|
|`sqrtPriceLimitX96`|`uint160`|The sqrt price at which to stop swapping|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount0`|`int256`|The amount of token0 in/out to pool|
|`amount1`|`int256`|The amount of token1 in/out to pool|


