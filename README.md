# 🔵 MyRules - 自用分流规则

自用分流规则集：传统金融直连、加密资产分地区出口、AI/流媒体走美区，四条路线精细化分流。

## 路由总览

| # | 规则文件 | 策略出口 | 说明 |
|:--- |:--- |:--- |:--- |
| 1 | `oldmoney.list` | **DIRECT（直连）** | 传统金融：IBKR、iFAST、Wise、AlipayHK、Tenpay Global / Tenpay Go、SGB、Maya、Starryblu。银行支付类风控敏感，严禁走机房代理 |
| 2 | `crypto_hk.list` | **HK（自建香港分组）** | 预测市场：Polymarket、Predict.fun（币安钱包预测市场技术方）。台湾双重封锁打不开，香港技术可达（自行承担合规风险） |
| 3 | `crypto_tw.list` | **TW（自建台湾分组）** | 除预测市场外的全部加密资产：CEX（含 Bybit，平台自限香港 IP，必须走台湾）、钱包、DeFi、公链 RPC、行情工具、NFT、矿池 |
| 4 | `ai_us.list` | **DMIT-US（自建美国分组）** | AI 大模型精简版：OpenAI、Claude、Gemini、Grok、Mistral。流媒体底座已有专门分组，其余一律由 FINAL 兜底 |
| 5 | 懒人配置自带规则 | — | 国内网站直连等基础分流（底座配置自带） |
| 6 | FINAL | **DMIT-US** | 以上都没命中的其余流量，统一走美区 DMIT 出口 |

> 自建分组（DMIT-US / TW / HK）由 `sync.yml` 在每次 CI 融合时自动注入到 `My_Auto.conf` 的 `[Proxy Group]` 顶部，导入小火箭后在"代理分组"里点选具体节点即可，无需改名。
>
> ⚠️ `crypto_uk.list` 已废弃删除，欧洲合规平台（Kraken/Nexo/Neverless）已并入 `crypto_tw.list`。

---

### 缓存刷新与订阅链接

* **CDN 强制刷新**（更新代码后在新标签页访问一次清除缓存）：
* oldmoney: `https://purge.jsdelivr.net/gh/aliang-crypto/MyRules@main/oldmoney.list`
* crypto_tw: `https://purge.jsdelivr.net/gh/aliang-crypto/MyRules@main/crypto_tw.list`
* crypto_hk: `https://purge.jsdelivr.net/gh/aliang-crypto/MyRules@main/crypto_hk.list`
* ai_us: `https://purge.jsdelivr.net/gh/aliang-crypto/MyRules@main/ai_us.list`

* **总订阅配置**：`https://cdn.jsdelivr.net/gh/aliang-crypto/MyRules@main/My_Auto.conf`
* **模块订阅**：`https://cdn.jsdelivr.net/gh/aliang-crypto/MyRules@main/GlobalRouting.sgmodule`

---

### 规则订阅链接（优先推荐 jsDelivr CDN 加速）

| 规则名称 | 策略出口 | jsDelivr CDN 加速链接（推荐） | GitHub Raw 原生直链 |
|:--- |:--- |:--- |:--- |
| **oldmoney** | **DIRECT（直连）** | `https://cdn.jsdelivr.net/gh/aliang-crypto/MyRules@main/oldmoney.list` | `https://raw.githubusercontent.com/aliang-crypto/MyRules/main/oldmoney.list` |
| **Crypto_HK** | **HK（自建香港分组）** | `https://cdn.jsdelivr.net/gh/aliang-crypto/MyRules@main/crypto_hk.list` | `https://raw.githubusercontent.com/aliang-crypto/MyRules/main/crypto_hk.list` |
| **Crypto_TW** | **TW（自建台湾分组）** | `https://cdn.jsdelivr.net/gh/aliang-crypto/MyRules@main/crypto_tw.list` | `https://raw.githubusercontent.com/aliang-crypto/MyRules/main/crypto_tw.list` |
| **AI_Media_US** | **DMIT-US（自建美国分组）** | `https://cdn.jsdelivr.net/gh/aliang-crypto/MyRules@main/ai_us.list` | `https://raw.githubusercontent.com/aliang-crypto/MyRules/main/ai_us.list` |

---

### Shadowrocket 挂载与排序说明

1. **添加规则集**：在➔ 点击当前激活的配置文件 ➔➔ 点击右上角 `+` 号：
* **类型**：选择 `RULE-SET`
* **策略**：
* `oldmoney.list` ➔ **DIRECT**
* `crypto_hk.list` ➔ HK 分组
* `crypto_tw.list` ➔ TW 分组
* `ai_us.list` ➔ DMIT-US 分组

2. **规则优先级排序（自上而下，严格按此顺序拖动）**：
* 🥇 **1. oldmoney.list** ➔ `DIRECT`（置于最顶端，保证金融/支付无条件走原生网络）
* 🥈 **2. crypto_hk.list** ➔ HK（预测市场，台湾打不开，必须优先命中）
* 🥉 **3. crypto_tw.list** ➔ TW（其余全量加密资产）
* 4️⃣ **4. ai_us.list** ➔ DMIT-US（AI / 流媒体）
* 🎯 **5. 懒人配置自带的其它规则** ➔ （国内直连、常规分流等）
* 🛡️ **6. FINAL** ➔ DMIT-US（漏网流量统一走美区 DMIT）

3. **分组选节点**：在"代理分组"里点开 DMIT-US、TW、HK，分别选好你要用的节点即可。分组由 CI 自动注入，无需改名。

---

### DNS 设置说明

DNS 与通用偏好已写死在 `.github/workflows/sync.yml`，每次 CI 融合自动应用，不用在小火箭里手动改（对照手机端截图整理）：

- `dns-server`：Cloudflare + Google DoH（个人偏好）
- `direct-dns-server`：doh.pub + 阿里 DoH，直连域名走国内解析
- `fallback-dns-server`：改回 `system`。**之前 Maya App 打不开的元凶**：备用 DNS 被改成 1.1.1.1/8.8.8.8 后，直连 DNS 只要超时 2 秒就回退到境外 DNS，银行域名被解析到错误地区
- `hijack-dns`：8.8.8.8:53、8.8.4.4:53、1.1.1.1:53
- `ipv6 = false`、`always-real-ip = *.apple.com`
