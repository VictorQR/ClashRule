# VictorQR's Clash Rule Repository

🎯 一套为 [Clash.Meta](https://github.com/MetaCubeX/Clash.Meta) 量身打造的个人自用规则集，旨在与主流规则互补，实现更精细化的网络流量管理。

<p align="center">
    <img src="https://img.shields.io/github/last-commit/VictorQR/ClashRule?style=for-the-badge&logo=github&label=最后提交" alt="最后提交">
    <img src="https://img.shields.io/github/repo-size/VictorQR/ClashRule?style=for-the-badge&logo=github&label=仓库大小" alt="仓库大小">
    <img src="https://img.shields.io/github/license/VictorQR/ClashRule?style=for-the-badge&label=许可证" alt="许可证">
</p>

---

## 📖 关于此仓库

本项目是我个人使用的 Clash.Meta 规则集，主要作为对 [ACL4SSR](https://github.com/ACL4SSR/ACL4SSR) 和 [blackmatrix7](https://github.com/blackmatrix7/ios_rule_script) 等通用规则的补充和优化。 它专注于处理一些特定应用和服务的流量，以满足个性化的代理需求。

这些规则旨在：
* **精准定位**：为特定应用（如 AI 工具、游戏平台）创建独立的规则列表。
* **优化体验**：修正一些通用规则可能存在的不足，确保常用服务的访问流畅。
* **易于集成**：可以方便地通过 `rule-provider` 或订阅转换工具整合进你现有的 Clash 配置中。

## 📁 规则集说明

本仓库主要提供以下几个自定义规则列表，存放于 `Ruleset` 目录下。

| 规则文件 | 描述 | Raw 链接 (点击复制) |
| :--- | :--- | :--- |
| 🤖 `AI.list` | 专为 OpenAI (ChatGPT), Claude, Google (Bard/Gemini) 等 AI 服务定制的代理规则。 | `https://raw.githubusercontent.com/VictorQR/ClashRule/main/Ruleset/AI.list` |
| 🚀 `Proxy.list` | 需要通过代理访问的补充规则，包含一些开发工具、游戏平台及个人常用网站。 | `https://raw.githubusercontent.com/VictorQR/ClashRule/main/Ruleset/Proxy.list` |
| 🎯 `Direct.list`| 需要强制直连的补充规则，主要覆盖国内服务、游戏CDN及其他特定直连域名。 | `https://raw.githubusercontent.com/VictorQR/ClashRule/main/Ruleset/Direct.list` |
| 🅿️ `PreProxy.list`| 前置代理规则，主要用于处理 PikPak 等特殊应用的登录和API请求。 | `https://raw.githubusercontent.com/VictorQR/ClashRule/main/Ruleset/PreProxy.list` |
| ⚙️ `ClashRule.ini` | 一个用于**订阅转换工具**（如 Sub-Store）的**示例配置文件**，展示了如何将本仓库的规则与其它通用规则集合并。 | `https://raw.githubusercontent.com/VictorQR/ClashRule/main/config/ClashRule.ini` |

## 🛠️ 如何使用

你可以通过以下两种主流方式来使用本仓库的规则。

### 方式一：在 Clash 配置文件中直接引用

你可以在你的主配置文件（例如 `config.yaml`）中的 `rule-providers` 部分添加这些规则，然后在 `rules` 部分进行调用。

**示例：**
```yaml
rule-providers:
  # 定义一个名为 MyAI 的规则提供者，引用本仓库的 AI.list
  MyAI:
    type: http
    behavior: classical # classical 对应普通 list 规则
    url: "[https://raw.githubusercontent.com/VictorQR/ClashRule/main/Ruleset/AI.list](https://raw.githubusercontent.com/VictorQR/ClashRule/main/Ruleset/AI.list)"
    path: ./ruleset/ai.list # 定义规则下载到本地的路径
    interval: 86400 # 更新间隔（秒），86400秒 = 24小时

  # 定义一个名为 MyDirect 的规则提供者
  MyDirect:
    type: http
    behavior: classical
    url: "[https://raw.githubusercontent.com/VictorQR/ClashRule/main/Ruleset/Direct.list](https://raw.githubusercontent.com/VictorQR/ClashRule/main/Ruleset/Direct.list)"
    path: ./ruleset/direct.list
    interval: 86400

# 在规则部分使用上面定义的规则集
rules:
  - RULE-SET,MyAI,PROXY # 让 MyAI 规则集走代理
  - RULE-SET,MyDirect,DIRECT # 让 MyDirect 规则集直连
  # ... 其他规则
```

### 方式二：通过订阅转换工具（如 Sub-Store）

本仓库的 `config/ClashRule.ini` 文件就是一份可以直接用于订阅转换的模板。 你可以：
1.  将 `config/ClashRule.ini` 的内容作为远程配置片段导入到你的订阅转换工具中。
2.  在工具中组合你的机场订阅和这份远程配置，生成一份包含所有规则的、完整的个人配置文件。

## 🙏 致谢

本规则集的完整实现（参考 `ClashRule.ini`）大量引用了以下社区维护的规则，感谢他们的辛勤付出：

* [ACL4SSR/ACL4SSR](https://github.com/ACL4SSR/ACL4SSR)
* [blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script)

## 📄 许可证

本项目采用 The MIT License 开源。