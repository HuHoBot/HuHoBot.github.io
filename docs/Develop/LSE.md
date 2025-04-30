# HuHoBot 自定义LSE附属插件

### 您可以按如下代码创建一个插件，编写一个HuHoBot拓展模块，并使用HuHoBot的API注册回调函数

```javascript
const HUHONAMESPACE = 'HuHo_Bot' //勿动
const NAMESPACE = 'Test' //修改成你自己想要的Namespace

/**
 * 回调函数
 * @param {array} keyWord
 */

function Callback(params){ 
    return "测试成功" //可以返回一个文本消息到群内
    return JSON.stringify({
        "text": `测试成功`,
        "imgUrl":qlogoUrl}
    ) //可以返回一个带图片的文本消息到群内(不发图请留空)
}

/**
 * 注册回调函数
 * @param {string} keyWord
 * @param {function} func
 */

function regCallbackEvent(type,keyWord,func){
    if(!ll.hasExported(HUHONAMESPACE,'regEvent')){
        return;
    }
    let regEvent = ll.imports(HUHONAMESPACE,'regEvent')
    ll.exports(func,NAMESPACE,func.name)
    regEvent(type,keyWord,NAMESPACE,func.name)
}

mc.listen("onServerStarted",()=>{
    let keyWord = "测试" //触发关键词
    regCallbackEvent("run",keyWord,Callback)
})
```

### 附录：事件数据结构说明

在 `BotCustomCommand` 事件中，`event.data` 包含以下 JSON 数据结构：

```json 
{
  "key": "关键字",
  "runParams": [
    "参数1",
    "参数2"
  ],
  "author": {
    "qlogoUrl": "用户头像URL",
    "bindNick": "绑定昵称",
    "openId": "用户OpenID"
  },
  "group": {
    "openId": "群组OpenID"
  }
}
```

- **key**: 触发命令的关键词。
- **runParams**: 命令执行时传递的参数列表。
- **author**: 发送命令的用户信息。
    - **qlogoUrl**: 用户头像 URL。
    - **bindNick**: 用户绑定的昵称。
    - **openId**: 用户的 OpenID。
- **group**: 群组信息。
    - **openId**: 群组的 OpenID。

### 附录：返回自定义响应

如果需要返回复杂的 JSON 结构，返回一个`格式化后的Json字符串`：

```javascript
return JSON.stringify({
    "text": `测试成功`,
    "imgUrl":qlogoUrl
});
```

responseJson示例：

```json
{
  "text": "这是返回的文本消息",
  //可留空
  "imgUrl": "https://example.com/image.jpg"
  //可留空
}
```

### 致谢
希望这份文档能帮助你更好地理解和开发 `HuHoBot附属插件`！