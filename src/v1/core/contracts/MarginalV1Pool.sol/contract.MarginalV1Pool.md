# MarginalV1Pool
[Git Source](https://github.com/MarginalProtocol/v1-core/blob/4dcf410464dd1b73aaabe9fa06bd3450c672d3b9/contracts/MarginalV1Pool.sol)

**Inherits:**
[IMarginalV1Pool](/contracts/interfaces/IMarginalV1Pool.sol/interface.IMarginalV1Pool.md), [ERC20](/contracts/test/USDT.sol/contract.ERC20.md)


## State Variables
### factory
The Marginal v1 factory that created the pool


```solidity
address public immutable factory;
```


### oracle
The Uniswap v3 oracle referenced by the pool for funding and position safety


```solidity
address public immutable oracle;
```


### token0
The first of the two tokens of the pool, sorted by address


```solidity
address public immutable token0;
```


### token1
The second of the two tokens of the pool, sorted by address


```solidity
address public immutable token1;
```


### maintenance
The minimum maintenance requirement for leverage positions on the pool


```solidity
uint24 public immutable maintenance;
```


### fee
The pool's fee in hundredths of a bip, i.e. 1e-6


```solidity
uint24 public constant fee = 1000;
```


### rewardPremium
The premium multiplier on liquidation rewards in hundredths of a bip, i.e. 1e-6

*Liquidation rewards set aside in native (gas) token.
Premium acts as an incentive above the expected gas cost to call IMarginalV1Pool#liquidate.*


```solidity
uint24 public constant rewardPremium = 2000000;
```


### tickCumulativeRateMax
The maximum rate of change in tick cumulative between the Marginal v1 pool and the Uniswap v3 oracle

*Puts a ceiling on funding paid per second*


```solidity
uint24 public constant tickCumulativeRateMax = 920;
```


### secondsAgo
The amount of time in seconds to average the Uniswap v3 oracle TWAP over to assess position safety


```solidity
uint32 public constant secondsAgo = 43200;
```


### fundingPeriod
The period in seconds to benchmark funding payments with respect to

*Acts as an averaging period on tick cumulative changes between the Marginal v1 pool and the Uniswap v3 oracle*


```solidity
uint32 public constant fundingPeriod = 604800;
```


### blockBaseFeeMin

```solidity
uint256 internal constant blockBaseFeeMin = 40e9;
```


### gasLiquidate

```solidity
uint256 internal constant gasLiquidate = 150000;
```


### MINIMUM_LIQUIDITY

```solidity
uint128 internal constant MINIMUM_LIQUIDITY = 10000;
```


### MINIMUM_SIZE

```solidity
uint128 internal constant MINIMUM_SIZE = 10000;
```


### state
The pool state represented in (L, sqrt(P)) space


```solidity
State public state;
```


### liquidityLocked
The liquidity used to capitalize outstanding leverage positions


```solidity
uint128 public liquidityLocked;
```


### protocolFees
The amounts of token0 and token1 that are owed to the protocol

*Protocol fees will never exceed uint128 max in either token*


```solidity
ProtocolFees public protocolFees;
```


### positions
Returns information about a leverage position by the position's key

*Either debt0 (zeroForOne = true) or debt1 (zeroForOne = false) will be updated each funding sync*


```solidity
mapping(bytes32 => Position.Info) public positions;
```


### unlocked

```solidity
uint256 private unlocked = 2;
```


## Functions
### lock


```solidity
modifier lock();
```

### onlyFactoryOwner


```solidity
modifier onlyFactoryOwner();
```

### constructor


```solidity
constructor(address _factory, address _token0, address _token1, uint24 _maintenance, address _oracle)
    ERC20("Marginal V1 LP Token", "MARGV1-LP");
```

### initialize


```solidity
function initialize() private;
```

### _blockTimestamp


```solidity
function _blockTimestamp() internal view virtual returns (uint32);
```

### balance0


```solidity
function balance0() private view returns (uint256);
```

### balance1


```solidity
function balance1() private view returns (uint256);
```

### oracleTickCumulatives


```solidity
function oracleTickCumulatives(uint32[] memory secondsAgos) private view returns (int56[] memory);
```

### stateSynced


```solidity
function stateSynced() private view returns (State memory);
```

### open

Opens a leverage position on the pool

*The caller of this method receives a callback in the form of IMarginalV1OpenCallback#marginalV1OpenCallback.
The caller must forward liquidation rewards in the native (gas) token to be escrowed by the pool contract
Rewards determined by current `block.basefee` * estimated gas cost to call IMarginalV1Pool#liquidate * rewardPremium*


```solidity
function open(
    address recipient,
    bool zeroForOne,
    uint128 liquidityDelta,
    uint160 sqrtPriceLimitX96,
    uint128 margin,
    bytes calldata data
) external payable lock returns (uint256 id, uint256 size, uint256 debt, uint256 amount0, uint256 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address of the owner of the opened position|
|`zeroForOne`|`bool`|Whether long token1 and short token0 (true), or long token0 and short token1 (false)|
|`liquidityDelta`|`uint128`|The amount of liquidity for the pool to lock to capitalize the position|
|`sqrtPriceLimitX96`|`uint160`|The Q64.96 sqrt price limit. If zero for one, the price cannot be less than this value after opening the position otherwise the call reverts. If one for zero, the price cannot be greater than this value after opening|
|`margin`|`uint128`|The amount of margin used to back the position in the token the position is long|
|`data`|`bytes`|Any data to be passed through to the callback|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`id`|`uint256`|The ID of the opened position|
|`size`|`uint256`|The size of the opened position in the token the position is long. Excludes margin amount provided by caller|
|`debt`|`uint256`|The debt of the opened position in the token the position is short|
|`amount0`|`uint256`|The amount of token0 caller must send to pool to open the position|
|`amount1`|`uint256`|The amount of token1 caller must send to pool to open the position|


### adjust

Adjusts the margin used to back a position on the pool

*The caller of this method receives a callback in the form of IMarginalV1AdjustCallback#marginalV1AdjustCallback
Old position margin is flashed out to recipient prior to the callback*


```solidity
function adjust(address recipient, uint96 id, int128 marginDelta, bytes calldata data)
    external
    lock
    returns (uint256 margin0, uint256 margin1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address to receive the old position margin|
|`id`|`uint96`|The ID of the position to adjust|
|`marginDelta`|`int128`|The delta of the margin backing the position on the pool. Adding margin to the position when positive, removing margin when negative|
|`data`|`bytes`|Any data to be passed through to the callback|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`margin0`|`uint256`|The amount of token0 to be used as the new margin backing the position|
|`margin1`|`uint256`|The amount of token1 to be used as the new margin backing the position|


### settle

Settles a position on the pool

*The caller of this method receives a callback in the form of IMarginalV1SettleCallback#marginalV1SettleCallback.
If a contract, `recipient` must implement a `receive()` function to receive the escrowed liquidation rewards in the native (gas) token from the pool.
Position size, margin, and liquidation rewards are flashed out before the callback to allow the caller to swap to repay the debt to the pool*


```solidity
function settle(address recipient, uint96 id, bytes calldata data)
    external
    lock
    returns (int256 amount0, int256 amount1, uint256 rewards);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address to receive the size, margin, and liquidation rewards of the settled position|
|`id`|`uint96`|The ID of the position to settle|
|`data`|`bytes`|Any data to be passed through to the callback|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount0`|`int256`|The delta of the balance of token0 of the pool. Position debt into the pool (> 0) if long token1 (zeroForOne = true), or position size and margin out of the pool (< 0) if long token0 (zeroForOne = false)|
|`amount1`|`int256`|The delta of the balance of token1 of the pool. Position size and margin out of the pool (< 0) if long token1 (zeroForOne = true), or position debt into the pool (> 0) if long token0 (zeroForOne = false)|
|`rewards`|`uint256`|The amount of escrowed native (gas) token sent to `recipient`|


### liquidate

Liquidates a position on the pool

*Reverts if position is safe from liquidation. Position is considered safe if
(`position.margin` + `position.size`) / oracleTwap >= (1 + `maintenance`) * `position.debt0` when position.zeroForOne = true
(`position.margin` + `position.size`) * oracleTwap >= (1 + `maintenance`) * `position.debt1` when position.zeroForOne = false
Safety checks are performed after syncing the position debts for funding payments
If a contract, `recipient` must implement a `receive()` function to receive the escrowed liquidation rewards in the native (gas) token from the pool.*


```solidity
function liquidate(address recipient, address owner, uint96 id) external lock returns (uint256 rewards);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address to receive liquidation rewards escrowed with the position|
|`owner`|`address`|The address of the owner of the position to liquidate|
|`id`|`uint96`|The ID of the position to liquidate|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`rewards`|`uint256`|The amount of escrowed native (gas) token sent to `recipient`|


### swap

Swap token0 for token1, or token1 for token0

*The caller of this method receives a callback in the form of IMarginalV1SwapCallback#marginalV1SwapCallback*


```solidity
function swap(
    address recipient,
    bool zeroForOne,
    int256 amountSpecified,
    uint160 sqrtPriceLimitX96,
    bytes calldata data
) external lock returns (int256 amount0, int256 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address to receive the output of the swap|
|`zeroForOne`|`bool`|The direction of the swap, true for token0 to token1, false for token1 to token0|
|`amountSpecified`|`int256`|The amount of the swap, which implicitly configures the swap as exact input (positive), or exact output (negative)|
|`sqrtPriceLimitX96`|`uint160`|The Q64.96 sqrt price limit. If zero for one, the price cannot be less than this value after the swap otherwise the call reverts. If one for zero, the price cannot be greater than this value after the swap|
|`data`|`bytes`|Any data to be passed through to the callback|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount0`|`int256`|The delta of the balance of token0 of the pool, exact when negative, minimum when positive|
|`amount1`|`int256`|The delta of the balance of token1 of the pool, exact when negative, minimum when positive|


### mint

Adds liquidity to the pool

*The caller of this method receives a callback in the form of IMarginalV1MintCallback#marginalV1MintCallback.
The pool is initialized through the first call to mint*


```solidity
function mint(address recipient, uint128 liquidityDelta, bytes calldata data)
    external
    lock
    returns (uint256 shares, uint256 amount0, uint256 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address to mint LP tokens to after adding liquidity to the pool|
|`liquidityDelta`|`uint128`|The liquidity added to the pool|
|`data`|`bytes`|Any data to be passed through to the callback|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`shares`|`uint256`|The amount of LP token shares minted to recipient|
|`amount0`|`uint256`|The amount of token0 added to the pool reserves|
|`amount1`|`uint256`|The amount of token1 added to the pool reserves|


### burn

Removes liquidity from the pool

*Reverts if not enough liquidity available to exit due to outstanding leverage positions*


```solidity
function burn(address recipient, uint256 shares)
    external
    lock
    returns (uint128 liquidityDelta, uint256 amount0, uint256 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address to send token amounts to after removing liquidity from the pool|
|`shares`|`uint256`|The amount of LP token shares to burn|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`liquidityDelta`|`uint128`|The liquidity removed from the pool|
|`amount0`|`uint256`|The amount of token0 removed from pool reserves|
|`amount1`|`uint256`|The amount of token1 removed from pool reserves|


### setFeeProtocol

Set the denominator of the protocol's % share of the fees


```solidity
function setFeeProtocol(uint8 feeProtocol) external lock onlyFactoryOwner;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`feeProtocol`|`uint8`|new protocol fee denominator for the pool|


### collectProtocol

Collect the protocol fee accrued to the pool


```solidity
function collectProtocol(address recipient) external lock onlyFactoryOwner returns (uint128 amount0, uint128 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address to which collected protocol fees should be sent|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount0`|`uint128`|The protocol fee collected in token0|
|`amount1`|`uint128`|The protocol fee collected in token1|


## Events
### Initialize

```solidity
event Initialize(uint160 sqrtPriceX96, int24 tick);
```

### Open

```solidity
event Open(
    address sender,
    address indexed owner,
    uint256 indexed id,
    uint128 liquidityAfter,
    uint160 sqrtPriceX96After,
    uint128 margin
);
```

### Adjust

```solidity
event Adjust(address indexed owner, uint256 indexed id, address recipient, uint256 marginAfter);
```

### Settle

```solidity
event Settle(
    address indexed owner,
    uint256 indexed id,
    address recipient,
    uint128 liquidityAfter,
    uint160 sqrtPriceX96After,
    int256 amount0,
    int256 amount1,
    uint256 rewards
);
```

### Liquidate

```solidity
event Liquidate(
    address indexed owner,
    uint256 indexed id,
    address recipient,
    uint128 liquidityAfter,
    uint160 sqrtPriceX96After,
    uint256 rewards
);
```

### Swap

```solidity
event Swap(
    address indexed sender,
    address indexed recipient,
    int256 amount0,
    int256 amount1,
    uint160 sqrtPriceX96,
    uint128 liquidity,
    int24 tick
);
```

### Mint

```solidity
event Mint(address sender, address indexed owner, uint128 liquidityDelta, uint256 amount0, uint256 amount1);
```

### Burn

```solidity
event Burn(address indexed owner, address recipient, uint128 liquidityDelta, uint256 amount0, uint256 amount1);
```

### SetFeeProtocol

```solidity
event SetFeeProtocol(uint8 oldFeeProtocol, uint8 newFeeProtocol);
```

### CollectProtocol

```solidity
event CollectProtocol(address sender, address indexed recipient, uint128 amount0, uint128 amount1);
```

## Errors
### Locked

```solidity
error Locked();
```

### Unauthorized

```solidity
error Unauthorized();
```

### InvalidLiquidityDelta

```solidity
error InvalidLiquidityDelta();
```

### InvalidSqrtPriceLimitX96

```solidity
error InvalidSqrtPriceLimitX96();
```

### SqrtPriceX96ExceedsLimit

```solidity
error SqrtPriceX96ExceedsLimit();
```

### MarginLessThanMin

```solidity
error MarginLessThanMin();
```

### RewardsLessThanMin

```solidity
error RewardsLessThanMin();
```

### Amount0LessThanMin

```solidity
error Amount0LessThanMin();
```

### Amount1LessThanMin

```solidity
error Amount1LessThanMin();
```

### InvalidPosition

```solidity
error InvalidPosition();
```

### PositionSafe

```solidity
error PositionSafe();
```

### InvalidAmountSpecified

```solidity
error InvalidAmountSpecified();
```

### InvalidFeeProtocol

```solidity
error InvalidFeeProtocol();
```

## Structs
### State

```solidity
struct State {
    uint160 sqrtPriceX96;
    uint96 totalPositions;
    uint128 liquidity;
    int24 tick;
    uint32 blockTimestamp;
    int56 tickCumulative;
    uint8 feeProtocol;
    bool initialized;
}
```

### ProtocolFees

```solidity
struct ProtocolFees {
    uint128 token0;
    uint128 token1;
}
```

