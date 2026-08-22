# HuHoBot Penguin 部署与配置教程

在使用 HuHoBot 前，需要完成 QQ 开放平台机器人的创建与申请：

1. 访问 [QQ 开放平台官网](https://q.qq.com)
2. 登录并创建/申请一个机器人。
3. 在配置时，连接方式请选择 **“其他方式连接”**。
4. 记录 Bot 的 `app-id` 与 `secret` 密钥，供后续配置使用。

## 配置设置
打开插件/程序的配置文件，按照如下结构配置 Bot 基础信息并绑定群聊。

### Bot 基础信息与群聊绑定
```yaml
bot:
  id: "_AppID"
  secret: "Your_Secret"
  name: HuHoBot
  groups:
    - "66535AF0D529..."
    - "DFD5BB8CBA5C..."

  chat-format:
    from: '[Game] <{name}> {}'
    from-group: '[QQ {name}]: {message}'
```
**配置要点说明：**

- **群号填写：** 在群聊中发送相关指令（如 `查信息`）获取当前群的真实群标识码，并将获取到的群号依次填入 `groups` 表中。
- **群号规范：** 填入 `groups` 列表中的群号时，务必加上双引号（例如：`"66535AF0D529..."`）。
- **消息互通格式：** `chat-format` 可自定义游戏端与 QQ 群聊端的消息转发格式，支持 `{name}` 与 `{message}` 变量。

## 新版 MOTD API 与在线查询配置

### MOTD API 启用配置
若要启用服务器状态及 MOTD 展示，需要在配置中定位到 `motd` 字段下的 `api` 项，并将其值换为标准 API 接口：

```yaml
motd:
  api: "http://motd.txssb.cn/api/app_img?ip={ip}&port={port}&dark=true&lang=zh-CN"
```

**参数与规则说明：**

- **保留占位符**：URL 中的 `{ip}` 和 `{port}` 必须保持原样，**不可变动**。
- **主题配色调节：**
  - `dark`：深色模式。
  - `dark=false`：浅色。

**详细文档与调试**：参考[官方文档](https://motd.txssb.cn/docs)，或使用其提供的在线测试器测试对应的 URL。
- **兼容性限制：** 暂不支持 **Simpfun (简幻欢)** 节点的状态查询。

### 在线查询 Markdown 权限说明
- 使用 `查在线` 时，请务必在配置中将 `use-markdown` 设置为 `true`，否则无法正常发送信息。
