# AI应用专区

# 云上OpenClaw(Clawdbot)快速接入企业微信应用指南
## 概述
本文主要介绍在UCloud轻量应用云主机中部署完成OpenClaw后如何配置接入企业微信应用（WeCom Agent）。

当前文档仅适配预装OpenClaw-2026.2.17及以上版本的应用镜像，您可以在UCloud控制台轻量应用云主机详情页进行版本确认。
![image](/images/appconf_os.png)


## 前置准备工作
在正式开始为OpenClaw(Clawdbot)配置接入企业微信应用之前，请您依次检查如下事项是否准备完成：
1. 您已经在本地电脑或者移动终端中安装了企业微信软件。
2. 您已经购买预装OpenClaw且镜像版本2026.2.17及以上版本的UCloud轻量应用云主机。

## 接入企业微信应用
### 新建企业微信应用
点击跳转并登录[企业微信管理后台](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fwork.weixin.qq.com%2Fwework_admin%2Fframe%23%2Fapps&objectId=2625147&objectType=1&contentType=rich)，进入应用管理 > 应用页面，在自建位置单击“创建应用”。依次设置应用Logo、应用名称、应用介绍（选填）、可见范围，设置完成后点击页面内的**创建应用**按钮。

## 为OpenClaw配置模型和通道
### 应用管理
选择相应的轻量应用云主机并进入详情页，点击**应用管理**即可对AIAgent进行配置。
![image](/images/appconf.png)

### 模型配置
为OpenClaw配置模型API Key，[UModelVerse](https://docs.ucloud.cn/modelverse/README) 旨在为客户提供快速搭建 AGI 应用的能力。仅需一个 API Key，即可轻松接入 OpenAI、Gemini 兼容的 API 接口，快速构建您的专属 AGI 应用，[ModelVerse 控制台](https://console.ucloud.cn/modelverse/experience/api-keys)

### 通道配置（配置飞书机器人App ID和App Secret）
1. 在应用管理的通道配置添加企业微信应用通道，此处需要配置五个参数。
    ![image](/images/qywxconf.png)

    **Corp ID**：在[企业微信管理后台](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fwork.weixin.qq.com%2Fwework_admin%2Fframe%23%2Fprofile&objectId=2625147&objectType=1&contentType=rich)中，找到“我的企业-企业信息”页面，在页面底部找到**企业ID**并且复制，将复制好的企业ID，粘贴至OpenClaw配置面板中的对应位置（Corp ID）输入框。

    **Corp Secret**：在[企业微信管理后台](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fwork.weixin.qq.com%2Fwework_admin%2Fframe%23%2Fprofile&objectId=2625147&objectType=1&contentType=rich)中，找到此前步骤新建的企业微信应用，单击进入应用详情。在应用详情页内，找到**Secret**，并点击查看按钮，在弹窗中点击**发送**。点击发送后，需要前往您的企业微信，此时会收到一条来自“企业微信团队”的消息，单击消息中的前往查看按钮，在弹窗内复制Secret。将复制好的Secret，粘贴至OpenClaw配置面板中的对应位置（Corp Secret）输入框中。

    **Agent ID**：在[企业微信管理后台](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fwork.weixin.qq.com%2Fwework_admin%2Fframe%23%2Fprofile&objectId=2625147&objectType=1&contentType=rich)中，找到此前步骤新建的企业微信应用，单击进入应用详情。在应用详情页内，找到**Agent ID**，复制并粘贴至OpenClaw配置面板中的对应位置（Agent ID）输入框中。

    **Token和EncodingAESKey**：在企业微信管理后台的应用管理详情页，找到“功能-接收消息”，点击**设置API接收**。此处暂时不填写URL，先随机获取Token和EncodingAESKey，然后将这两个参数分别填入OpenClaw配置面板的对应位置输入框中。
    ![image](/images/qywxconf2.png)
    ![image](/images/qywxconf3.png)

    五个参数均填写完成，等待片刻完成配置后，可以看到已接入通道中企业微信应用显示“运行中”状态。

2. 返回之前配置URL的应用管理页面，参考以下步骤来配置URL。

#### URL填写方式一：使用公网IP地址组成URL链接
首先回到OpenClaw**应用管理**页面，[防火墙放行18789端口](https://docs.ucloud.cn/ulhost/guide/openclaw_conf?id=%e9%98%b2%e7%81%ab%e5%a2%99%e6%94%be%e8%a1%8c%e7%ab%af%e5%8f%a3)，并生成管理员token，启用OpenClaw WebUI功能。
![image](/images/appconf_webui.png)

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

首先回到OpenClaw**应用管理**页面，[防火墙放行18789端口](https://docs.ucloud.cn/ulhost/guide/openclaw_conf?id=%e9%98%b2%e7%81%ab%e5%a2%99%e6%94%be%e8%a1%8c%e7%ab%af%e5%8f%a3)，并**生成管理员token**，启用OpenClaw WebUI功能。
![image](/images/appconf_webui.png)

将您的域名替换到下面的URL链接中，并且填入到企业微信管理页面的URL输入框中。
```Plain
http://您的域名:18789/wecom/bot
```
**注意**：URL需要使用http而非https，并使用英文冒号，并且加上端口号（默认为18789）和 /wecom/agent 。

### 配置企业可信IP
配置企业可信IP，这一步决定了您的企业微信应用是否能够接收到来自您部署的OpenClaw回复的信息。

同样需要进入前面创建的[企业微信应用管理](https://cloud.tencent.com/developer/tools/blog-entry?target=https%3A%2F%2Fwork.weixin.qq.com%2Fwework_admin%2Fframe%23%2Fapps&objectId=2625147&objectType=1&contentType=rich)详情页，在页面底部找到**企业可信IP**，并单击**配置**。
在配置企业可信IP的弹窗中，填入已部署OpenClaw的轻量应用服务器实例公网IP地址后，点击确定。

### 完成企业微信应用配置
配置完成后，您可以前往企业微信客户端软件的工作台，找到并点击之前步骤中创建的应用，然后就可以尝试与它进行对话。如果企业微信应用能够以AI的方式对话，则说明您已经成功完成OpenClaw接入企业微信应用。