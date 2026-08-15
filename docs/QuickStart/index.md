# HuHoBot Penguin 部署与配置教程

在使用`HuHoBot` ，需要完成 QQ 开放平台机器人的创建与申请：

1. 访问 [QQ 开放平台官网](https://q.qq.com)
2. 登录并创建/申请一个机器人。
3. 在入配置时，连接方式请选择 **“其他方式连接”**。
4. 记录Bot的 `app-id` 与 `secret` 密钥备后续配置使用。

## 配置设置
打开插件/程序的配置文件，按照如下结构基础与群绑定。

 Bot 基础与群聊绑定
```yaml
bot:
 -id "_AppID"
  secret: "Your_Secret"
  name: HuHoBot
  groups:
    - "66535AF0D529..."
    - "DFD5BB8CBA5C..."

  chat-format:
    from: '[Game] <{name}> {}'
    from-group: '[QQ {name}: {message}'
```
**配置要点说明：**

- **群号与填入：** 在群聊中发送相关令（如 `查信息`）获取当前群的真实群标识码，并将到的群号依次填入 `groups`表下。
- **号规范：** 填入 `groups` 列表下的群号 **务必记得加上双引号**（例如66535..."`）。
- **消息互通格式：** `chat-format` 可自定义游戏端与 QQ 群聊端的消息转发格式，支持 `{name}` 与 `{message}`变量## 新版 Motd API 与在线查询配置

### Mot API 启用配置
若要启用状态及 Mot 展示，需要在配置中定位到 `motd` 字段下的 `api` 项，并将其值换为标准 API 接口：

```yaml
motd:
  api: "http://motd.txssb.cn/api/app_img?ip={ip}&port={port}&dark=true&lang=zh-CN"
```

**参数与规则说明：**

- **留占位符**：URL 中的`{ip}` 和 `{port}` 必须保持原样， **不可变动**。
- **主题配色调节：**
  - `dark`：深色模式。
  - `dark=false`：浅色。

**详细文档与调试**：参考[官方文档](https://motd.txssb.cn/docs) 或使用其提供的测试器在线对应的 URL。
- **兼容性限制：** 暂不支持 **Simpfun (简幻欢)** 节点的状态查询。

### 在线查询 Markdown 权说明
- 使用`查在线`时，请务必在中将 `use-markdown` 设置为 `true` 开，否则**无法正常发送信息**
