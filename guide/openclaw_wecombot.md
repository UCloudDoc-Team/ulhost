# AI应用专区

# 云上OpenClaw(Clawdbot)快速接入企业微信指南
## 概述
本文主要介绍在UCloud轻量应用云主机中部署完成OpenClaw后如何配置接入企业微信（WeCom）。

当前文档仅适配镜像版本2026.2.17及以上版本，您可以在UCloud控制台轻量应用云主机详情页进行版本确认。


## 前置准备工作
在正式开始为OpenClaw(Clawdbot)配置接入企业微信机器人之前，请您依次检查如下事项是否准备完成：
1. 您已经在本地电脑或者移动终端中安装了企业微信软件。
2. 您已经购买预装OpenClaw且镜像版本2026.2.17及以上版本的UCloud轻量应用云主机。

## 接入企业微信机器人

### 新建企业微信机器人
1. 前往[企业微信官网](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fwork.weixin.qq.com%2F&objectId=2625147&objectType=1&contentType=rich)，使用有企业管理员权限的账号登录。如您尚未在企业微信中拥有企业，可以参考[创建&注册企业](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fopen.work.weixin.qq.com%2Fwwopen%2Fmanual%2Fdetail%3Ft%3Dregister&objectId=2625147&objectType=1&contentType=rich)来创建一个新企业。


2. 在企业微信管理后台左侧导航依次找到并进入**安全与管理** > **管理工具**，选择**智能机器人**，然后在页面内点击**创建机器人**，滑到页面最底端，点击**API模式创建**按钮。

3. 依次填写名称、简介、可见范围、URL（参考后续步骤），并且点击随机获取按钮生成Token和Encoding-AESKey（这是企业微信与OpenClaw进行加密通信的密钥）。
**注意**：此处先不用点击“创建”按钮，URL填写完成，点击随机获取Token、Encoding-AESKey后，先不要点击页面下方的“创建”按钮，而是需要先前往轻量应用云主机控制台页面，参考接下来的“配置模型和通道”步骤进行操作，完成后再返回企业微信机器人配置页面点击创建。否则，会报错提示“服务没有正确响应，请确认后重试”。

#### URL填写方式一：使用公网IP地址组成URL链接
复制部署了OpenClaw的轻量应用云主机的公网IP地址，替换到下面的URL链接中，然后填入到企业微信管理页面的URL输入框中。
```Plain
http://轻量应用云主机的公网IP地址:18789/wecom/bot
```
**注意**：URL需要使用http而非https，并使用英文冒号，并且加上端口号（默认为18789）和 /wecom/agent 。
#### URL填写方式二：使用已备案域名组成URL链接
**前置要求**：
1. 您的企业微信已经进行了企业认证，则在创建机器人配置URL时，必须要配置已经完成备案的域名，并且域名的备案主体需要和企业微信认证企业一致或者有关联关系，否则会提示”域名主体校验未通过，需配置备案主题与当前企业主体相同或有关联关系的域名”。
2. 您已经拥有一个满足企业微信要求的已备案域名（域名备案主体和认证企业一致），并且您的域名已经DNS解析到部署了OpenClaw的轻量应用云主机实例公网IP。
**URL配置**：
将您的域名替换到下面的URL链接中，并且填入到企业微信管理页面的URL输入框中。
```Plain
http://您的域名:18789/wecom/bot
```
**注意**：URL需要使用http而非https，并使用英文冒号，并且加上端口号（默认为18789）和 /wecom/agent 。


## 为OpenClaw配置模型和通道
### 应用管理
选择相应的轻量应用云主机并进入详情页，点击**应用管理**即可对AIAgent进行配置。
![image](/images/appconf.png)

### 模型配置
为OpenClaw配置模型API Key，[UModelVerse](https://docs.ucloud.cn/modelverse/README) 旨在为客户提供快速搭建 AGI 应用的能力。仅需一个 API Key，即可轻松接入 OpenAI、Gemini 兼容的 API 接口，快速构建您的专属 AGI 应用，[ModelVerse 控制台](https://console.ucloud.cn/modelverse/experience/api-keys)

### 通道配置（配置企业微信机器人Token 和 EncodingAESKey）
1. 在应用管理的通道配置输入框中，输入此前创建企业微信机器人时随机生成的 Token 和 EncodingAESKey 。
2. 点击应用并确认操作，等待几十秒完成配置；
3. 等待几十秒后查看状态，确保你的钉钉通道显示**运行中**。

### 完成企业微信机器人配置
1. 此时您需要再回到企业微信机器人创建页面，点击创建按钮。
2. 创建成功后，在机器人详情页面中，点击“…”按钮，再点击获取机器人二维码，通过移动端企业微信扫码后添加该机器人。
3. 添加完成后，无需配对即可在企业微信聊天窗中与机器人直接进行聊天。如果企业微信机器人能够以AI的方式对话，则说明您已经成功完成OpenClaw应用接入企业微信机器人。

