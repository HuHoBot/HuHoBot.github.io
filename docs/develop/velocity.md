# Velocity 适配器

本文介绍如何为 Velocity 编写 HuHoBotPenguin Proxy 附属插件。

!!! note

    BungeeCord 和 Velocity 共用 `HuHoBot-Penguin_Proxy-x.y.z.jar`，但事件包名和平台注册方式不同。本页只介绍 Velocity。

## 引入 SDK

```kotlin
dependencies {
    compileOnly(files("libs/HuHoBot-Penguin_Proxy-x.y.z.jar"))
    compileOnly("com.velocitypowered:velocity-api:3.4.0-SNAPSHOT")
    kapt("com.velocitypowered:velocity-api:3.4.0-SNAPSHOT")
}
```

`velocity-plugin.json`：

```json
{
  "id": "my-huhobot-addon",
  "name": "MyHuHoBotAddon",
  "version": "1.0.0",
  "main": "com.example.myaddon.MyHuHoBotAddon",
  "dependencies": [
    { "id": "huhobot", "optional": false }
  ]
}
```

## 监听 QQ 群消息

事件类：

```text
cn.huohuas001.huhobotPenguin.velocity.events.OnBotRecvMsg
```

Velocity 没有通用的 `Cancellable` 接口，HuHoBot 事件提供 `isCancelled()` 和 `setCancelled(boolean)` 方法。

```java
import cn.huohuas001.huhobotPenguin.velocity.events.OnBotRecvMsg;
import com.velocitypowered.api.event.Subscribe;

public final class BotListener {
    @Subscribe
    public void onBotMessage(OnBotRecvMsg event) {
        if (event.getMessage().getContent().equalsIgnoreCase("/hello")) {
            event.replyText("你好");
            event.setCancelled(true);
        }
    }
}
```

注册监听器：

```java
server.getEventManager().register(this, new BotListener());
```

## 自定义命令事件

事件类：

```text
cn.huohuas001.huhobotPenguin.velocity.events.OnBotCommand
```

```java
@Subscribe
public void onBotCommand(OnBotCommand event) {
    if ("hello".equals(event.getMessage().getCommandKey())) {
        event.replyText("参数: " + event.getMessage().getCommandArguments());
        event.setCancelled(true);
    }
}
```

## 获取主插件实例

Velocity 的插件实例通常由 Guice 注入。如果需要从插件管理器查找：

```java
server.getPluginManager()
    .getPlugin("huhobot")
    .flatMap(container -> container.getInstance())
    .filter(instance -> instance instanceof HuHoBotVelocity)
    .map(instance -> (HuHoBotVelocity) instance);
```

更推荐在附属插件初始化时保存由依赖注入或平台生命周期提供的实例。

### 查询认证 QQ 号

```java
String qq = bot.getAuthenticatedQq(groupOpenId, openId);
// 未认证时 qq == null
```
## 注册命令和发送消息

```java
// 4参版本 - 注册独立命令（兼容旧 API）
bot.registerBotCommand("hello", "say Hello {params}", 0, true);

// 5参版本 - 注册扩展命令（关联到扩展）
bot.registerAddon("MyAddon", "1.0.0", "扩展描述", "作者");
bot.registerBotCommand("MyAddon", "mycmd", "say Hello {params}", 0, true);

bot.sendBotText("发送到配置中的所有群");
bot.sendBotText(groupOpenId, "发送到指定群");
bot.sendBotMarkdown("# Markdown");
bot.sendBotMarkdown(groupOpenId, markdown, keyboard);
bot.unregisterBotCommand("hello");
```

Proxy 共享 API：

```java
import cn.huohuas001.huhobotPenguin.proxy.api.ProxyBotApi;

// 4参版本
ProxyBotApi.registerBotCommand("hello", "say Hello {params}");

// 5参版本 - 注册扩展命令
ProxyBotApi.registerAddon("MyAddon", "1.0.0", "扩展描述", "作者");
ProxyBotApi.registerBotCommand("MyAddon", "mycmd", "say Hello {params}");

ProxyBotApi.sendBotText(bot, "发送到配置群");
ProxyBotApi.sendBotText(groupOpenId, "发送到指定群");
```

### 方法说明

- `registerAddon(name, version, description, author)`：注册扩展，返回 `boolean`
- `registerBotCommand(addonName, key, command, permission, pushMenu)`：注册扩展命令（5参）
- `registerBotCommand(key, command, permission, pushMenu)`：注册独立命令（4参，兼容旧 API）
- `permission > 0`：仅管理员可执行
- `pushMenu = true`：同步到 QQ 指令面板
- `unregisterBotCommand(key)` 用于移除运行时注册的命令

## 回复事件

```java
event.replyText("普通文本");
event.replyMarkdown("Markdown 内容");
event.replyMarkdown("Markdown 内容", keyboard);
```

## 注意事项

HuHoBot 使用 `server.getEventManager().fire(event).get()` 等待 Velocity 事件完成后读取取消状态。监听器中不要执行长时间阻塞操作；异步工作完成后，如需取消事件，应在事件 Future 完成前设置取消状态。
