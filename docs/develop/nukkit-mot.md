# Nukkit-MOT 适配器

本文介绍如何为 Nukkit-MOT 编写 HuHoBotPenguin 附属插件。

## 引入 SDK

将 `HuHoBot-Penguin_Nukkit-x.y.z.jar` 放到项目的 `libs` 目录：

```kotlin
dependencies {
    compileOnly(files("libs/HuHoBot-Penguin_Nukkit-x.y.z.jar"))
}
```

`plugin.yml`：

```yaml
name: MyHuHoBotAddon
main: com.example.myaddon.MyHuHoBotAddon
version: 1.0.0
api: ["1.0.5"]
depend:
  - HuHoBotPenguin
```

## 监听 QQ 群消息

事件类：

```text
cn.huohuas001.huhobotPenguin.nukkit.events.OnBotRecvMsg
```

Kotlin 示例：

```kotlin
import cn.huohuas001.huhobotPenguin.nukkit.events.OnBotRecvMsg
import cn.nukkit.event.EventHandler
import cn.nukkit.event.Listener

class BotListener : Listener {
    @EventHandler
    fun onBotMessage(event: OnBotRecvMsg) {
        val message = event.message
        if (message.content.equals("/hello", ignoreCase = true)) {
            event.replyText("你好，${message.sender.username}")
            event.setCancelled(true)
        }
    }
}
```

在插件启用时注册：

```kotlin
server.pluginManager.registerEvents(BotListener(), this)
```

Java 监听器使用 `@EventHandler`，方法只能接收一个事件参数。

## 自定义命令事件

事件类：

```text
cn.huohuas001.huhobotPenguin.nukkit.events.OnBotCommand
```

```kotlin
@EventHandler
fun onBotCommand(event: OnBotCommand) {
    if (event.message.commandKey == "hello") {
        event.replyText("参数: ${event.message.commandArguments}")
        event.setCancelled(true)
    }
}
```

消息 `/hello world` 对应：

```text
commandKey = hello
commandArguments = world
```

## 获取主插件实例

```kotlin
import cn.huohuas001.huhobotPenguin.nukkit.HuHoBotNukkit

val raw = server.pluginManager.getPlugin("HuHoBotPenguin")
if (raw is HuHoBotNukkit) {
    raw.sendBotText("来自 Nukkit 附属插件")
}
```

### 查询认证 QQ 号

```kotlin
val qq: String? = bot.getAuthenticatedQq(groupOpenId, openId)
if (qq == null) {
    // 当前 OpenID 未认证
}
```

未认证时返回 `null`，已认证时返回绑定的 QQ 号。
## 注册命令和发送消息

```kotlin
val bot = raw as HuHoBotNukkit

// 4参版本 - 注册独立命令（兼容旧 API）
bot.registerBotCommand(
    key = "hello",
    command = "say Hello {params}",
    permission = 0,
    pushMenu = true
)

// 5参版本 - 注册扩展命令（关联到扩展）
bot.registerAddon(name = "MyAddon", version = "1.0.0", description = "扩展描述", author = "作者")
bot.registerBotCommand(
    addonName = "MyAddon",
    key = "mycmd",
    command = "say Hello {params}",
    permission = 0,
    pushMenu = true
)

bot.sendBotText("发送到所有配置群")
bot.sendBotText(groupOpenId, "发送到指定群")
bot.sendBotMarkdown("# Markdown")
bot.sendBotMarkdown(groupOpenId, markdown, keyboard)

bot.unregisterBotCommand("hello")
```

命令模板支持 `{params}`、`{group}`、`{user}`、`{name}`、`{nickname}`、`{0}` 以及 `&1` 等公共占位符。

### 方法说明

- `registerAddon(name, version, description, author)`：注册扩展，返回 `boolean`
- `registerBotCommand(addonName, key, command, permission, pushMenu)`：注册扩展命令（5参）
- `registerBotCommand(key, command, permission, pushMenu)`：注册独立命令（4参，兼容旧 API）
- `permission > 0`：仅管理员可执行
- `pushMenu = true`：同步到 QQ 指令面板
- 指定群发送方法返回 `boolean`
- `unregisterBotCommand(key)` 用于移除运行时注册的命令

## 回复和取消

```kotlin
event.replyText("普通文本")
event.replyMarkdown("Markdown 内容")
event.setCancelled(true)
```

`setCancelled(true)` 会阻止这条消息继续进入默认全量转发流程。

## 注意事项

QQ 回调来自异步线程，HuHoBot 会先切换到 Nukkit 主线程再触发事件，并等待监听器执行完成后读取取消状态。监听器中仍不应执行耗时阻塞操作。
