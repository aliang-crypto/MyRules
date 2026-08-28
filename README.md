# 🛡️ MyRules - 私有分流规则库

个人专属分流规则集，针对加密资产、Web3 钱包、链上 DApp 及跨国合规业务进行精细化路由隔离。

---
改完代码，CDN 强刷：
新标签页访问一次清楚缓存连接（只需把原链接的 cdn 改为 purge）：
https://purge.jsdelivr.net/gh/aliang-crypto/MyRules@main/crypto_all.list

### 规则订阅链接（优先推荐 jsDelivr CDN 加速）

| 规则名称 | 适用业务 / 平台 | 推荐策略出口 | jsDelivr CDN 加速链接（推荐） | GitHub Raw 原生直链 |
| :--- | :--- | :--- | :--- | :--- |
| **Crypto_UK** | 🇬🇧 英国 (UK) | `https://cdn.jsdelivr.net/gh/aliang-crypto/MyRules@main/crypto_uk.list` | `https://raw.githubusercontent.com/aliang-crypto/MyRules/main/crypto_uk.list` |
| **Crypto_All** | 🇹🇼 台湾 (TW) | `https://cdn.jsdelivr.net/gh/aliang-crypto/MyRules@main/crypto_all.list` | `https://raw.githubusercontent.com/aliang-crypto/MyRules/main/crypto_all.list` |

---

### 小火箭 (Shadowrocket) 挂载与排序说明

1. 在【配置】➔【规则】中以 `RULE-SET` 方式添加上述 CDN 链接。
2. **规则优先级排序（自上而下）**：
   - 🔼 **1. `crypto_uk.list`** ➔ 绑定英国节点分组
   - 🔽 **2. `crypto_all.list`** ➔ 绑定台湾节点分组
3. 保证欧洲特定合规平台优先匹配英国线路，其余全量加密资产流量统一进入台湾远端解析黑盒。
