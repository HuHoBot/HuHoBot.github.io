# HuHoBot Allay Adapter

[![GitHub Release](https://img.shields.io/github/v/release/HuHoBot/AllayMCAdapter?style=for-the-badge)](https://github.com/HuHoBot/SpigotAdapter/releases)
[![License](https://img.shields.io/github/license/HuHoBot/AllayMCAdapter?style=for-the-badge)](https://github.com/HuHoBot/SpigotAdapter/blob/main/LICENSE)
[![Build Status](https://img.shields.io/github/actions/workflow/status/HuHoBot/AllayMCAdapter/build.yml?style=for-the-badge)](https://github.com/HuHoBot/SpigotAdapter/actions)

专为AllayMC设计的下一代基岩版服务器管理解决方案，提供安全的无第三方QQ机器人依赖管理体验。

!!! note

    由于技术原因，暂时无法为Allay提供命令回调，请等待后续更新.

### 进阶功能

- **扩展API**
    - 自定义命令系统(详见下文)

## 📥 安装指南

### 环境要求

- Java 21+
- Allay Server 0.2.0+

### 快速开始

1. **访问 GitHub Releases 页面**：
    - 打开浏览器，访问 [HuHoBot-AllayAdapter Releases](https://github.com/HuHoBot/AllayMCAdapter/releases)
    - 下载最新版本的 `HuHoBot-vx.x.x-AllayMC.jar` 文件

2. **参照** [快速开始](../QuickStart/index.md)


### 高级配置（可选）

- 如果需要自定义功能，请参考`⚙️ 配置示例`进行详细设置

---

## ⚙️ 配置示例

```yaml
# 服务器唯一ID (启动时自动生成)
# ! 请勿手动修改，留空即可
serverId: 
# 通信加密密钥 (绑定后自动获取)
# ! 请勿手动修改，留空即可
hashKey: 
# 群聊消息格式 (可用变量: {nick}, {msg})
chatFormatGroup: 群:<{nick}> {msg}
# MOTD服务器地址
# 格式: 地址:端口 (示例: play.easecation.net:19132)
motdUrl: play.easecation.net:19132
# 服务器显示名称
serverName: AllayMC
# 自定义命令列表
customCommand:
  - key: "加白名" #执行关键词，可使用"/执行 关键词 参数1 参数2"来执行自定义命令
    command: "whitelist add &1" #&1为参数占位符，第一个参数为&1，第二个&2，以此类推
    permission: 0 #0是普通权限，大于0则为管理员权限
  - key: 管理加白名
    command: whitelist add &1
    permission: 1

```

### 配置自定义命令

#### 通过配置文件设置

在 `config.yml` 文件中，你可以通过 `customCommand` 字段来定义自定义命令。每个自定义命令包含以下属性：

- **key**：触发命令的关键词（字符串）
- **command**：实际执行的服务器命令（字符串）
- **permission**：权限级别（整数）

示例配置如下：

```yaml
customCommand:
  - key: "加白名" #执行关键词，可使用"/执行 关键词 参数1 参数2"来执行自定义命令
    command: "whitelist add &1" #&1为参数占位符，第一个参数为&1，第二个&2，以此类推
    permission: 0 #0是普通权限，大于0则为管理员权限
```

## 🤝 参与贡献

欢迎提交PR或通过[Discussions](https://github.com/HuHoBot/SpigotAdapter/discussions)提出建议

