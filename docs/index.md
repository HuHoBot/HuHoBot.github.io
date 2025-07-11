# HuHoBot
新一代Minecraft服务器管理机器人解决方案，突破传统机器人框架限制，提供更安全稳定的交互体验。

# 在阅读以下内容之前，您是否有一定的阅读和开服基础？能否按文档进行操作？
!!! warning
    **请务必阅读此提示，否则将无法使用HuHoBot**
- 如果是，请继续阅读
- **如果否，请先查看此链接[AI一键解答](AskAI/index.md)**

## 🌟 核心优势

| 特性     | 传统方案             | HuHoBot           |
|--------|------------------|-------------------|
| 账号安全   | ❌ 需要实体QQ号，存在封号风险 | ✅ 无QQ第三方客户端依赖，零风控 |
| 部署复杂度  | ❌ 需搭建完整机器人框架     | ✅ 即装即用，一键绑定       |
| 服务器兼容性 | ❌ 部分面板服不支持       | ✅ 全平台兼容，有网即用      |
| 协议更新影响 | ❌ 需要频繁适配新协议      | ✅ 协议无关设计，相对稳定     |

## 🚀 功能特性

### 核心功能

- **无缝绑定**：通过WebSocket实现服务器与控制端即时绑定
- **智能风控规避**：基于事件驱动的非侵入式通信协议

## ☕ 快速开始
- 如何安装？请看[快速开始](QuickStart/index.md)

## 📡指令列表
- **快速获取指令列表**: 可在群内输入`@HuHoBot /帮助`可快速查看指令列表
- 详细说明请见下文

## 🤖 指令分类说明

### ⚙️ **白名单管理**
| 指令格式                  | 描述                     | 权限   |
|---------------------------|--------------------------|--------|
| `/添加白名单 <name>`       | 向服务器添加一个白名单     | 管理员 |
| `/删除白名单 <name>`       | 从服务器删除一个白名单     | 管理员 |
| `/查白名单 [关键词/页码]`   | 查询服务器白名单列表       | 管理员 |

---

### 🛡️ **服务器管理**
| 指令格式                  | 描述                     | 权限   |
|---------------------------|--------------------------|--------|
| `/绑定 <serverId> [多群]`  | 绑定目标服务器            | 管理员 |
| `/管理帮助`                | [查看详细管理指南](AdminHelp/index.md) | 管理员 |
| `/执行命令 <command>`      | 向服务器发送执行命令请求    | 管理员 |

!!! note 

    新版已取消`/执行`命令，可使用 `/关键词 参数1 参数2` 直接执行
    如果执行者拥有管理员权限，则自动使用原先的`/管理员执行`

---

### 💬 **群服互通**
| 指令格式                  | 描述                     | 权限   |
|---------------------------|--------------------------|--------|
| `/设置名称 <name>`         | 设置群服互通显示名称       | 任何人 |
| `/发信息 <message>`        | 向服务器发送消息           | 任何人 |
| `/查在线`                  | 查询服务器在线玩家         | 任何人 |
| `/在线服务器`              | 查看当前在线服务器         | 任何人 |

--- 

### 🌐 **服务器状态查询**
| 指令格式                  | 描述                     | 权限   |
|---------------------------|--------------------------|--------|
| `/motd <url> <platform>`  | 查询服务器Motd信息        | 任何人 |
| `/blockMotd`              | 禁止本群Motd某服务器      | 管理员 |
| `/unblockMotd`            | 允许本群Motd某服务器      | 管理员 |

---

### 🔑 **身份认证**
| 指令格式                  | 描述                     | 权限   |
|---------------------------|--------------------------|--------|
| `/认证 <qq>`               | 认证QQ号                 | 任何人 |
| `/认证 <qq> <openId>`      | 管理员人工认证QQ号        | 管理员 |
| `/解除认证 <openId>`       | 解除已认证QQ号            | 管理员 |


!!! warning

    表中没有提到的功能就是不支持，如有需求，请自行根据开发文档自行开发。


## 📞QQ交流群
### 群号:1005746321 [点我加入](http://qm.qq.com/cgi-bin/qm/qr?_wv=1027&k=N6tVRxGR8sDwYHBx9YgAhkqRTp1gseyk&authKey=M7Fd3Op6nHjXjSXefBtHBPqIq2wtX8AfufZor9DrfRrJkhyS2rohkt7iuOSwbtn8&noverify=0&group_code=1005746321)

## ❓ 常见问题
- 请到[常见问题](Question/index.md)页面查看


## 📄 开源协议

[GNU General Public License v3.0](LICENSE.txt) - 自由使用、修改和分发，但需遵守以下条款：

- **开源义务**：任何衍生作品必须保持开源
- **相同许可**：修改后的版本必须使用相同许可证
- **版权声明**：必须保留原始版权声明

完整协议文本请查看 [LICENSE](LICENSE.txt) 文件
