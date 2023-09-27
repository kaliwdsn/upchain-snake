# upchain-snake
## upchain-snake 项目结构
 > solana-token 基于solana的token

## upchain-snake 设计理念

 ### 原则
 > 涉及一款贪吃蛇2d游戏，接入solana区块链，使玩家在娱乐的同时获取收益，游戏采用链上+链下相结合的方式实现游戏整体逻辑

 ### 支持的客户端
 - h5网页版
 - 移动版（Android）
 - 移动版（iOS）

 ### 支持的链
 - EVM系列链（Ethereum、BSC等）
 - Solana区块链

 ### 账户设计（H5）
 - 用户通过授权签名来注册或登录游戏账户（用户账户）
 - 游戏系统不托管用户资产
 - 游戏内赚取的积分会写入合约中，由用户通过游戏内功能领取（调用合约领取）

 ### 游戏门票
 > 参与游戏需要付出门票

 - 门票来源：用户可通过游戏商城购买门票[NFT]
 - 门票定价：采用梯度定价的方式，用户需要使用代币来购买门票，代币类型为：EVM相关主网币或SOL
 - 门票使用：用户进入游戏场会自动扣除用户门票，门票不足将无法进入游戏场

 **实现细节：**
 - 用户授权钱包，调用合约，购买门票
 - 中心化服务通过事件接收购买详细信息，并记录到中心化数据库
 - 客户端将通过中心化数据库来获取用户门票数量

 **合约相关**
 用户购买门票支出的代币，将会按照1:10000的方式换算成食物，食物是一个类似于代币，食物用来在游戏场供玩家猎取

 ### 游戏逻辑
 玩家通过在游戏内吃地图上的食物，来获取积分（这里成为游戏积分A），其中地图上会有一些干扰，干扰项如下：
 - 部分食物是没有奖励的，即这部分食物是干扰项
 - 地图上会随机产生一些机器蛇，干扰用户在游戏内猎取食物
 - 机器蛇在游戏内死亡之后，会善生一串食物，这部分食物也是不携带积分的，即用户猎取这些食物不获取游戏积分A

 ### 游戏场
 游戏场分为限时模式、无尽模式和体验模式，详细说明如下：
 - 限时模式：游戏时间有限，场内食物积分更多（相对于无尽模式）
 - 无尽模式：没有时间限制

 ### 游戏结束
 游戏结束之后，玩家猎取的食物所携带的积分总额，会按照积分总额和游戏时间，以一定的策略换算成积分B，积分B可提现，可交易
