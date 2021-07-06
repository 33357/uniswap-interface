# 部署uniswapv2合约与前端
所需项目：https://github.com/WhiteMatrixTech/UniswapV2Clone
https://github.com/WhiteMatrixTech/Uniswap-interface-v2-clone

## 部署合约

```bash
# 克隆项目
git clone https://github.com/WhiteMatrixTech/UniswapV2Clone
```

```bash
# 安装依赖
yarn
```

```bash
# 查看账户
yarn run env-cmd -f envs/.env.rinkeby yarn hardhat accounts --network rinkeby
```

```bash
# 编译合约
yarn run env-cmd -f envs/.env.rinkeby yarn run hardhat compile
```

### 修改init_code_hash
`/contracts/libraries/UniswapV2Library.sol 31:29` 的`2c272808f669dbb141e4759d110f215f9bd446cabd2be19f80565277bfd2139c`为`/artiffacts/contratcs/UniswapV2Pair.sol/UniswapV2Pair.json`中`bytecode`字段的[Keccak-256](http://emn178.github.io/online-tools/keccak_256.html)值，记为`init_code_hash`。

```bash
# 部署合约
yarn run env-cmd -f envs/.env.rinkeby yarn run hardhat deploy --network rinkeby
```

```bash
# 验证合约
yarn run env-cmd -f envs/.env.rinkeby yarn hardhat --network rinkeby etherscan-verify --api-key <api-key>
```

## 部署前端

```bash
# 克隆项目
git clone https://github.com/WhiteMatrixTech/Uniswap-interface-v2-clone
```

```bash
# 安装依赖
yarn
```

### 替换合约

全文检索并替换：
router_address：`0xD8601953361A518596904C5968e40E78Ce7B1Ed9`
factory_address：`0x96f8005E358A2B8e4f7b3d74dF5FE6751887c9ED`
weth_address：`0x6b9c1644C6Ee1d6594E759dc2053DD091CB56b05`
init_code_hash: `0x2c272808f669dbb141e4759d110f215f9bd446cabd2be19f80565277bfd2139c`

```bash
# 启动
yarn start
```