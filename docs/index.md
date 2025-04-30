# HuHoBot
新一代Minecraft服务器管理机器人解决方案，突破传统机器人框架限制，提供更安全稳定的交互体验。

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

### 功能列表

| 命令     | 描述             |
|--------|----------------|
| /添加白名单 | 向服务器内添加一个白名单   |
| /删除白名单 | 向服务器内删除一个白名单   |
| /绑定    | 绑定服务器          |
| /设置名称  | 设置自己在本群群服互通的名称 |
| /发信息   | 群服互通向服务器内发送消息  |
| /执行命令  | 向服务器发送执行命令的请求  |
| /查白名单  | 查询服务器内置白名单     |
| /查在线   | 查询服务器在线名单      |
| /在线服务器 | 查询在线服务器        |
| /执行    | 执行自定义指令        |
| /管理员执行 | 以管理员身份运行自定义内容  |

!!! warning

    表中没有提到的功能就是不支持，如有需求，请自行根据开发文档自行开发。


## 📞QQ交流群
### 群号:1005746321 [点我加入](http://qm.qq.com/cgi-bin/qm/qr?_wv=1027&k=N6tVRxGR8sDwYHBx9YgAhkqRTp1gseyk&authKey=M7Fd3Op6nHjXjSXefBtHBPqIq2wtX8AfufZor9DrfRrJkhyS2rohkt7iuOSwbtn8&noverify=0&group_code=1005746321)

## ❓ 常见问题
<details>
<summary>📡 怎么绑定不上？</summary>
检查控制台是否输出"握手成功"的字段
<br/>
如果未出现，请使用<code>/huhobot reconnect</code>手动重新建立连接
</details>

<details>
<summary>🤔 需要准备QQ号吗？</summary>
完全不需要！本方案采用全新的通信协议，彻底摆脱对第三方聊天平台的依赖。
</details>

<details>
<summary>🛡️ 支持哪些服务器版本？</summary>
✅ Spigot/Folia: 已测试版本：<code>1.8 - 1.21</code> 
<br/>
✅ EndStone: 已测试版本：<code>1.21.60+</code>
<br/>
✅ LSE: 已测试版本：<code>1.21.50+</code>
<br/>
✅ Allay: 已测试版本：<code>0.2.0+</code>
</details>

<details>
<summary>🔧 如何更新配置？</summary>
支持热重载配置：<code>/huhobot reload</code>
</details>

<details>
<summary>🤖 怎么开启消息互通？</summary>
本机器人不支持群服消息互通，因官方机器人API限制每个群每月仅能发送三条主动消息
</details>

<details>
<summary>🌐 查在线显示其他服务器信息？</summary>
请修改配置文件中的 <code>motdUrl</code> 字段为你的服务器地址  
<br/>
示例：<code>motdUrl: "play.yourserver.com:25565"</code>
<br/>
部分适配器配置文件为motd字段，请根据实际情况参考分文档查看。
</details>

<details>
<summary>🔍 查在线无反应怎么办？</summary>
排查步骤：  
<br/>
1. 检查连接状态，使用 <code>/huhobot reconnect</code> 重连
<br/>
2. 尝试清空 motdUrl 字段：<code>"motdUrl": ""</code>
</details>

<details>
<summary>⌨️ 执行命令无响应？</summary>
注意命令格式区别：  
<br/>
- <code>/执行 加白</code> → 用于自定义指令回调
<br/>
- <code>/执行命令 list</code> → 向控制台发送命令
</details>

<details>
<summary>👥 允许玩家自助加白名单？</summary>
请按上文配置文件示例配置customCommand字段
<br/>
使用方式：<code>/执行 加白 "玩家ID"</code>（带空格参数需加引号）
</details>

<details>
<summary>👮 如何设置管理员？</summary>
在群内使用指令：  
<code>/管理帮助</code> → 查看管理指令列表
</details>

<details>
<summary>🏰 是否支持多个服务器？</summary>
当前版本每个群仅支持绑定一个服务器，多服务器绑定功能正在开发中  
如需管理多服务器，建议为每个服务器创建独立群组
</details>

<details>
<summary>👩‍👧‍👦 是否支持多个群？</summary>
当然支持！仅需在"/绑定"指令后加入"多群"参数即可
<br>
例如:<code>/绑定 test4270code414bbe5057198c4d91dc 多群</code>
</details>


## 📄 开源协议

[GNU General Public License v3.0](LICENSE.txt) - 自由使用、修改和分发，但需遵守以下条款：

- **开源义务**：任何衍生作品必须保持开源
- **相同许可**：修改后的版本必须使用相同许可证
- **版权声明**：必须保留原始版权声明

完整协议文本请查看 [LICENSE](LICENSE.txt) 文件
