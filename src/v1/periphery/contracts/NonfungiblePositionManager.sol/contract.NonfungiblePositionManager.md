# NonfungiblePositionManager
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/1d4c6a63a24ea055be056199b2cac6431f68ec06/contracts/NonfungiblePositionManager.sol)

**Inherits:**
[INonfungiblePositionManager](/contracts/interfaces/INonfungiblePositionManager.sol/interface.INonfungiblePositionManager.md), Multicall, ERC721, [PeripheryImmutableState](/contracts/base/PeripheryImmutableState.sol/abstract.PeripheryImmutableState.md), [PositionManagement](/contracts/base/PositionManagement.sol/abstract.PositionManagement.md), [PositionState](/contracts/base/PositionState.sol/abstract.PositionState.md), PeripheryValidation

Wraps Marginal v1 leverage positions in the ERC721 non-fungible token interface


## State Variables
### _positions

```solidity
mapping(uint256 => Position) private _positions;
```


### _nextId

```solidity
uint256 private _nextId = 1;
```


## Functions
### onlyApprovedOrOwner


```solidity
modifier onlyApprovedOrOwner(uint256 tokenId);
```

### constructor


```solidity
constructor(address _factory, address _WETH9)
    ERC721("Marginal V1 Position Token", "MRGLV1-POS")
    PeripheryImmutableState(_factory, _WETH9);
```

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


```solidity
function mint(MintParams calldata params)
    external
    payable
    checkDeadline(params.deadline)
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
function lock(LockParams calldata params)
    external
    payable
    onlyApprovedOrOwner(params.tokenId)
    checkDeadline(params.deadline)
    returns (uint256 margin);
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
function free(FreeParams calldata params)
    external
    payable
    onlyApprovedOrOwner(params.tokenId)
    checkDeadline(params.deadline)
    returns (uint256 margin);
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


```solidity
function burn(BurnParams calldata params)
    external
    payable
    onlyApprovedOrOwner(params.tokenId)
    checkDeadline(params.deadline)
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
|`rewards`|`uint256`|The amount of escrowed liquidation rewards in native (gas) token received after settling position|


### ignite

Burns an existing position, settling on pool via swap through spot


```solidity
function ignite(IgniteParams calldata params)
    external
    payable
    onlyApprovedOrOwner(params.tokenId)
    checkDeadline(params.deadline)
    returns (uint256 amountOut, uint256 rewards);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`IgniteParams`|The parameters necessary for settling the position, encoded as `IgniteParams` in calldata|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|The amount of margin token received after settling position|
|`rewards`|`uint256`|The amount of escrowed liquidation rewards in native (gas) token received after settling position|


### grab

Grabs an existing position, liquidating on pool


```solidity
function grab(GrabParams calldata params) external payable checkDeadline(params.deadline) returns (uint256 rewards);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`GrabParams`|The parameters necessary for liquidating a position, encoded as `GrabParams` in calldata|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`rewards`|`uint256`|The amount of escrowed liquidation rewards in native (gas) token received after liquidating the position|


## Events
### Mint

```solidity
event Mint(
    uint256 indexed tokenId,
    address indexed recipient,
    uint256 positionId,
    uint256 size,
    uint256 debt,
    uint256 margin,
    uint256 fees,
    uint256 rewards
);
```

### Lock

```solidity
event Lock(uint256 indexed tokenId, address indexed recipient, uint256 marginAfter);
```

### Free

```solidity
event Free(uint256 indexed tokenId, address indexed recipient, uint256 marginAfter);
```

### Burn

```solidity
event Burn(uint256 indexed tokenId, address indexed recipient, uint256 amountIn, uint256 amountOut, uint256 rewards);
```

### Ignite

```solidity
event Ignite(uint256 indexed tokenId, address indexed recipient, uint256 amountOut, uint256 rewards);
```

### Grab

```solidity
event Grab(uint256 indexed tokenId, address indexed recipient, uint256 rewards);
```

## Errors
### Unauthorized

```solidity
error Unauthorized();
```

### InvalidPoolKey

```solidity
error InvalidPoolKey();
```

## Structs
### Position

```solidity
struct Position {
    address pool;
    uint96 id;
}
```

