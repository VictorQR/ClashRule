# VictorQR's Clash Rule Repository

一套为 [Clash.Meta](https://github.com/MetaCubeX/Clash.Meta) 量身打造的个人自用规则集，旨在作为主流规则的**高效补充包**，实现更精细化的网络流量管理。

---

## 📖 设计理念

本项目并非一套大而全的独立规则，而是作为对 [ACL4SSR](https://github.com/ACL4SSR/ACL4SSR) 和 [blackmatrix7](https://github.com/blackmatrix7/ios_rule_script) 等优秀通用规则的补充与优化。

它专注于解决以下问题：
* **精准分流**：为 AI 服务、特定游戏、网盘等创建独立的精细化规则。
* **修正补充**：处理一些通用规则可能存在的覆盖不足或冲突问题。
* **轻量高效**：避免与上游规则集的大量重复，保持个人配置的简洁与高效。

## 📁 规则集说明

本仓库的核心规则均存放于 `Ruleset` 目录下。

| 规则文件 | 描述 | Raw 链接 (一键复制) |
| :--- | :--- | :--- |
| 🤖 `AI.list` | **AI 服务专用**<br>覆盖 OpenAI (ChatGPT), Claude, Google (Gemini), Perplexity 等主流 AI 服务。 | `https://raw.githubusercontent.com/VictorQR/ClashRule/main/Ruleset/AI.list` |
| 🚀 `Proxy.list` | **代理补充**<br>包含开发工具、个人常用网站及其他需要代理的域名。 | `https://raw.githubusercontent.com/VictorQR/ClashRule/main/Ruleset/Proxy.list` |
| 🎯 `Direct.list` | **直连补充**<br>经精简优化，专注于补充通用规则集未覆盖的国内服务、游戏 CDN 及其他需强制直连的域名。 | `https://raw.githubusercontent.com/VictorQR/ClashRule/main/Ruleset/Direct.list` |
| 🅿️ `PreProxy.list`| **前置代理**<br>用于处理 `PikPak` 等特殊应用的登录和 API 请求，确保最高匹配优先级。 | `https://raw.githubusercontent.com/VictorQR/ClashRule/main/Ruleset/PreProxy.list` |

此外，`config` 目录下提供了一个 `ClashRule.ini` 文件，这是一个用于**订阅转换工具**（如 Sub-Store）的**示例配置文件**，展示了如何将本仓库的规则与其它通用规则集合并。

## 🛠️ 如何使用

### 方式一：在 Clash 配置文件中直接引用 (推荐)

在你的主配置文件（例如 `config.yaml`）中的 `rule-providers` 部分添加这些规则，然后在 `rules` 部分进行调用。这种方法可以保持你的主配置文件整洁，并能自动更新规则。

**示例 `config.yaml`:**
```yaml
# 1. 在 rule-providers 部分定义规则提供者
rule-providers:
  MyAI:
    type: http
    behavior: classical
    url: "[https://raw.githubusercontent.com/VictorQR/ClashRule/main/Ruleset/AI.list](https://raw.githubusercontent.com/VictorQR/ClashRule/main/Ruleset/AI.list)"
    path: ./ruleset/AI.list
    interval: 86400 # 每天更新一次

  MyDirect:
    type: http
    behavior: classical
    url: "[https://raw.githubusercontent.com/VictorQR/ClashRule/main/Ruleset/Direct.list](https://raw.githubusercontent.com/VictorQR/ClashRule/main/Ruleset/Direct.list)"
    path: ./ruleset/Direct.list
    interval: 86400

  # ... 根据需要添加其他规则 ...

# 2. 在 rules 部分按需调用
rules:
  # 建议将个人补充规则放在前面，以确保优先生效
  - RULE-SET,MyAI,PROXY # 让 AI 服务走代理
  - RULE-SET,MyDirect,DIRECT # 强制直连
  # ... 接着是你引用的其他通用规则 ...
````

### 方式二：通过订阅转换工具（如 Sub-Store）

本仓库的 `config/ClashRule.ini` 文件是一份可以直接用于订阅转换的模板。

1.  将 `ClashRule.ini` 的内容作为远程配置片段导入到你的订阅转换工具中。
2.  在工具中组合你的机场订阅和这份远程配置，生成一份包含所有规则的、完整的个人配置文件。

## 🙏 致谢

本规则集的实现（参考 `ClashRule.ini`）大量引用了以下社区维护的规则，感谢他们的辛勤付出：

  * [ACL4SSR/ACL4SSR](https://github.com/ACL4SSR/ACL4SSR)
  * [blackmatrix7/ios\_rule\_script](https://github.com/blackmatrix7/ios_rule_script)

## 📄 许可证

本项目采用 [The MIT License](https://github.com/VictorQR/ClashRule/blob/main/LICENSE) 开源。

