# HuHoBot BDSAdapter Adapter

[![GitHub Release](https://img.shields.io/github/v/release/HuHoBot/BDSAdapter?style=for-the-badge)](https://github.com/HuHoBot/BDSAdapter/releases)
[![License](https://img.shields.io/github/license/HuHoBot/BDSAdapter?style=for-the-badge)](https://github.com/HuHoBot/BDSAdapter/blob/main/LICENSE)

专为BDS设计的下一代基岩版服务器管理解决方案，提供安全的无第三方QQ机器人依赖管理体验。

### 进阶功能

- **扩展API**
    - 自定义命令系统(详见下文)

## 📥 安装指南

### 环境要求

- LegacyScriptEngine 0.9.4+

### 快速开始

1. **访问 GitHub Releases 页面**：
	- 打开浏览器，访问 [HuHoBot-BDSAdapter Releases](https://github.com/HuHoBot/BDSAdapter/releases)
	- 下载最新版本的 `HuHoBot-BDS-vx.x.x.zip` 文件

2. **放置插件文件**：
	- 将下载的 `HuHoBot-BDS-vx.x.x.zip` 文件`解压后`放入服务器的 `plugins` 目录中

3. **重启服务器**：
	- 重启你的 Minecraft 服务器以加载新插件

4. **添加机器人**
	- [加入交流群](http://qm.qq.com/cgi-bin/qm/qr?_wv=1027&k=N6tVRxGR8sDwYHBx9YgAhkqRTp1gseyk&authKey=M7Fd3Op6nHjXjSXefBtHBPqIq2wtX8AfufZor9DrfRrJkhyS2rohkt7iuOSwbtn8&noverify=0&group_code=1005746321) 点击HuHo_Bot头像并添加到群聊

5. **完成绑定**：
	- 按照控制台提示完成服务器与机器人的绑定操作

### 高级配置（可选）

- 如果需要自定义功能，请参考`⚙️ 配置示例`进行详细设置

---

## ⚙️ 配置示例

```json5
{
	"serverId": "", //不用管
	"hashKey": "", //不用管
	"serverName": "server", // 服务器名称
	"addSimulatedPlayerTip": true, //是否添加模拟玩家提示
	"chatFormat": {
		"game": "<{name}> {msg}", // 群聊格式
		"group": "群:<{nick}> {msg}"
	},
	"motd": {
		"server_ip": "play.easecation.net", //使用/查在线的时候显示的图片地址（改成你自己的进服IP）
		"server_port": 19132, //使用/查在线的时候显示的图片地址（改成你自己的进服端口）
		"api": "https://motdbe.blackbe.work/status_img?host={server_ip}:{server_port}", //使用"/查在线"时的Motd图片地址Api（无特殊需求勿动）（必须返回图片）
		"text": "共{online}人在线", //使用"/查在线"时的Motd文本，留空不显示
		"output_online_list": true, //是否显示在线列表
		"post_img": true //是否显示Motd图片
	},
	"customCommand": [
		{
			"key": "加白名", //执行关键词，可使用"/执行 关键词 参数1 参数2"来执行自定义命令
			"command": "whitelist add &1", //&1为参数占位符，第一个参数为&1，第二个&2，以此类推
			"permission": 0 //0是普通权限，大于0则为管理员权限
		},
		{
			"key": "管理加白名",
			"command": "whitelist add &1",
			"permission": 1
		}
	],
	"version": 2
}

```

### 配置自定义命令

#### 通过配置文件设置

在 `config.json` 文件中，你可以通过 `customCommand` 字段来定义自定义命令。每个自定义命令包含以下属性：

- **key**：触发命令的关键词（字符串）
- **command**：实际执行的服务器命令（字符串）
- **permission**：权限级别（整数）

示例配置如下：

```json5
{
    "customCommand": [
		{
			"key": "加白名", //执行关键词，可使用"/执行 关键词 参数1 参数2"来执行自定义命令
			"command": "whitelist add &1", //&1为参数占位符，第一个参数为&1，第二个&2，以此类推
			"permission": 0 //0是普通权限，大于0则为管理员权限
		},
		{
			"key": "管理加白名",
			"command": "whitelist add &1",
			"permission": 1
		}
	]
}
```

#### 通过插件设置

如果你需要更详细的开发指南和高级功能，请查阅[开发文档](../Develop/LSE.md)。

## 🤝 参与贡献

欢迎提交PR或通过[Discussions](https://github.com/HuHoBot/BDSAdapter/discussions)提出建议

