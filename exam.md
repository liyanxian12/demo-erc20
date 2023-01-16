# 区块链培训作业

请大家 fork 本仓库后答题，做完后提交自己的软件仓库链接。

## 第 1 题：Solidity 语言有哪些数据类型？

例如：

-   bool
-   int8

评分标准：每个数据类型计 1 分  
参考资料： https://docs.soliditylang.org/en/latest/types.html


答案：
1、布尔类型
bool：可接受 true 和 false 两个值，默认为 false。

2、整型
int 和 uint：分别表示有符号和无符号的整数，默认为0。支持关键字 int8 到 int256，以及 uint8 到 uint256，从8位到256位，以8位为步长递增，int 和 uint 分别是 int256 和 uint256 的别名。

3、地址类型
address：包含一个20字节的值（代表一个以太坊地址的大小）。一个地址可以用来获取余额，也可以通过转账的方式来转移余额。

4、字节类型
bytes1，bytes2，…，bytes32：字节用于存储固定大小的字符集，长度范围是1 ~ 32。字节的一个优点是它使用更少的Gas，所以当我们知道数据的长度时，最好使用它。

5、字符串类型
string：字符串用于存储等于或大于一个字节的字符集，字符串的长度是动态的。

6、枚举类型
enum：创建用户定义的数据类型，用于为一个整型常量分配一个名称，这使得合约具有可读性、可维护性和更不容易出错。枚举的选项可以用从0开始的无符号整数值表示。


## 第 2 题：列举并测试以太坊的 JSONRPC API。

评分标准：每条有效的（提供文本命令和测试截图） API 计 2 分，例如：

---

第 1 个 API： net_version

```shell
curl -s -X POST -H "Content-Type: application/json" https://matic-mumbai.chainstacklabs.com \
-d '{"id":1,"jsonrpc":"2.0","method":"net_version","params":[]}' | jq
```

![1673317288973](https://user-images.githubusercontent.com/7695325/211447294-e9e142c1-0fec-4588-9c8a-7ebfbd38a907.png)

---

答案：
1、curl -s -X POST -H "Content-Type: application/json" https://matic-mumbai.chainstacklabs.com -d '{"id":1,"jsonrpc":"2.0","method":"eth_blockNumber","params":[]}'
![image](https://user-images.githubusercontent.com/37762014/212617095-96195c0d-54b6-4d45-bcd2-ae6e3aca4275.png)

2、curl -s -X POST 'https://matic-mumbai.chainstacklabs.com' \--header 'Content-Type: application/json' \--data-raw '{"jsonrpc":"2.0","method":"web3_clientVersion","params":[],"id":67}'
![image](https://user-images.githubusercontent.com/37762014/212617200-1f966b7d-5ad3-43f0-84be-4104292b893e.png)

3、curl -s -X POST -H "Content-Type: application/json" https://matic-mumbai.chainstacklabs.com -d '{"jsonrpc":"2.0","method":"net_version","params":[],"id":67}'
![image](https://user-images.githubusercontent.com/37762014/212618175-73c414e5-ee21-4355-a3f2-958f617163ec.png)

4、curl -s -X POST -H "Content-Type: application/json" https://matic-mumbai.chainstacklabs.com -d '{"jsonrpc":"2.0","method":"eth_protocolVersion","params":[],"id":67}'
![image](https://user-images.githubusercontent.com/37762014/212618493-d42249b9-e1c2-4858-af6a-2c08b386840d.png)

5、curl -s -X POST -H "Content-Type: application/json" https://matic-mumbai.chainstacklabs.com -d '{"jsonrpc":"2.0","method":"eth_getTransactionCount","params":["0x407d73d8a49eeb85d32cf465507dd71d507100c1","latest"],"id":1}'
![image](https://user-images.githubusercontent.com/37762014/212618578-810dfb8b-9386-4e1c-9d17-436f12210c58.png)

6、curl -s -X POST -H "Content-Type: application/json" https://matic-mumbai.chainstacklabs.com -d '{"jsonrpc":"2.0","method":"eth_gasPrice","params":[],"id":73}'
![image](https://user-images.githubusercontent.com/37762014/212618656-c6e9e775-cb1a-4a52-b52f-80de7f3595a4.png)

7、curl -s -X POST -H "Content-Type: application/json" https://matic-mumbai.chainstacklabs.com -d '{"jsonrpc":"2.0","method":"eth_accounts","params":[],"id":1}'
![image](https://user-images.githubusercontent.com/37762014/212618969-d3f2080d-a4a8-4b9b-a910-9d8d25e04fa4.png)

8、curl -s -X POST -H "Content-Type: application/json" https://matic-mumbai.chainstacklabs.com -d '{"jsonrpc":"2.0","method":"net_listening","params":[],"id":67}'
![image](https://user-images.githubusercontent.com/37762014/212620246-41d9ed1e-0f98-46d3-8e4d-9efee606c41e.png)



## 第 3 题：同一个合约里代码相同的函数，为什么 GAS 费不同？

请用 Remix 验证在同一个合约里，名称不同、代码相同的函数的 GAS 费不相等，并解释原因。

评分标准：

-   验证成功： 10 分，对过程要截图
-   解释正确： 10 分


答案：
gas费是用于测量在以太坊区块链上执行特定操作所需的成本。gas其实类似于汽油，后者作为汽车的能量保证汽车可以正常行驶，以太坊网络上的gas为交易行为进行“加油”，并允许用户执行不同的操作。gas费相当于手续费，或者给矿工的辛苦费。处理链上数据的手续费，用来平衡整个网络交易速度。处理速度一定，当交易数据多了，那么谁出的价格高就优先处理谁的订单。gas费是必要的，是整个网络应承担的成本，因为网络上的每个节点都必须花费存储和计算资源，用来验证每条消息并保持网络的一致状态，这时候就需要消耗gas来补偿网络。 所以每个币的转账都有最低额度要求，这个最低额度要求往往也是目前需要的最少gas费额度。
gas费会上升和下降，原因有以下几个方面：
1.以太坊提升区块 gas limit。每一次以太坊将区块 gas limit 提升会让gas费下降；
2.以太坊链非常繁荣。gas 费用受区块链需求的影响，为了让自己的交易尽快打包，就需要更多的gas费，大量的交易在竞争，矿工优先处理 gas 价格最高的交易。因此，随着以太坊区块链上的活动增加，gas 的使用也会增加。gas费用上升，说明以太坊链上活动活跃，用户纷纷提高自己的gas费来完成交易。
3.以太坊链越来越拥堵。造成 Gas 费用上涨的根本原因，是以太坊网络利用率不断升高，处于严重的拥堵状态。以太坊网络利用率提高，因为用户活动太活跃，但同时也越来越拥堵。例如，以太坊上某个著名项目发售引发抢购潮就会让gas费瞬间飙涨。今年8月20日零时左右，以太坊GAS费瞬时飙升至2400Gwei以上，这是因为一款名为”0n1Force“的NFT项目发售引发抢购潮。



## 第 4 题：用 Remix 部署校验合约

用 Remix 写一个合约，部署到 mumbai 链上，计算 mumbai 链的最近平均出块时间，并校验合约代码代码。

评分标准：

-   代码正确：截图 10 分
-   部署成功：截图 10 分
-   代码校验：截图 5 分
-   获取结果：截图 5 分

## 第 5 题：黑名单 ERC20 合约

### 5.1 修复 BlacklistTokenFactory 合约里的 bug

命令 `yarn deploy:mumbai` 会在 mumbai 链上部署 BlacklistTokenFactory 和一个 BlacklistToken 合约（简称 BT1 ），地址保存在 deploy/deployed/mumbai.json 文件里（提示：删除该文件可以重新部署）。请在区块链浏览器上调用 BlacklistTokenFactory 合约里的 createBlacklistToken 函数，动态创建一个 BlacklistToken 合约（简称 BT2 ）， BT2 的地址保存在 BlacklistTokenFactory 的 blacklistTokens 数组里，也可以在交易里的 CreateBlacklistToken 事件里查看 BT2 的地址。因为目前 BlacklistTokenFactory 合约里有 bug，导致 `yarn test` 报告某些测试用例失败。请在区块链浏览器上比较 BT1 和 BT2 的功能，找出 BT2 功能异常的问题现象。并尝试修复合约 contracts/BlacklistTokenFactory.sol 的代码，能通过文件 test/BlacklistTokenFactory.test.js 里全部的自动化测试。

评分标准：

-   找到问题现象： 截图 10 分
-   解释问题原因： 10 分
-   修改合约代码： 20 分
-   自动化测试全部通过： 10 分

### 5.2 优化 BlacklistTokenFactory.test.js

参考： https://hardhat.org/tutorial/testing-contracts , 使用 loadFixture 重构 test/BlacklistTokenFactory.test.js 文件。

评分标准： 30 分

### 5.3 增强 BlacklistToken 合约的功能

修改本代码仓库里的 BlacklistToken 合约代码，在转账的时候抽取 10% 的手续费，并把被扣除的手续费转给合约的创建者。

评分标准：

-   代码正确： 30 分
-   部署成功： 10 分
-   代码校验： 10 分
-   手工测试： 10 分
-   
### 5.4 对 BlacklistToken 合约进行自动化测试

目前 BlacklistToken 还没有写测试用例，请在 test/BlacklistToken.test.js 文件里尽量补齐。可参考 https://hardhat.org/tutorial/testing-contracts 和网上其它开源项目的测试用例。

评分标准：每个有效的（能执行通过）测试用例 10 分，性质相同的用例不重复计分
