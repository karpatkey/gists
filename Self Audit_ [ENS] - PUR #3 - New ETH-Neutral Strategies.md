---
title: 'Internal - Self Audit: [ENS] - PUR #3 - New ETH-Neutral Strategies'
tags: [' treasury', ens, preset_update]

---

# Self Audit: [ENS] - PUR #3 - New ETH-Neutral Strategies

This is an attempt into improved transparency and efficiency for preset update requests. It aims to make payloads readable and summarize the most relevant information for stakeholders to quickly be able to understand proposed changes.

You can find the payload in the proposal: [Self Audit: [ENS] - PUR #3 - New ETH-Neutral Strategies]()

Transactions included in the payload consist of one of the folowing two categories:
- ERC20 token approvals: approvals are necessary for interacting with relevant smart contracts for treasury strategy
- Scope changes applied to the [Roles](https://etherscan.io/address/0xf20325cf84b72e8bbf8d8984b8f0059b984b390b) contract, which handles permissions given to karpatkey to execute on the [Avatar Safe](https://app.safe.global/home?safe=eth:0x4F2083f5fBede34C2714aFfb3105539775f7FE64)

All function calls generate events that contain the data needed to understand the actions being executed. So the result of the succesfull execution can be understood by simulating the payload execution and analysing emitted events.

This simulation was done using Tenderly. This is the [Tenderly Simulation Link](https://dashboard.tenderly.co/public/safe/safe-apps/simulator/5605f593-5723-45fa-8484-88eb41d5c231).

There are a total of 92 transactions included in the preset update. Each of this actions has an `id` which links the description to the corresponding position in the payload, for treaceability. The actions consist of:
* 28 `approvals`
* 18 `scopeTarget`
* 4 `revokeTarget`
* 4 `scopeAllowFunction`
* 20 `scopeFunction`
* 2 `scopeRevokeFunction`
* 16 `scopeParameterAsOneOf`

## Approval

ERC20 token approvals are needed to interact with the contracts of interest. Events emitted have the following structure (and they get emitted by the token contract that's being approved for spending):

```
event Approval(address owner, address spender, uint256 value)
```

In all cases the owner is the [Avatar Safe](https://etherscan.io/address/0x4F2083f5fBede34C2714aFfb3105539775f7FE64) and the value is infinite. There are also revokes which have `value = 0`.

### Approvals

| id | token | spender |
|-----|-------|---------|
| 0 | 0x4d5f47fa6a74757f35c14fd3a6ef8e3c9bc514e8 (aave_v3:aEthWETH) | 0xd322a49006fc828f9b5b37ab215f99b4e5cab19c (aave_v3:WRAPPED_TOKEN_GATEWAY_V3) |
| 1 | 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2 (WETH) | 0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2 (aave_v3:POOL_V3) |
| 2 | 0xe95a203b1a91a908f9b9ce46459d101078c2c3cb (aETHc) | 0xf047f23acfdb1315cf63ad8ab5146d5fda4267af (ankr:SWAP_POOL) |
| 3 | 0xa35b1b31ce002fbf2058d22f30f95d405200a15b (stader:ETHx) | 0x9f0491b32dbce587c50c4c43ab303b06478193a7 (stader:USER_WITHDRAWAL_MANAGER) |
| 4 | 0x59cd1c87501baa753d0b5b5ab5d8416a45cd71db (spark:spWETH) | 0xbd7d6a9ad7865463de44b05f04559f65e3b11704 (spark:WRAPPED_TOKEN_GATEWAY_V3) |
| 5 | 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2 (WETH) | 0xc13e21b648a5ee794902342038ff3adab66be987 (spark:LENDING_POOL_V3) |
| 6 | 0xae78736cd615f374d3085123a210448e74fc6393 (rETH) | 0x68b3465833fb72a70ecdf485e0e4c7bd8665fc45 (uniswapv3:ROUTER_2) |
| 7 | 0xe95a203b1a91a908f9b9ce46459d101078c2c3cb (aETHc) | 0xba12222222228d8ba445958a75a0704d566bf2c8 (balancer:VAULT) |
| 8 | 0xa35b1b31ce002fbf2058d22f30f95d405200a15b (stader:ETHx) | 0xba12222222228d8ba445958a75a0704d566bf2c8 (balancer:VAULT) |
| 9 | 0xe95a203b1a91a908f9b9ce46459d101078c2c3cb (aETHc) | 0xa96a65c051bf88b4095ee1f2451c2a9d43f53ae2 (curve:ankrETH_POOL) |
| 10 | 0xa35b1b31ce002fbf2058d22f30f95d405200a15b (stader:ETHx) | 0x13f4ea83d0bd40e75c8222255bc855a974568dd4 (pancake_swap:SMART_ROUTER) |
| 11 | 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2 (WETH) | 0x13f4ea83d0bd40e75c8222255bc855a974568dd4 (pancake_swap:SMART_ROUTER) |
| 20 | 0xc00e94cb662c3520282e6f5717214004a7f26888 (COMP) | 0x5550d13389bb70f45fcef58f19f6b6e87f6e747d (sushiswap:ROUTE_PROCESSOR_3_2) |
| 21 | 0xba100000625a3754423978a60c9317c58a424e3d (BAL) | 0x5550d13389bb70f45fcef58f19f6b6e87f6e747d (sushiswap:ROUTE_PROCESSOR_3_2) |
| 22 | 0x5a98fcbea516cf06857215779fd812ca3bef1b32 (LDO) | 0x5550d13389bb70f45fcef58f19f6b6e87f6e747d (sushiswap:ROUTE_PROCESSOR_3_2) |
| 23 | 0xd533a949740bb3306d119cc777fa900ba034cd52 (CRV) | 0x5550d13389bb70f45fcef58f19f6b6e87f6e747d (sushiswap:ROUTE_PROCESSOR_3_2) |
| 24 | 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2 (WETH) | 0x5550d13389bb70f45fcef58f19f6b6e87f6e747d (sushiswap:ROUTE_PROCESSOR_3_2) |
| 25 | 0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48 (USDC) | 0x5550d13389bb70f45fcef58f19f6b6e87f6e747d (sushiswap:ROUTE_PROCESSOR_3_2) |
| 26 | 0x6b175474e89094c44da98b954eedeac495271d0f (DAI) | 0x5550d13389bb70f45fcef58f19f6b6e87f6e747d (sushiswap:ROUTE_PROCESSOR_3_2) |
| 27 | 0xdac17f958d2ee523a2206206994597c13d831ec7 (USDT) | 0x5550d13389bb70f45fcef58f19f6b6e87f6e747d (sushiswap:ROUTE_PROCESSOR_3_2) |

### Revokes

| id | token | spender |
|-----|-------|---------|
| 12 | 0xc00e94cb662c3520282e6f5717214004a7f26888 (COMP) | 0x827179dd56d07a7eea32e3873493835da2866976 (sushiswap:ROUTE_PROCESSOR_3) |
| 13 | 0xba100000625a3754423978a60c9317c58a424e3d (BAL) | 0x827179dd56d07a7eea32e3873493835da2866976 (sushiswap:ROUTE_PROCESSOR_3) |
| 14 | 0x5a98fcbea516cf06857215779fd812ca3bef1b32 (LDO) | 0x827179dd56d07a7eea32e3873493835da2866976 (sushiswap:ROUTE_PROCESSOR_3) |
| 15 | 0xd533a949740bb3306d119cc777fa900ba034cd52 (CRV) | 0x827179dd56d07a7eea32e3873493835da2866976 (sushiswap:ROUTE_PROCESSOR_3) |
| 16 | 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2 (WETH) | 0x827179dd56d07a7eea32e3873493835da2866976 (sushiswap:ROUTE_PROCESSOR_3) |
| 17 | 0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48 (USDC) | 0x827179dd56d07a7eea32e3873493835da2866976 (sushiswap:ROUTE_PROCESSOR_3) |
| 18 | 0x6b175474e89094c44da98b954eedeac495271d0f (DAI) | 0x827179dd56d07a7eea32e3873493835da2866976 (sushiswap:ROUTE_PROCESSOR_3) |
| 19 | 0xdac17f958d2ee523a2206206994597c13d831ec7 (USDT) | 0x827179dd56d07a7eea32e3873493835da2866976 (sushiswap:ROUTE_PROCESSOR_3) |

## Scope Changes

Besides the (more readable) approvals, this payload makes changes to the `Roles` modifier contract, which is currently enabled on the managed safe. Permissions of this type can be seen as well through the events emitted, each having its particular structure.

This changes are detailed in the next sections, grouped by the action they perform.

### scopeTarget

To interact with contracts they have to be scoped first (the contract address). `scopeTarget` function scopes calls to an address, limited to specific function signatures, and per function scoping rules.

`ScopeTarget` events have the following structure:

```
event ScopeTarget(
    uint16 role,
    address targetAddress
)
```

- `role` here is the `roleId` used to identify the role being modified. Current configuration has `roleId = 1`
- `targetAddress` here is the scoped address on which a function signature should be allowed

In all cases, `scopeTarget` is called in the `Roles` contract with `role = 1`.

| id_ | target |
|-----|--------|
| 34 | 0xa17581a9e3356d9a858b789d68b4d866e593ae94 (compound_v3:cWETHv3) |
| 36 | 0xa397a8c2086c554b531c02e29f3291c9704b00c7 (compound_v3:MainnetBulker) |
| 39 | 0xd322a49006fc828f9b5b37ab215f99b4e5cab19c (aave_v3:WRAPPED_TOKEN_GATEWAY_V3) |
| 42 | 0xf047f23acfdb1315cf63ad8ab5146d5fda4267af (ankr:SWAP_POOL) |
| 44 | 0x84db6ee82b7cf3b47e8f19270abde5718b936670 (ankr:ETH2_STAKING) |
| 47 | 0xcf5ea1b38380f6af39068375516daf40ed70d299 (stader:STAKE_POOLS_MANAGER) |
| 49 | 0x9f0491b32dbce587c50c4c43ab303b06478193a7 (stader:USER_WITHDRAWAL_MANAGER) |
| 52 | 0xbd7d6a9ad7865463de44b05f04559f65e3b11704 (spark:WRAPPED_TOKEN_GATEWAY_V3) |
| 55 | 0xc13e21b648a5ee794902342038ff3adab66be987 (spark:LENDING_POOL_V3) |
| 58 | 0x5550d13389bb70f45fcef58f19f6b6e87f6e747d (sushiswap:ROUTE_PROCESSOR_3_2) |
| 62 | 0xa96a65c051bf88b4095ee1f2451c2a9d43f53ae2 (curve:ankrETH_POOL) |
| 64 | 0x13f4ea83d0bd40e75c8222255bc855a974568dd4 (pancake_swap:SMART_ROUTER) |
| 68 | 0x1b0e765f6224c21223aea2af16c1c46e38885a40 (compound_v3:CometRewards) |
| 71 | 0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2 (aave_v3:POOL_V3) |
| 76 | 0xb188b1cb84fb0ba13cb9ee1292769f903a9fec59 (aura:REWARD_POOL_DEPOSIT_WRAPPER) |
| 81 | 0x2a14db8d09db0542f6a371c0cb308a768227d67d (aura:auraB_wstETH_STABLE_REWARDER) |
| 83 | 0xba12222222228d8ba445958a75a0704d566bf2c8 (balancer:VAULT) |
| 88 | 0x68b3465833fb72a70ecdf485e0e4c7bd8665fc45 (uniswapv3:ROUTER_2) |

### RevokeTarget

If no interactions are further needed with certain contracts they can be revoked, meaning the role no longer has permission interact with it. `revokeTarget` function disallows all calls made to an address.

`RevokeTarget` events have the following structure:

```
event RevokeTarget(
		uint16 role,
		address targetAddress
)
```

- `role` here is the roleId used to identify the role being modified
- `targetAddress` here is the address to be disallowed

In all cases, `revokeTarget` is called in the `Roles` contract with `role = 1`.

| id_ | target |
|-----|--------|
| 28 | 0x0052688295413b32626d226a205b95cdb337de86 (balancer:bb_aV3_USD_GAUGE) |
| 29 | 0x59d66c58e83a26d6a0e35114323f65c3945c89c1 (aura:auraB_stETH_STABLE_REWARDER) |
| 31 | 0xcd4722b7c24c29e0413bdcd9e51404b4539d14ae (balancer:B_stETH_STABLE_GAUGE) |
| 32 | 0xd48451a61d5190a1ba7c9d17056490cb5d50999d (aura:aurabb_aV3_USD_REWARDER) |

### scopeAllowFunction

In order to call functions in scoped targets (contracts), functions have to be scoped. `scopeAllowFunction` function allows a specific function signature on a scoped target (enables to call function from already scoped contract address in `scopeTarget` without any constraint). 

`ScopeAllowFunction` events have the following structure:

```
event ScopeAllowFunction(
    uint16 role,
    address targetAddress,
    bytes4 selector,
    ExecutionOptions options,
    uint256 resultingScopeConfig
)
```

- `role` here is the `roleId` used to identify the role being modified
- `targetAddress` here is the scoped address on which a function signature should be allowed
- `selector` here is the function signature being scoped
- `options` here is the index of the `ExecutionOptions` enum, it can give permission to send ether, use delegate_call or both

```
enum ExecutionOptions {
    None,
    Send,
    DelegateCall,
    Both
}
```

In all cases, `scopeAllowFunction` is called in the `Roles` contract with `role = 1`.

| id_ | targetAddress | selector | options |
|-----|---------------|----------|---------|
| 45  | 0x84db6ee82b7cf3b47e8f19270abde5718b936670 (ankr:ETH2_STAKING) | 0x9fa65c56 (stakeAndClaimAethC()) | 1 (Send) |
| 46  | 0x84db6ee82b7cf3b47e8f19270abde5718b936670 (ankr:ETH2_STAKING) | 0xc957619d (unstakeAETH(uint256 shares)) | 0 (None) |
| 51  | 0x9f0491b32dbce587c50c4c43ab303b06478193a7 (stader:USER_WITHDRAWAL_MANAGER) | 0x379607f5 (claim(uint256 _requestId)) | 0 (None) |
| 63  | 0xa96a65c051bf88b4095ee1f2451c2a9d43f53ae2 (curve:ankrETH_POOL) | 0x3df02124 (exchange(int128 i, int128 j, uint256 dx, uint256 min_dy)) | 1 (Send) |

### scopeFunction

Works the same way as scopeAllowFunction, but allows for constraining of call paramters only to single values. `scopeFunction` function sets scoping rules for a function, on a scoped address.

`ScopeFunction` events have the following structure:

```
event ScopeFunction(
    uint16 role,
    address targetAddress,
    bytes4 functionSig,
    bool[] isParamScoped,
    ParameterType[] paramType,
    Comparison[] paramComp,
    bytes[] compValue,
    ExecutionOptions options,
    uint256 resultingScopeConfig
)
```

- `role` here is the `roleId` used to identify the role being modified
- `targetAddress` here is the scoped address on which a function signature should be allowed
- `functionSig` here is the function signature being scoped
- `isParamScoped` is a bool array with value 0 for non-scoped (non-constrained) and 1 for scoped parameters (constrained)
- `paramType` here is the index of the `ParameterType` enum, it determines the type of parameter being passed for constraining the interaction
- `paramComp`
- `compValue` values the parameter can take
- `options` here is the index of the `ExecutionOptions` enum, it can give permission to send ether, use delegate_call or both

```
enum ParameterType {
    Static,
    Dynamic,
    Dynamic32
}
```

In all cases, `scopeFunction` is called in the Roles contract with `role = 1`.

| id | targetAddress | functionSig | isParamScoped | compValue | options |
|-----|---------------|-------------|---------------|-----------|---------|
| 35 | 0xa17581a9e3356d9a858b789d68b4d866e593ae94 (compound_v3:cWETHv3) | 0x110496e5 (allow(address,bool)) | [True] | compound_v3:MainnetBulker | 0 (None) |
| 37 | 0xa397a8c2086c554b531c02e29f3291c9704b00c7 (compound_v3:MainnetBulker) | 0x555029a6 (invoke(bytes32[] actions, bytes[] data)) | [True, True, True, False, True, True, True, True, True] | 64, 128, 1, ANY, 1, 32, 96, compound_v3:cWETHv3, ENS_Avatar_Safe | 1 (Send) |
| 40 | 0xd322a49006fc828f9b5b37ab215f99b4e5cab19c (aave_v3:WRAPPED_TOKEN_GATEWAY_V3) | 0x474cf53d (depositETH(address, address, uint16)) | [True, True] | aave_v3:POOL_V3, ENS_Avatar_Safe | 1 (Send) |
| 41 | 0xd322a49006fc828f9b5b37ab215f99b4e5cab19c (aave_v3:WRAPPED_TOKEN_GATEWAY_V3) | 0x80500d20 (withdrawETH(address, uint256, address)) | [True, False, True] | aave_v3:POOL_V3, ANY, ENS_Avatar_Safe | 0 (None) |
| 43 | 0xf047f23acfdb1315cf63ad8ab5146d5fda4267af (ankr:SWAP_POOL) | 0xe28079be (swapEth(uint256, address)) | [False, True] | ANY, ENS_Avatar_Safe | 0 (None) |
| 48 | 0xcf5ea1b38380f6af39068375516daf40ed70d299 (stader:STAKE_POOLS_MANAGER) | 0xf340fa01 (deposit(address)) | [True] | ENS_Avatar_Safe | 1 (Send) |
| 50 | 0x9f0491b32dbce587c50c4c43ab303b06478193a7 (stader:USER_WITHDRAWAL_MANAGER) | 0xccc143b8 (requestWithdraw(uint256, address)) | [False, True] | ANY, ENS_Avatar_Safe | 0 (None) |
| 53 | 0xbd7d6a9ad7865463de44b05f04559f65e3b11704 (spark:WRAPPED_TOKEN_GATEWAY_V3) | 0x474cf53d (depositETH(address, address, uint16)) | [True, True] | spark:LENDING_POOL_V3, ENS_Avatar_Safe | 1 (Send) |
| 54 | 0xbd7d6a9ad7865463de44b05f04559f65e3b11704 (spark:WRAPPED_TOKEN_GATEWAY_V3) | 0x80500d20 (withdrawETH(address, uint256, address)) | [True, False, True] | spark:LENDING_POOL_V3, ANY, ENS_Avatar_Safe | 0 (None) |
| 56 | 0xc13e21b648a5ee794902342038ff3adab66be987 (spark:LENDING_POOL_V3) | 0x617ba037 (supply(address, uint256, address, unit16)) | [True, False, True] | WETH, ANY, ENS_Avatar_Safe | 0 (None) |
| 57 | 0xc13e21b648a5ee794902342038ff3adab66be987 (spark:LENDING_POOL_V3) | 0x69328dec (withdraw(address, uint256, address)) | [True, False, True] | WETH, ANY, ENS_Avatar_Safe | 0 (None) |
| 59 | 0x5550d13389bb70f45fcef58f19f6b6e87f6e747d (sushiswap:ROUTE_PROCESSOR_3_2) | 0x2646478b (processRoute(address, uint256, address, uint256, address, bytes)) | [False, False, False, False, True] | ANY, ANY, ANY, ANY, ENS_Avatar_Safe | 0 (None) |
| 65 | 0x13f4ea83d0bd40e75c8222255bc855a974568dd4 (pancake_swap:SMART_ROUTER) | 0x04e45aaf (exactInputSingle((address, address, uint24, address, uint256, uint256, uint160))) | [False, False, False, True] | ANY, ANY, ANY, ENS_Avatar_Safe | 0 (None) |
| 69 | 0x1b0e765f6224c21223aea2af16c1c46e38885a40 (compound_v3:CometRewards) | 0xb7034f7e (claim(address, address, bool)) | [False, True] | ANY, ENS_Avatar_Safe | 0 (None) |
| 72 | 0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2 (aave_v3:POOL_V3) | 0x617ba037 (supply(address, uint256, address, unit16)) | [False, False, True] | ANY, ANY, ENS_Avatar_Safe | 0 (None) |
| 74 | 0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2 (aave_v3:POOL_V3) | 0x69328dec (withdraw(address, uint256, address)) | [False, False, True] | ANY, ANY, ENS_Avatar_Safe) | 0 (None) |
| 77 | 0xb188b1cb84fb0ba13cb9ee1292769f903a9fec59 (aura:REWARD_POOL_DEPOSIT_WRAPPER) | 0x9eba6619 (depositSingle(address _rewardPoolAddress, address _inputToken, uint256 _inputAmount, bytes32 _balancerPoolId, (address[] assets, uint256[] maxAmountsIn, bytes userData, bool fromInternalBalance))) | [] | 0 | 0 (None) |
| 82 | 0x2a14db8d09db0542f6a371c0cb308a768227d67d (aura:auraB_wstETH_STABLE_REWARDER) | 0x7050ccd9 (getReward(address _account, bool _claimExtras)) | [True] | ENS_Avatar_Safe | 0 (None) |
| 84 | 0xba12222222228d8ba445958a75a0704d566bf2c8 (balancer:VAULT) | 0x52bbbe29 (swap((bytes32 poolId, uint8 kind, address assetIn, address assetOut, uint256 amount, bytes userData),(address sender, bool fromInternalBalance, address recipient, bool toInternalBalance), uint256 limit, uint256 deadline)) | [True, True, False, True, False, False, False, False, False, False, False, False, True, True] | 224, ENS_Avatar_Safe, ANY, ENS_Avatar_Safe, ANY, ANY, ANY, ANY, ANY, ANY, ANY, ANY, 192, ZERO_ADDRESS | 0 (None) |
| 89 | 0x68b3465833fb72a70ecdf485e0e4c7bd8665fc45 (uniswapv3:ROUTER_2) | 0x04e45aaf (exactInputSingle((address tokenIn, address tokenOut, uint24 fee, address recipient, uint256 amountIn, uint256 amountOutMinimum, uint160 sqrtPriceLimitX96))) | [False, False, False, True] | ANY, ANY, ANY, ENS_Avatar_Safe | 0 (None) |


#### Notes

- You won't find the `0x110496e5 (allow(address,bool))` in the `cWETHv3` contract. There is an extension of the `cWETHv3` contract which contains the `allow` function needed to interact with the ETH Comet in Compound V3. More info can be found in the [Compound Docs](https://docs.compound.finance/).
- The `invoke` function in the `compound_v3:MainnetBulker` everytime you want to interact with the `cWETHv3` comet in Compound v3.

### scopeParameterAsOneOf

`scopeParameterAsOneOf` function sets and enforces scoping rules, for a single parameter of a scoped function, on a scoped target (constraining the argument to be an element belonging in a given set). Parameter will be scoped with comparison type OneOf.

Permissions of this type can be seen as well through the events emitted, which have the following structure:

```
event ScopeParameterAsOneOf(
    uint16 role,
    address targetAddress,
    bytes4 functionSig,
    uint256 index,
    ParameterType paramType,
    bytes[] compValues,
    uint256 resultingScopeConfig
)
```

- `role` here is the `roleId` used to identify the role being modified
- `targetAddress` here is the scoped address on which functionSig lives.
- `functionSig` here is the function signature being scoped
- `index` here is the parameter index in the function
- `paramType` here is the index of the `ParameterType` enum
- `compValues` array containing the values the parameter can take
- `options` here is the index of the `ExecutionOptions` enum, it can give permission to send ether, use delegate_call or both

In all cases, scopeFunction is called in the `Roles` contract with `role = 1`.

| id_ | targetAddress | functionSig | index | compValues |
|-----|---------------|-------------|-------|------------|
| 38 | 0xa397a8c2086c554b531c02e29f3291c9704b00c7 (compound_v3:MainnetBulker) | 0x555029a6 (invoke(bytes32[] actions, bytes[] data)) | 3 | 0x414354494f4e5f535550504c595f4e41544956455f544f4b454e000000000000, 0x414354494f4e5f57495448445241575f4e41544956455f544f4b454e00000000, |
| 60 | 0x5550d13389bb70f45fcef58f19f6b6e87f6e747d (sushiswap:ROUTE_PROCESSOR_3_2) | 0x2646478b (processRoute(address tokenIn, uint256 amountIn, address tokenOut,uint256 amountOutMin, address to, bytes route)) | 0 | COMP, BAL, LDO, CRV, WETH, USDC, USDT, DAI, |
| 61 | 0x5550d13389bb70f45fcef58f19f6b6e87f6e747d (sushiswap:ROUTE_PROCESSOR_3_2) | 0x2646478b (processRoute(address tokenIn, uint256 amountIn, address tokenOut,uint256 amountOutMin, address to, bytes route)) | 2 | WETH, USDC, USDT, DAI, |
| 66 | 0x13f4ea83d0bd40e75c8222255bc855a974568dd4 (pancake_swap:SMART_ROUTER) | 0x04e45aaf (exactInputSingle((address tokenIn, address tokenOut, uint24 fee, address recipient, uint256 amountIn, uint256 amountOutMinimum, uint160 sqrtPriceLimitX96))) | 0 | stader:ETHx, WETH, |
| 67 | 0x13f4ea83d0bd40e75c8222255bc855a974568dd4 (pancake_swap:SMART_ROUTER) | 0x04e45aaf (exactInputSingle((address tokenIn, address tokenOut, uint24 fee, address recipient, uint256 amountIn, uint256 amountOutMinimum, uint160 sqrtPriceLimitX96))) | 1 | stader:ETHx, WETH, |
| 70 | 0x1b0e765f6224c21223aea2af16c1c46e38885a40 (compound_v3:CometRewards) | 0xb7034f7e (claim(address comet, address src, bool shouldAccrue)) | 0 | compound_v3:cUSDCv3, compound_v3:cWETHv3, |
| 73 | 0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2 (aave_v3:POOL_V3) | 0x617ba037 (supply(address asset, uint256 amount, address onBehalfOf, unit16 referralCode)) | 0 | DAI, USDC, WETH, |
| 75 | 0x87870bca3f3fd6335c3f4ce8392d69350b4fa4e2 (aave_v3:POOL_V3) | 0x69328dec (withdraw(address asset, uint256 amount, address onBehalfOf)) | 0 | DAI, USDC, WETH, |
| 78 | 0xb188b1cb84fb0ba13cb9ee1292769f903a9fec59 (aura:REWARD_POOL_DEPOSIT_WRAPPER) | 0x9eba6619 (depositSingle(address _rewardPoolAddress, address _inputToken, uint256 _inputAmount, bytes32 _balancerPoolId, (address[] assets, uint256[] maxAmountsIn, bytes userData, bool fromInternalBalance))) | 0 | aura:auraB_wstETH_STABLE_REWARDER, aura:auraB_rETH_STABLE_REWARDER, |
| 79 | 0xb188b1cb84fb0ba13cb9ee1292769f903a9fec59 (aura:REWARD_POOL_DEPOSIT_WRAPPER) | 0x9eba6619 (depositSingle(address _rewardPoolAddress, address _inputToken, uint256 _inputAmount, bytes32 _balancerPoolId, (address[] assets, uint256[] maxAmountsIn, bytes userData, bool fromInternalBalance))) | 1 | wstETH, WETH, rETH, |
| 80 | 0xb188b1cb84fb0ba13cb9ee1292769f903a9fec59 (aura:REWARD_POOL_DEPOSIT_WRAPPER) | 0x9eba6619 (depositSingle(address _rewardPoolAddress, address _inputToken, uint256 _inputAmount, bytes32 _balancerPoolId, (address[] assets, uint256[] maxAmountsIn, bytes userData, bool fromInternalBalance))) | 3 | balancer:B_wstETH_STABLE, balancer:B_rETH_STABLE, |
| 85 | 0xba12222222228d8ba445958a75a0704d566bf2c8 (balancer:VAULT) | 0x52bbbe29 (swap((bytes32 poolId, uint8 kind, address assetIn, address assetOut, uint256 amount, bytes userData),(address sender, bool fromInternalBalance, address recipient, bool toInternalBalance), uint256 limit, uint256 deadline)) | 7 | balancer:B_50WETH_50AURA, balancer:B_80BAL_20WETH, balancer:B_60WETH_40DAI, balancer:B_50USDC_50WETH, balancer:B_50COMP_50WETH, balancer:B_stETH_STABLE, balancer:B_rETH_STABLE, balancer:B_ankrETH_wstETH_STABLE, balancer:B_ETHx_WETH_STABLE, |
| 86 | 0xba12222222228d8ba445958a75a0704d566bf2c8 (balancer:VAULT) | 0x52bbbe29 (swap((bytes32 poolId, uint8 kind, address assetIn, address assetOut, uint256 amount, bytes userData),(address sender, bool fromInternalBalance, address recipient, bool toInternalBalance), uint256 limit, uint256 deadline)) | 9 | AURA, BAL, WETH, COMP, wstETH, rETH, aETHc, stader:ETHx, |
| 87 | 0xba12222222228d8ba445958a75a0704d566bf2c8 (balancer:VAULT) | 0x52bbbe29 (swap((bytes32 poolId, uint8 kind, address assetIn, address assetOut, uint256 amount, bytes userData),(address sender, bool fromInternalBalance, address recipient, bool toInternalBalance), uint256 limit, uint256 deadline)) | 10 | WETH, DAI, USDC, wstETH, rETH, aETHc, stader:ETHx, |
| 90 | 0x68b3465833fb72a70ecdf485e0e4c7bd8665fc45 (uniswapv3:ROUTER_2) | 0x04e45aaf (exactInputSingle((address tokenIn, address tokenOut, uint24 fee, address recipient, uint256 amountIn, uint256 amountOutMinimum, uint160 sqrtPriceLimitX96))) | 0 | COMP, CRV, CVX, DAI, LDO, rETH, rETH2, sETH2, SWISE, USDC, USDT, WETH, |
| 91 | 0x68b3465833fb72a70ecdf485e0e4c7bd8665fc45 (uniswapv3:ROUTER_2) | 0x04e45aaf (exactInputSingle((address tokenIn, address tokenOut, uint24 fee, address recipient, uint256 amountIn, uint256 amountOutMinimum, uint160 sqrtPriceLimitX96))) | 1 | DAI, USDC, USDT, sETH2, WETH, |

### ScopeRevokeFunction

Similar to `revokeTarget`, if specific function calls are no longer needed they can be revoked, meaning the role no longer has permission to interact with it. `scopeRevokeFunction` function disallows a specific function signature on a scoped target (disables the whitelisting of scopedFunction or scopedAllowFunction).

`ScopeRevokeFunction` events have the following structure

```
event ScopeRevokeFunction(
        uint16 role,
        address targetAddress,
        bytes4 selector,
        uint256 resultingScopeConfig
    )
```

- `role` here is the `roleId` used to identify the role being modified
- `targetAddress` here is the scoped address on which a function signature should be disallowed.
- `selector` here is the function signature being unscoped/revoked

In all cases, `scopeRevokeFunction` is called in the Roles contract with `role = 1`.

| id_ | targetAddress | functionSig |
|-----|---------------|-------------|
| 30 | 0x827179dd56d07a7eea32e3873493835da2866976 (sushiswap:ROUTE_PROCESSOR_3) | 0x2646478b (processRoute) |
| 33 | 0xdeb83d81d4a9758a7baec5749da863c409ea6c6b (cowswap:ORDER_SIGNER) | 0x83afcefd (signOrder) |

# Findings & Conclusion

- `Approve`
    - Missing Sushiswap allowances mention in the post (we are changing the approvals for the router without mentioning it)
- `ScopeTarget`
    - compound_v3:MainnetBulker? It's needed for ETH interactions with Compound V3
    - Sushiswap Router 3_2 not mentioned in proposal
- `RevokeTarget`
    - Why for all? We are not mentioning them in the proposal?
        - 0x0052688295413b32626d226a205b95cdb337de86 balancer:bb_aV3_USD_GAUGE revoke
        - 0x59d66c58e83a26d6a0e35114323f65c3945c89c1 aura:auraB_stETH_STABLE_REWARDER revoke
        - 0xcd4722b7c24c29e0413bdcd9e51404b4539d14ae balancer:B_stETH_STABLE_GAUGE revoke
        - 0xd48451a61d5190a1ba7c9d17056490cb5d50999d aura:aurabb_aV3_USD_REWARDER
- `ScopeAllowFunction`
- `ScopeFunction`
    - id 35 - ✅ compound_v3:cWETHv3 allow???? signature wrong? Due to the extended ABI
    - id 37 - ✅ what are the parameters? 
    - id 59 - Sushiswap router - missing tokensIn and out constrain but recipient avatar
        - Later constrained in `scopeParameterAsOneOf`
    - id 65 - pancake swap router - missing tokensIn and out constrain but recipient avatar
        - Later constrained in `scopeParameterAsOneOf`
    - id 72 - aave v3 pool - missing assetIn constrain but only to avatar
        - Later constrained in `scopeParameterAsOneOf`
    - id 74 - aave v3 pool - missing assetOut constrain but only to avatar
        - Later constrained in `scopeParameterAsOneOf`
    - id 77 - aura pool deposit missing all constrains
        - Later constrained in `scopeParameterAsOneOf`
    - id 84 - balancer vault - missing all constraints but only to avatar
        - Later constrained in `scopeParameterAsOneOf`
    - id 89 - Uniswap router v3 - missing all constraints but only to avatar
        - Later constrained in `scopeParameterAsOneOf
    - The Balancer:Vault scoping should be exlpained better
- `ScopeParameterAsOneOf`
    - ID 38 ✅ - compound v3 mainnet bulker - scoping is hard to understand
    - ID 70 `?` - usdc shouldn't be included? (check if events show current state or sdk issue)
    - id 73 & 75 `?` - shouldnt DAI and USDC already be included? (check if events show current state or sdk issue)
    - id 78 & 79 & 80 - Aura deposit wrapper not mentioning it in the post
    - CompoundV3: MainnetBulker scoping should be explained better
- `ScopeRevokeFunction`
    - internal - why unscope function calls and not the target?

# References

Methodology was derived from [Due Dilligence: BIP-442 Karpatkey Payload](https://forum.balancer.fi/t/bip-442-permissions-preset-update-request-2/5209/3#due-dilligence-bip-442-karpatkey-payload-1) post by [@gosuto](https://forum.balancer.fi/u/gosuto). This served as a great starting point and model for this post.

https://github.com/gnosis/zodiac-modifier-roles-v1