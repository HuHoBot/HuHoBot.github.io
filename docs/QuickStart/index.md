# 快速开始

## 1. 安装插件
- Java类 核心:
    - 将下载好的`HuHoBot-XX-X.X.X.jar`加入`plugins`目录下
    - 启动服务器

- LSE:
    - 将下载好的`HuHoBot-BDS-vX.X.X.zip`解压出`HuHo_Bot`文件夹后拖入`plugins`目录下
    - 启动服务器

- EndStone:
    - 将下载好的`endstone_huhobot_vX.X.X.dll`加入`plugins`目录下
    - 启动服务器

- 第三方: 请根据插件文档说明安装

## 2. 配置插件
- 配置插件的配置文件`config.yml`或`config.json`，具体配置方法请参考对应的[适配器文档](../Adapter/index.md)。

## 3. 添加机器人
- [加入交流群](http://qm.qq.com/cgi-bin/qm/qr?_wv=1027&k=N6tVRxGR8sDwYHBx9YgAhkqRTp1gseyk&authKey=M7Fd3Op6nHjXjSXefBtHBPqIq2wtX8AfufZor9DrfRrJkhyS2rohkt7iuOSwbtn8&noverify=0&group_code=1005746321) 点击HuHo_Bot头像并添加到群聊

## 4. 完成绑定

- 请在控制台输出中找到这一条内容
    ```bash
    [HuHoBot] 服务器尚未在机器人进行绑定，请在群内输入"/绑定 xxxxxxxxxxxxxxxxxxxxxxx"
    ```

- 在`你要绑定的群内`输入以下对话
    ```bash
    @HuHoBot /绑定 xxxxxxxxxxxxxxxxxxxxxxx
    ```

    如图:

    ![BindExample](BindExample.png)

- 输入绑定码

    - 在控制台中会找到这样一条内容
        ```bash
        [HuHoBot] 收到一个新的绑定请求，如确认绑定，请输入"/huhobot bind xxxx"来进行确认
        ```
    
    - 在控制台输入
        ```bash
        huhobot bind xxxx
        ```

    - 成功绑定
        - 当机器人弹出这个消息时代表成功绑定
            ![BindSuccess](BindSuccess.png)

        - 同时控制台会重新连接并提示
            ```bash
            [HuHoBot] 与服务端握手成功.
            ```

    - 添加别的管理员: 请参照[管理员帮助](../AdminHelp/index.md)


