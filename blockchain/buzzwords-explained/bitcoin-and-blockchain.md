# Bitcoin & Blockchain

<span style='color: gray'>比特币与区块链</span>

## Bitcoin

<span style='color: gray'>比特币</span>

两种含义：一种 [blockchain](#blockchain) 技术；一种可以交易的 [token](#token)。

### Satoshi Nakamoto

<span style='color: gray'>中本聪</span>

[bitcoin](#bitcoin) 创造者对自己的称呼。

很多人自称是 [bitcoin](#bitcoin) 创造者，但都拿不出证据。如果有个人能够使用中本聪在 [genesis block](#genesis_block) 中的 [address](#address) `1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa` 进行一次 [transaction](#transaction)，并在此之前向大众公布该 transaction 的细节，那么就说明 TA 拥有这个 [wallet](#wallet) 的 [private key](#private-key) ，就能够证明 TA 是中本聪（或者是偷了中本聪的 wallet 的人）。

### Blockchain

<span style='color: gray'>区块链</span>

一种数据库，数据库中的数据对所有人可见，数据的量只增加不减少，历史数据无法被修改（除非遭受 [51% attack](#51-attack)）。

### Block

<span style='color: gray'>区块</span>

[blockchain](#blockchain) 存储数据的基本单位。

以 [bitcoin](#bitcoin) 为例，平均每 10 分钟由全体 [miner](#miner) 算出一个 block，每个 block 中存储了：

- 前一个 block 是哪个
- 被哪个 [miner](#miner) 算出
- 被算出来的时间点
- 产出了多少新的币
- 0 至若干个 [transaction](#transaction)
- [gas](#gas)
- [coinbase](#coinbase)

等等信息，因为 block 的“前一个 Block 是哪个”信息，所以从最新的 block 可以追溯到第一个 block，连成一个链条，所以叫做 [blockchain](#blockchain)。第一个 block 没有前一个 block，被称为 [genesis block](#genesis_block)。

#### Genesis block

<span style='color: gray'>创世区块</span>

每个 [blockchain](#blockchain) 的第一个 [block](#block)。

#### Coinbase

<span style='color: gray'>区块基础信息</span>

[miner](#miner) 在 [block](#block) 里留的一段话，有长度限制。

著名交易所 Coinbase 的名字应该就是从这里来的（没有考证）。

[Satoshi Nakamoto](#satoshi-nakamoto) 在 [genesis block](#genesis_block) 里留的话是：

> EThe Times 03/Jan/2009 Chancellor on brink of second bailout for banks

在各种 [explorer](#explorer) 中可以看到，比如 [blockchair🔗](https://blockchair.com/bitcoin/block/0)。

#### Explorer

<span style='color: gray'>区块浏览器</span>

用于浏览 [blockchain](#blockchain) 中的数据的 App，一般是网页。

基本上每个 [blockchain](#blockchain) 都有一个或多个官方或第三方提供的浏览器。

#### Gas

<span style='color: gray'>手续费</span>

[transaction](#transaction) 的发起者给 [miner](#maner) 的小费。

miner 很闲的时候，可以少给或不给小费。

### Fork

<span style='color: gray'>分叉</span>

### Transaction

<span style='color: gray'>交易/转账</span>

#### Pending transaction

<span style='color: gray'>待确认交易</span>

由于 [transaction](#transaction) 发起者没给或少给 [gas](#gas) ，或者 [miner](#miner) 忙不过来导致的，还没有被 [mining](#mining) 的 [transaction](#transaction)。

### Token

<span style='color: gray'>代币、通证（可流通的数字权益证明）、密令（去中心化共识的加密数字令牌）</span>

可以理解为钱。

### Wallet

<span style='color: gray'>钱包</span>

进行 [transaction](#transaction) 所必须的东西，分为 [address](#address) 和 [private key](#private-key) 两部分。

#### Address

<span style='color: gray'>钱包地址/公钥</span>

[wallet](#wallet) 公开的部分，相当于银行卡账号。

不同的是所有人都可以看到你卡里有多少 [token](#token)，以及历史 [transaction](#transaction)（一些拥有匿名交易功能的区块链除外）。

#### Private key

<span style='color: gray'>私钥</span>

[wallet](#wallet) 私密的部分，相当于银行卡密码。

##### Mnemonic Phrase

<span style='color: gray'>助记词</span>

使用 12 个单词来描述 [private key](#private-key)，更方便记忆，和 [private key](#private-key) 有同等作用，是一一对应的关系。

##### Hardware Wallet

<span style='color: gray'>硬件钱包</span>

可以理解为网银盾。

### Layer2

<span style='color: gray'>二层网络/闪电网络</span>

### Mining

<span style='color: gray'>挖矿</span>

[miner](#miner) 把 [transaction](#transaction) 打包放进 [block](#block) 中，并完成算法难题的过程。

#### POW

<span style='color: gray'>Proof of work，工作量证明</span>

#### Miner

<span style='color: gray'>矿工</span>

#### Mining pool

<span style='color: gray'>矿池</span>

### Mining revenue

<span style='color: gray'>挖矿收益</span>

#### 51% attack
