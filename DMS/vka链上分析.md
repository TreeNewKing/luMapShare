# 信息收集

[vka代币地址](https://arbiscan.io/address/0xAFccb724e3aec1657fC9514E3e53A0E71e80622D)

```
0xAFccb724e3aec1657fC9514E3e53A0E71e80622D
```

[esvka地址](https://arbiscan.io/address/0x95b3f9797077ddca971ab8524b439553a220eb2a)

```
0x95b3f9797077ddca971ab8524b439553a220eb2a
```

[质押vka时交互的地址](https://arbiscan.io/address/0x5adace6475526539c7930921cefd9bb57cc7afa4#readProxyContract)

```
0x5adace6475526539c7930921cefd9bb57cc7afa4
```

[VKA锁定地址](https://arbiscan.io/address/0xA6f217d92A1F23C0454792cb7Bf81c74C8416550#code)

```
0xA6f217d92A1F23C0454792cb7Bf81c74C8416550 
```

[金库地址](https://arbiscan.io/address/0xb1bcd571a035b0165303b4b9ad8ffcee18faab40#readProxyContract)

```
0xB1BCd571A035b0165303B4b9ad8FfCEe18FaaB40
```

[dune数据](https://dune.com/treenewking/arbxiang-mu-shu-ju-he-ji)

## 交互合约

[ 从0x5ad交互合约中可以调用可读函数获得发放奖励的两位veChefs主厨](https://arbiscan.io/address/0x5adace6475526539c7930921cefd9bb57cc7afa4#readProxyContract)

 ##  主厨合约

```
veChefs[0] => 0x1A667E5c308aEf6d5E529559Ac93d19CAd19f3EA (esvkaHolderContract:230,817 esVKA)
 - startTime=>1715241523(2024-05-09 15:58:43)
 - endingTime->estimatedTime=>1728578861(2024-10-11 00:47:41)
 - rewardPerSecond=>38000000000000000(0.038esvka/s)
veChefs[1] => 0xB1BCd571A035b0165303B4b9ad8FfCEe18FaaB40 (usdcHolderContract:11,847usd)
 -rewardToken=>0xaf88d065e77c8cC2239327C5EDb3A432268e5831(USDC合约地址)
 - startTime=>1715246161(2024-05-09 17:16:01)
 - endingTime=>estimatedTime=>1723672571(2024-08-15 05:56:11)
 - rewardPerSecond=>0.011000(0.011000USDC/s)
```

第一个合约是发送esVKA的主厨，这个地址有230,817 个esVKA

第二个合约是发送Vka的主厨，这个地址有11,847usdc

> 注：这两个地址也是代理合约地址不是Implement合约地址

0x5ad代理合约的Implement合约地址为:

**[0x6db007b03b6c87b1a7d2b5bf98910681b315adf6](https://arbiscan.io/address/0x6db007b03b6c87b1a7d2b5bf98910681b315adf6#code)**

可以从这个地址获得交互合约的逻辑代码

在主厨的Transaction中可以找到加入池子的情况获得两个池合约地址（这两个地址也是RegistedTokens的）

esvkaChef

```
#	Name	     Type	     Data
0	_token	     address    0xA6f217d92A1F23C0454792cb7Bf81c74C8416550(vka锁定合约)
1	_allocPoint	 uint256	100

#	Name	     Type	     Data
0	_token	     address	 0xf25Bde89AD25493656f7cB7e53b001A6e662aF8F(vka质押信息查询合约)
1	_allocPoint	 uint256	 1
```

usdcChef

```
#	Name	      Type	        Data
0	_token	      address	    0xA6f217d92A1F23C0454792cb7Bf81c74C8416550
1	_allocPoint	  uint256 	    100

#	Name	      Type    	     Data
0	_token         address	     0xf25Bde89AD25493656f7cB7e53b001A6e662aF8F
1	_allocPoint	   uint256       1
```

##  PoolInfo

继续在主厨合约中通过中两个地址获得PoolInfo（调用poolInfo这个可读函数）

0xA6f的池信息

```
  totalSupply   uint256 :  9727142572131186423102258
  allocPoint   uint256 :  0
  lastRewardTime   uint256 :  1723381234
  accRewardPerShare   uint256 :  25387209970
```

 0xf25的池信息

```
  totalSupply   uint256 :  12737378218710726386035010
  allocPoint   uint256 :  100
  lastRewardTime   uint256 :  1723381234
  accRewardPerShare   uint256 :  28387217667
```

## UserInfo

此外还可以在主厨合约中查询到用户信息UserInfo（调用userInfo可读函数）

在[esVkaChef](https://arbiscan.io/address/0x1A667E5c308aEf6d5E529559Ac93d19CAd19f3EA#readProxyContract)中查询UserInfo

代币:0xA6f217d92A1F23C0454792cb7Bf81c74C8416550

userAddress:0x4368b63829f321d10b664d0ede39afe140ba8b1a

```
  amount          uint256 :  75388131236785267254060
  rewardDebt      uint256 :  1913894316954183367581 
  lastClaimTime   uint256 :  1723348788
```

代币:0xf25Bde89AD25493656f7cB7e53b001A6e662aF8F

userAddress:0x4368b63829f321d10b664d0ede39afe140ba8b1a

```
  amount          uint256 :  76405328059021966788840
  rewardDebt      uint256 :  2161538914089205805571
  lastClaimTime   uint256 :  1723348788
```

在UsdcChef中的逻辑统计在此省略

# 收益领取交互逻辑

## 用户交互合约

用法发起TransAction触发的函数

```
代理合约地址:0x5adace6475526539c7930921cefd9bb57cc7afa4(代理合约)
方法:ClaimWithCompound
参数:
#	Name	        Type	Data
0	isUsdcCompound	bool	false
1	isEsVKACompound	bool	false
```

[从实现合约中读取代码](https://vscode.blockscan.com/arbitrum-one/0x6db007b03b6c87b1a7d2b5bf98910681b315adf6)

ClaimWithCompound函数代码

```solidity
    //@note require user's USDC approval to be done before calling this function
    function claimWithCompound(bool isUsdcCompound, bool isEsVKACompound) external {
        address _user = msg.sender;
        uint256 usdcBalanceBefore = IERC20(USDC).balanceOf(_user);
        uint256 esVKABalanceBefore = IERC20(esVKA).balanceOf(_user);

        for (uint256 i; i < veChefs.length; ++i) {
//对将usdc奖励和esvka奖励进行提取
            IChefIncentivesController(veChefs[i]).claimAll(_user);
        }
//如果Usdc和esvka奖励都不选择复投调用multiClaim函数进行收集
        if (!isUsdcCompound && !isEsVKACompound) {
            multiClaim(_user);
        }
//计算用户从协议中领取到的USDC和esVka奖励
        uint256 usdcAmount = IERC20(USDC).balanceOf(_user) - usdcBalanceBefore;
        uint256 esVKAAmount = IERC20(esVKA).balanceOf(_user) - esVKABalanceBefore;
//如果用户选择了USDC复投且领取的奖励大于0，则将USDC奖励自动swap为VKA后进行质押
        if (isUsdcCompound && usdcAmount > 0) {
            IERC20(USDC).transferFrom(_user, address(this), usdcAmount);
            uint256 vkaAmount = _swap(_user, usdcAmount);
            uint128 targetExpiryDate = getUserTargetExpiry(_user, veToken);
            increaseLockPosition(uint128(vkaAmount), targetExpiryDate);
        }
//如果用户选择了esvka复投且领取的奖励大于0，则将esvka锁定
        if (isEsVKACompound && esVKAAmount > 0) {
            uint128 targetExpiryDate = getUserTargetExpiry(_user, esVKALocking);
            increaseEsLockPosition(uint128(esVKAAmount), targetExpiryDate);
        }
        //refresh balances after claiming and locking
        _refreshUserBalances(msg.sender);
    }
        function multiClaim(address _user) public {
        for (uint256 i; i < veChefs.length; ++i) {
            IChefIncentivesController(veChefs[i]).claimAll(_user);
            IChefIncentivesController(veChefs[i]).refreshUserBalance(_user);
        }
    }
```

在claimWithCompound函数中若usdc和esvka都不选择复投则调用代码块，调用对于主厨合约的claimAll函数进行收益领取

```solidity

  function multiClaim(address _user) public {
        for (uint256 i; i < veChefs.length; ++i) {
            IChefIncentivesController(veChefs[i]).claimAll(_user);
            IChefIncentivesController(veChefs[i]).refreshUserBalance(_user);
        }
    }
```

通过调用两位主厨的claimAll函数收取收益此时代码的上下文来到了主厨合约。

## esVkaChef代码

```solidity
ImplemntContractAddress 0xba18ebd2939002b94c77dc7a9fd6189a98216c1b
    function claimAll(address _user) external {
        claim(_user, registeredTokens);
    }
        /********************** Emission Calc + Transfer ***********************/
    /**
     * @notice Claim rewards.
     * @param _user address for claim
     * @param _tokens array of reward-bearing tokens
     */
    function claim(address _user, address[] memory _tokens) public nonReentrant whenNotPaused {
        _updateEmissions();
        uint256 currentTimestamp = block.timestamp;
        uint256 pending = userBaseClaimable[_user];
        userBaseClaimable[_user] = 0;
        uint256 _totalAllocPoint = totalAllocPoint;
        uint256 length = _tokens.length;
        for (uint256 i; i < length; ) {
            if (!vaildPODToken[_tokens[i]]) revert InvalidRToken();
            PoolInfo storage pool = poolInfo[_tokens[i]];
            if (pool.lastRewardTime == 0) revert UnknownPool();
            _updatePool(pool, _totalAllocPoint);
            UserInfo storage user = userInfo[_tokens[i]][_user];
            uint256 rewardDebt = (user.amount * pool.accRewardPerShare) / ACC_REWARD_PRECISION;
            pending = pending + rewardDebt - user.rewardDebt;
            user.rewardDebt = rewardDebt;
            user.lastClaimTime = currentTimestamp;
            //@note Confirm that ve / POD amount cannot be transfer before using
            // _handleTokenAfterClaim(_tokens[i], _user);
            unchecked {
                i++;
            }
        }
        _sendRewardToken(_user, pending);
    }
    
        /**
     * @dev Send RewardToken rewards to user.
     * @param _user address of recipient
     * @param _amount of RewardToken
     */
    function _sendRewardToken(address _user, uint256 _amount) internal {
        if (_amount == 0) {
            return;
        }

        address RewardTokenToken_ = rewardToken;
        uint256 chefReserve = IERC20(RewardTokenToken_).balanceOf(address(this));
        if (_amount > chefReserve) {
            revert OutOfRewards();
        } else {
            IERC20(RewardTokenToken_).safeTransfer(_user, _amount);
        }
    }
```

其中收益计算公式为

```solidity
          for (uint256 i; i < length; ) {
            if (!vaildPODToken[_tokens[i]]) revert InvalidRToken();
            PoolInfo storage pool = poolInfo[_tokens[i]];
            if (pool.lastRewardTime == 0) revert UnknownPool();
            _updatePool(pool, _totalAllocPoint);
            UserInfo storage user = userInfo[_tokens[i]][_user];
            /**
            * 收益计算公式
            **/
            uint256 rewardDebt = (user.amount * pool.accRewardPerShare) / ACC_REWARD_PRECISION;
            pending = pending + rewardDebt - user.rewardDebt;
            user.rewardDebt = rewardDebt;
            
            user.lastClaimTime = currentTimestamp;
            //@note Confirm that ve / POD amount cannot be transfer before using
            // _handleTokenAfterClaim(_tokens[i], _user);
            unchecked {
                i++;
            }
        }
```

