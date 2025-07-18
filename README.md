# AIMOVE NFT 项目说明

本项目包含后端、前端以及在 Aptos 区块链上部署的 NFT 智能合约。本文档将指导您完成项目设置、依赖安装、合约编译与发布等步骤。

---

## 项目描述

AIMOVE 是一个利用人工智能驱动的学习平台，旨在帮助开发者高效掌握 Aptos 区块链上的 Move 编程语言，并通过 NFT 技术激励学习过程。项目通过 AI 提供个性化学习路径、智能代码分析和实时反馈，解决传统区块链开发学习曲线陡峭的问题。用户可以在平台上学习 Move 语言、开发 NFT 智能合约，并在 Aptos 测试网上部署和测试代码。

### 主要功能包括

- **AI 驱动学习**：动态生成定制化学习内容和练习。
- **NFT 激励机制**：通过完成学习任务获得独一无二的 NFT 奖励，增强学习动力。
- **交互式开发环境**：提供 Aptos 区块链沙盒，支持实时合约部署和调试。
- **智能代码分析**：AI 实时检查代码，提供错误提示和优化建议。

---


## Aptos 区块链集成

AIMOVE 深度整合了 Aptos 区块链的以下特性：
- **Move 语言**：使用 Move 语言开发 NFT 智能合约，利用其资源导向编程和安全性特性，确保合约逻辑的可靠性和资产安全。
- **Aptos 测试网**：通过 Aptos CLI 与测试网交互，支持用户在真实区块链环境中编译、发布和测试 NFT 合约。
- **NFT 功能**：实现基于 Move 的 NFT 铸造、转移和查询功能，用户可通过学习任务获得 NFT 奖励，存储在 Aptos 链上。
- **Aptos 节点 API**：通过 `rest_url`（如 `https://fullnode.testnet.aptoslabs.com`）与 Aptos 节点交互，获取链上数据和交易状态。

---

## 项目结构

- **后端 (Backend)**：使用 Node.js 和 Prisma 构建，提供后端 API 服务。
- **前端 (Frontend)**：使用现代前端框架，提供用户交互界面。
- **智能合约 (NFT on Aptos)**：使用 Move 语言在 Aptos 区块链上实现 NFT 功能。

---

## 后端 (Backend)

1. **复制环境变量**
   ```bash
   cp .env.example .env
   ```
   > 注意: 请手动编辑 `.env` 文件，填写所需的环境变量。

2. **下载依赖**
   ```bash
   pnpm install
   ```

3. **生成 Prisma 客户端**
   ```bash
   pnpm prisma generate
   ```

4. **启动项目**
   ```bash
   pnpm start:dev
   ```

---

## 前端 (Frontend)

1. **复制环境变量**
   ```bash
   cp .env.example .env
   ```
   > 注意: 请手动编辑 `.env` 文件，填写所需的环境变量。

2. **下载依赖**
   ```bash
   pnpm install
   ```

3. **启动项目**
   ```bash
   pnpm dev
   ```

---

## NFT Aptos 上链 - 智能合约

1. **Aptos CLI 初始化**
   ```bash
   aptos init
   ```
   - 选择网络：testnet
   - 私钥输入：可留空以自动生成
   - 账户信息将保存在 `.aptos/config.yaml`

   > ⚠️ 注意: 私钥务必妥善保管，泄露可能导致资产丢失！

2. **领取测试币**
   - 访问 CLI 输出的 faucet 链接领取测试币，例如：  
     `https://aptos.dev/network/faucet?address=你的账户地址`
   - 查询余额：
     ```bash
     aptos account balance
     ```
     > 1 APT = 100,000,000 Octa

3. **.aptos/config.yaml 说明**

   配置文件示例：

   ```yaml
   profiles:
     default:
       network: Testnet
       private_key: ed25519-priv-0x...
       public_key: ed25519-pub-0x...
       account: 你的账户地址
       rest_url: "https://fullnode.testnet.aptoslabs.com"
   ```

   - `private_key`：账户私钥，务必保密
   - `public_key`：账户公钥，可公开
   - `account`：Aptos 账户地址
   - `rest_url`：Aptos 节点 API 地址

4. **Move 合约编译**
   ```bash
   aptos move compile
   ```
   - 首次编译会自动拉取依赖
   - 如有未使用变量警告，可忽略或按提示优化

5. **Move 合约发布**
   ```bash
   aptos move publish --assume-yes
   ```
   - 发布成功后会输出交易哈希，可在区块链浏览器查询

   示例输出：

   ```json
   {
     "Result": {
       "transaction_hash": "0x...",
       "gas_used": 4668,
       "gas_unit_price": 100,
       "sender": "你的账户地址",
       "sequence_number": 0,
       "success": true,
       "timestamp_us": 1752651565396134,
       "version": 6809603678,
       "vm_status": "Executed successfully"
     }
   }
   ```

---

## Aptos 官方文档

如有其他问题，请参考官方文档或联系项目维护者。

---

## 项目亮点 / 创新点

- **AI 驱动的学习体验**：通过 xAI 的 Grok 3，AIMOVE 提供个性化的 Move 学习路径，结合智能代码分析，显著降低区块链开发的入门门槛。
- **NFT 激励机制**：用户通过完成学习任务获得 Aptos 链上的 NFT 奖励，增强学习动力，同时展示区块链技术的实际应用。
- **无缝区块链集成**：结合 Aptos 区块链的 Move 语言和测试网，提供真实的开发和部署体验，适合初学者和高级开发者。
- **模块化架构**：前端、后端和智能合约分离设计，便于维护和扩展，支持多种学习场景。