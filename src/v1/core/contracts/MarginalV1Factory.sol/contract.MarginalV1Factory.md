# MarginalV1Factory
[Git Source](https://github.com/MarginalProtocol/v1-core/blob/2d246e9b4f6e970321a0f235176b47b340c9a03b/contracts/MarginalV1Factory.sol)

**Inherits:**
[IMarginalV1Factory](/contracts/interfaces/IMarginalV1Factory.sol/interface.IMarginalV1Factory.md)


## State Variables
### marginalV1Deployer
Returns the Marginal v1 pool deployer to use when creating pools


```solidity
address public immutable marginalV1Deployer;
```


### uniswapV3Factory
Returns the Uniswap v3 factory to reference for pool oracles


```solidity
address public immutable uniswapV3Factory;
```


### observationCardinalityMinimum
Returns the minimum observation cardinality the Uniswap v3 oracle must have

*Used as a check that averaging over `secondsAgo` in the Marginal v1 pool is likely to succeed*


```solidity
uint16 public immutable observationCardinalityMinimum;
```


### owner
Returns the current owner of the Marginal v1 factory contract

*Changed via permissioned `setOwner` function on the factory*


```solidity
address public owner;
```


### getPool
Returns the pool address for the given unique Marginal v1 pool key

*tokenA and tokenB may be passed in either token0/token1 or token1/token0 order*


```solidity
mapping(address => mapping(address => mapping(uint24 => mapping(address => address)))) public getPool;
```


### isPool
Returns whether given address is a Marginal v1 pool deployed by the factory


```solidity
mapping(address => bool) public isPool;
```


### getLeverage
Returns the maximum leverage associated with the pool maintenance if pool exists


```solidity
mapping(uint24 => uint256) public getLeverage;
```


## Functions
### constructor


```solidity
constructor(address _marginalV1Deployer, address _uniswapV3Factory, uint16 _observationCardinalityMinimum);
```

### createPool

Creates a new Marginal v1 pool for the given unique pool key

*tokenA and tokenB may be passed in either token0/token1 or token1/token0 order*


```solidity
function createPool(address tokenA, address tokenB, uint24 maintenance, uint24 uniswapV3Fee)
    external
    returns (address pool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenA`|`address`|The address of either token0/token1|
|`tokenB`|`address`|The address of the other token token1/token0|
|`maintenance`|`uint24`|The minimum maintenance requirement for the pool|
|`uniswapV3Fee`|`uint24`|The fee tier of the Uniswap v3 oracle used by the Marginal v1 pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`pool`|`address`|The address of the created Marginal v1 pool|


### setOwner

Sets the owner of the Marginal v1 factory contract

*Can only be called by the current factory owner*


```solidity
function setOwner(address _owner) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`_owner`|`address`|The new owner of the factory|


### enableLeverage

Enables a new leverage tier for Marginal v1 pool deployments

*Can only be called by the current factory owner*


```solidity
function enableLeverage(uint24 maintenance) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`maintenance`|`uint24`|The minimum maintenance requirement associated with the leverage tier|


## Events
### PoolCreated

```solidity
event PoolCreated(
    address indexed token0, address indexed token1, uint24 maintenance, address indexed oracle, address pool
);
```

### LeverageEnabled

```solidity
event LeverageEnabled(uint24 maintenance, uint256 leverage);
```

### OwnerChanged

```solidity
event OwnerChanged(address indexed oldOwner, address indexed newOwner);
```

## Errors
### Unauthorized

```solidity
error Unauthorized();
```

### InvalidMaintenance

```solidity
error InvalidMaintenance();
```

### InvalidOracle

```solidity
error InvalidOracle();
```

### InvalidObservationCardinality

```solidity
error InvalidObservationCardinality(uint16 observationCardinality);
```

### PoolActive

```solidity
error PoolActive();
```

### LeverageActive

```solidity
error LeverageActive();
```

