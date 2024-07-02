# INonfungiblePositionManager
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/d846d56fa6d1e439306e60a85e98fc298babb2f7/contracts/interfaces/INonfungiblePositionManager.sol)

**Inherits:**
IERC721Metadata

Wraps Marginal v1 leverage positions in a non-fungible token to allow for transfers


## Functions
### positions

Returns details of an existing position

*Do *NOT* use in callback. Vulnerable to re-entrancy view issues.*


```solidity
function positions(uint256 tokenId)
    external
    view
    returns (
        address pool,
        uint96 positionId,
        bool zeroForOne,
        uint128 size,
        uint128 debt,
        uint128 margin,
        uint128 safeMarginMinimum,
        bool liquidated,
        bool safe,
        uint256 rewards
    );
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenId`|`uint256`|The NFT token id associated with the position|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`pool`|`address`|The pool address position taken out on|
|`positionId`|`uint96`|The position ID stored in the pool for the associated position|
|`zeroForOne`|`bool`|Whether position settlement requires debt in of token0 for size + margin out of token1|
|`size`|`uint128`|The position size on the pool in the margin token|
|`debt`|`uint128`|The position debt owed to the pool in the non-margin token|
|`margin`|`uint128`|The margin backing the position on the pool|
|`safeMarginMinimum`|`uint128`|The minimum margin requirements necessary to keep position open on pool while also being safe from liquidation|
|`liquidated`|`bool`|Whether the position has been liquidated|
|`safe`|`bool`|Whether the position can be liquidated|
|`rewards`|`uint256`|The reward available to liquidators when position not safe|


### mint

Mints a new position, opening on pool

*If a contract, `msg.sender` must implement a `receive()` function to receive any refunded excess liquidation rewards in the native (gas) token from the manager.*


```solidity
function mint(MintParams calldata params)
    external
    payable
    returns (uint256 tokenId, uint256 size, uint256 debt, uint256 margin, uint256 fees, uint256 rewards);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`MintParams`|The parameters necessary for the position mint, encoded as `MintParams` in calldata|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`tokenId`|`uint256`|The NFT token id associated with the minted position|
|`size`|`uint256`|The position size on the pool in the margin token|
|`debt`|`uint256`|The position debt owed to the pool in the non-margin token|
|`margin`|`uint256`|The amount of margin token in used to open the position|
|`fees`|`uint256`|The amount of fees in margin token paid to open the position|
|`rewards`|`uint256`|The amount of liquidation rewards in native (gas) token escrowed in opened position|


### lock

*Adds margin to an existing position*


```solidity
function lock(LockParams calldata params) external payable returns (uint256 margin);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`LockParams`|The parameters necessary for adding margin to the position, encoded as `LockParams` in calldata|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`margin`|`uint256`|The margin backing the position after calling lock|


### free

Removes margin from an existing position


```solidity
function free(FreeParams calldata params) external returns (uint256 margin);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`FreeParams`|The parameters necessary for removing margin from the position, encoded as `FreeParams` in calldata|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`margin`|`uint256`|The margin backing the position after calling free|


### burn

Burns an existing position, settling on pool via external payer

*If a contract, `msg.sender` must implement a `receive()` function to receive any refunded excess debt payment in the native (gas) token from the manager.*


```solidity
function burn(BurnParams calldata params)
    external
    payable
    returns (uint256 amountIn, uint256 amountOut, uint256 rewards);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`BurnParams`|The parameters necessary for settling the position, encoded as `BurnParams` in calldata|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountIn`|`uint256`|The amount of debt token in used to settle position|
|`amountOut`|`uint256`|The amount of margin token received after settling position|
|`rewards`|`uint256`|The amount of escrowed liquidation rewards in native (gas) token released by pool after settling position|


### ignite

Burns an existing position, settling on pool via swap through spot

*If a contract, `recipient` must implement a `receive()` function to receive any excess liquidation rewards unused by the spot swap in the native (gas) token from the manager.*


```solidity
function ignite(IgniteParams calldata params) external returns (uint256 amountOut, uint256 rewards);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`IgniteParams`|The parameters necessary for settling the position, encoded as `IgniteParams` in calldata|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|The amount of margin token received after settling position|
|`rewards`|`uint256`|The amount of escrowed liquidation rewards in native (gas) token released by pool after settling position|


## Structs
### MintParams

```solidity
struct MintParams {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    bool zeroForOne;
    uint128 sizeDesired;
    uint128 sizeMinimum;
    uint128 debtMaximum;
    uint256 amountInMaximum;
    uint160 sqrtPriceLimitX96;
    uint128 margin;
    address recipient;
    uint256 deadline;
}
```

### LockParams

```solidity
struct LockParams {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    uint256 tokenId;
    uint128 marginIn;
    uint256 deadline;
}
```

### FreeParams

```solidity
struct FreeParams {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    uint256 tokenId;
    uint128 marginOut;
    address recipient;
    uint256 deadline;
}
```

### BurnParams

```solidity
struct BurnParams {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    uint256 tokenId;
    address recipient;
    uint256 deadline;
}
```

### IgniteParams

```solidity
struct IgniteParams {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    uint256 tokenId;
    uint256 amountOutMinimum;
    address recipient;
    uint256 deadline;
}
```

