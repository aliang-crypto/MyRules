# 🔵 MyRules - 自用分流规则

自用分流规则集，针对加密、传统金融、流媒体、AI 等跨国合规业务进行精细化路由分流隔离。

---

### 缓存刷新与订阅链接

* **CDN 强制刷新**（更新代码后在新标签页访问一次清除缓存）：
  * oldmoney: `https://purge.jsdelivr.net/gh/aliang-crypto/MyRules@main/OldMoney.list`
  * Crypto_All: `https://purge.jsdelivr.net/gh/aliang-crypto/MyRules@main/crypto_all.list`
  * Crypto_UK: `https://purge.jsdelivr.net/gh/aliang-crypto/MyRules@main/crypto_uk.list`

* **总订阅配置**：`https://cdn.jsdelivr.net/gh/aliang-crypto/MyRules@main/My_Auto.conf`
* **模块订阅**：`https://cdn.jsdelivr.net/gh/aliang-crypto/MyRules@main/GlobalRouting.sgmodule`

---

### 规则订阅链接（优先推荐 jsDelivr CDN 加速）

| 规则名称 | 策略出口 | jsDelivr CDN 加速链接（推荐） | GitHub Raw 原生直链 |
| :--- | :--- | :--- | :--- |
| **Old_Money** | **DIRECT (直连)** | `https://cdn.jsdelivr.net/gh/aliang-crypto/MyRules@main/OldMoney.list` | `https://raw.githubusercontent.com/aliang-crypto/MyRules/main/OldMoney.list` |
| **Crypto_UK** | **GB 英国 (UK)** | `https://cdn.jsdelivr.net/gh/aliang-crypto/MyRules@main/crypto_uk.list` | `https://raw.githubusercontent.com/aliang-crypto/MyRules/main/crypto_uk.list` |
| **Crypto_All** | **TW 台湾 (TW)** | `https://cdn.jsdelivr.net/gh/aliang-crypto/MyRules@main/crypto_all.list` | `https://raw.githubusercontent.com/aliang-crypto/MyRules/main/crypto_all.list` |

---

### Shadowrocket 挂载与排序说明

1. **添加规则集**：在【配置】➔ 点击当前激活的配置文件 ➔【规则】➔ 点击右上角 `+` 号：
   * **类型**：选择 `RULE-SET`
   * **策略**：
     * `oldmoney.list` ➔ 选 **DIRECT**
     * `crypto_uk.list` ➔ 选 **英国节点分组**
     * `crypto_all.list` ➔ 选 **台湾节点分组**

2. **规则优先级排序（自上而下，严格按此顺序拖动）**：
   * 🥇 **1. oldmoney.list** ➔ `DIRECT`（置于最顶端，保证金融/支付无条件走原生网络）
   * 🥈 **2. crypto_uk.list** ➔ `英国节点`（保证特定英区金融平台优先命中合规出口）
   * 🥉 **3. crypto_all.list** ➔ `台湾节点`（其余全量 Web3/加密平台走台湾远端解析）
   * 🎯 **4. 懒人配置自带的其它规则** ➔ （流媒体、常规分流等）
   * 🛡️ **5. FINAL / 漏斗规则** ➔ `DIRECT` 或 `PROXY`
