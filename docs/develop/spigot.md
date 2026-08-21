# Spigot/Paper 适配器

本文介绍如何为 Spigot、Paper 或兼容 Bukkit API 的服务端编写 HuHoBotPenguin 附属插件。

## 引入 SDK

将 `HuHoBot-Penguin_Spigot-x.y.z.jar` 放到项目的 `libs` 目录：

```kotlin
dependencies {
    compileOnly(files("libs/HuHoBot-Penguin_Spigot-x.y.z.jar"))
    compileOnly("org.spigotmc:spigot-api:1.16.5-R0.1-SNAPSHOT")
}
```

`plugin.yml`：

```yaml
name: MyHuHoBotAddon
main: com.example.myaddon.MyHuHoBotAddon
version: 1.0.0
api-version: '1.16'
depend:
  - HuHoBotPenguin
```

`depend` 保证 HuHoBotPenguin 先于附属插件加载。

## 监听 QQ 群消息

事件类：

```java
cn.huohuas001.huhobotPenguin.spigot.events.OnBotRecvMsg
```

```java
package com.example.myaddon;

import cn.huohuas001.huhobotPenguin.spigot.events.OnBotRecvMsg;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;

public final class BotListener implements Listener {
    @EventHandler
    public void onBotMessage(OnBotRecvMsg event) {
        String user = event.getMessage().getSender().getUsername();
        String content = event.getMessage().getContent();

        if (content.equalsIgnoreCase("/hello")) {
            event.replyText("你好，" + user);
            event.setCancelled(true);
        }
    }
}
```

在 `onEnable` 注册：

```java
getServer().getPluginManager().registerEvents(new BotListener(), this);
```

取消事件会阻止 HuHoBot 后续的默认全量转发。

## 自定义命令事件

事件类：

```java
cn.huohuas001.huhobotPenguin.spigot.events.OnBotCommand
```

```java
@EventHandler
public void onBotCommand(OnBotCommand event) {
    if ("hello".equals(event.getMessage().getCommandKey())) {
        String args = event.getMessage().getCommandArguments();
        event.replyText("参数: " + args);
        event.setCancelled(true);
    }
}
```

消息 `/hello world` 对应：

```text
commandKey = hello
commandArguments = world
```

## 获取主插件实例

```java
import cn.huohuas001.huhobotPenguin.spigot.HuHoBotSpigot;
import org.bukkit.plugin.Plugin;

Plugin raw = getServer().getPluginManager().getPlugin("HuHoBotPenguin");
if (raw instanceof HuHoBotSpigot) {
    HuHoBotSpigot bot = (HuHoBotSpigot) raw;
}
```

## 注册命令和发送消息

```java
HuHoBotSpigot bot = (HuHoBotSpigot) raw;

bot.registerBotCommand(
    "hello",
    "say Hello {params}",
    0,
    true
);

bot.sendBotText("发送到配置中的所有 QQ 群");
bot.sendBotText(groupOpenId, "发送到指定 QQ 群");
bot.sendBotMarkdown("# Markdown");
bot.sendBotMarkdown(groupOpenId, markdown, keyboard);
```

方法说明：

- `permission > 0`：仅管理员可执行
- `pushMenu = true`：同步到 QQ 指令面板
- 指定群发送方法返回 `boolean`
- `unregisterBotCommand(key)` 用于移除运行时注册的命令

## 回复事件

```java
event.reply("普通文本");
event.replyText("普通文本");
event.replyMarkdown("Markdown 内容");
event.replyMarkdown("Markdown 内容", keyboard);
```

回复会自动使用原消息的消息 ID和序号。

## 注意事项

事件会在 Bukkit 主线程触发。监听器中不要进行同步网络请求或长时间数据库操作，必要时使用 Bukkit Scheduler 异步执行。
