# 适配器开发

HuHoBotPenguin 为不同 Minecraft 服务端提供独立的附属插件 API。请根据运行平台阅读对应页面：

- [Spigot/Paper](spigot.md)
- [Nukkit-MOT](nukkit-mot.md)
- [BungeeCord](bungeecord.md)
- [Velocity](velocity.md)
- [Allay](allay.md)

## 公共 API

所有适配器都提供以下能力：

- 监听 QQ 群消息：`OnBotRecvMsg`
- 监听自定义命令：`OnBotCommand`
- 读取统一的 `MsgPack` 消息快照
- 取消事件，阻止后续默认转发
- 回复触发消息
- 注册和注销运行时自定义命令
- 向所有配置群或指定群发送文本、Markdown

各平台的事件类位于不同包中，但 API 结构保持一致。事件注册必须使用目标平台自己的事件系统。

## MsgPack

`MsgPack` 位于 `server-AdapterCommon`，适配器 JAR 中也会包含该类：

```java
import cn.huohuas001.huhobotPenguin.adapter.api.MsgPack;
```

它是不可变消息快照，不直接暴露 QQ SDK 的原始事件对象。

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `messageId` | `String` | QQ 消息 ID |
| `groupOpenId` | `String` | QQ 群 OpenID，用于回复和指定群发送 |
| `groupId` | `String?` | QQ 群 ID，可能为空 |
| `sender` | `Sender` | 消息发送者 |
| `content` | `String` | 消息文本 |
| `rawContent` | `String` | 原始消息文本 |
| `timestamp` | `String?` | 消息时间戳 |
| `messageSequence` | `Int` | 回复消息所需的消息序号 |
| `commandKey` | `String?` | 自定义命令键 |
| `commandArguments` | `String?` | 自定义命令参数 |
| `mentions` | `List<Mention>` | At 用户列表 |
| `attachments` | `List<Attachment>` | 附件列表 |

Java 通过 `getMessageId()`、`getGroupOpenId()`、`getSender()` 等方法访问字段。

## 事件

`OnBotRecvMsg` 在 QQ 消息进入公共命令处理前触发。适合进行消息过滤、审计或自定义回复。

`OnBotCommand` 在消息命中运行时注册的自定义命令时触发。此时 `MsgPack` 中会额外填充 `commandKey` 和 `commandArguments`。

两个事件都支持：

```java
event.replyText("普通文本");
event.replyMarkdown("Markdown 内容");
event.setCancelled(true);
```

`replyText` 和 `replyMarkdown` 返回 `boolean`。返回 `true` 表示发送请求已提交，返回 `false` 表示机器人未启动、参数为空或发送失败。

## 运行时命令

各平台主类提供：

```text
registerBotCommand(key, command, permission, pushMenu)
unregisterBotCommand(key)
```

命令模板支持：

- `{params}`：完整参数
- `{group}`：群 ID
- `{user}`：用户 ID
- `{0}`、`{1}`：按空格拆分后的参数
- `&1`、`&2`：按空格拆分后的参数

`permission > 0` 表示仅管理员可以执行，`pushMenu = true` 表示同步到 QQ 指令面板。

## 线程约束

QQ 消息回调来自 QQ 客户端线程。Spigot、Nukkit、Allay 会切换到平台服务器线程后触发事件；Bungee 使用 Bungee 事件总线；Velocity 等待 `EventManager.fire` 完成后再读取取消状态。

监听器中不要执行长时间阻塞操作。网络请求、数据库操作和复杂计算应提交到平台异步调度器。

## 版本

附属插件应使用与服务器中 HuHoBotPenguin 相同版本的适配器 JAR 编译，并使用 `compileOnly`，避免将另一份 HuHoBot 类打包进附属插件。
