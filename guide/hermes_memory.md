# AI应用专区

# 云上Hermes记忆管理配置指南

## 概述

DBMemory智能记忆增强是Hermes镜像提供的高级记忆管理功能，通过绑定UCloud PostgreSQL数据库，为您的AI助手提供持久化、智能化的记忆能力。

启用记忆增强后，AI助手能够：
1. 持久化存储对话记忆，重启后依然保留
2. 智能检索历史记忆，提供更精准的上下文
3. 支持大规模记忆存储，突破本地存储限制

**适用镜像版本**：预装HermesAgent-2026.5.16及以上版本

**前置条件**：

!> - 需要创建UCloud PostgreSQL 15.7及以上版本实例
!> - PostgreSQL实例需与轻量应用云主机处于相同VPC
!> - 开启功能前请先联系技术支持开启PostgreSQL超级管理员权限，并确保该数据库正常运行

---

## 访问记忆管理

选择相应的轻量应用云主机并进入详情页，在顶部Tab栏点击**记忆管理**。

![image](/images/hermes_memory_entry.png)

进入记忆管理页面后，可以看到DBMemory智能记忆增强的配置入口，点击**立即启用**按钮开始配置。

---

## 配置流程

### 第一步：绑定数据库

在弹出的配置窗口中，第一步为绑定数据库：

![image](/images/hermes_memory_step1.png)

**配置项说明**：

| 配置项 | 说明 |
|--------|------|
| 绑定轻量主机 | 自动填充当前轻量应用云主机ID |
| 所属VPC | 自动填充当前VPC |
| 选择PostgreSQL实例 | 从下拉列表中选择已创建的PostgreSQL实例（仅显示运行中且版本≥15的实例） |
| 用户名 | 数据库登录用户名（如：root） |
| 登录密码 | 数据库登录密码 |

**操作步骤**：
1. 点击"选择PostgreSQL实例"下拉框，选择目标数据库
2. 输入数据库用户名
3. 输入数据库登录密码
4. 点击**下一步**按钮

### 第二步：LLM服务配置

数据库绑定完成后，进入第二步LLM服务配置：

![image](/images/hermes_memory_step2.png)

**配置项说明**：

| 配置项 | 说明 |
|--------|------|
| 模型 | 填写模型ID（如：gpt-4o-mini、gpt-4等） |
| API Key | 填写LLM服务的API Key |
| API Endpoint | 填写API端点地址，以http://或https://开头 |

**操作步骤**：
1. 输入模型ID
2. 输入API Key
3. 输入API Endpoint
4. 点击**确定**按钮

点击确定后，系统会在后台执行配置任务：

![image](/images/hermes_memory_configuring.png)

⚠️ **注意**：请耐心等待约30-60秒，不要关闭页面。配置完成后页面会自动更新状态。

---

## 配置完成

配置成功后，记忆管理页面将显示当前运行状态：

![image](/images/hermes_memory_done.png)

| 信息项 | 说明 |
|--------|------|
| 服务名称 | 记忆管理 |
| 更新时间 | 配置更新时间 |
| 状态 | 运行中 |

**绑定数据库信息**：

| 信息项 | 说明 |
|--------|------|
| 资源名称 | PostgreSQL实例内网IP |
| 端口 | 数据库端口（默认5432） |
| 用户名 | 数据库登录用户名 |

**LLM服务配置信息**：

| 信息项 | 说明 |
|--------|------|
| 接入方式 | 自定义 |
| API Key | 已配置的API Key（部分显示） |
| 模型 | 使用的模型ID |
| 模型Base URL | API端点地址 |

配置成功后，您可以：
- 点击**停止**暂停记忆管理服务
- 点击**重新配置**修改数据库或LLM配置

---

## 常见问题

### Q: PostgreSQL实例找不到？

A: 请确保：
1. PostgreSQL实例与轻量应用云主机在同一个项目下
2. PostgreSQL实例与轻量应用云主机在同一个VPC
3. PostgreSQL实例状态为运行中
4. PostgreSQL版本为15.7及以上

### Q: 绑定数据库失败？

A: 请检查：
1. 用户名和密码是否正确
2. 数据库是否允许当前VPC访问
3. 是否已联系技术支持开启PostgreSQL超级管理员权限
4. PostgreSQL版本是否为15.7及以上

### Q: LLM服务配置失败？

A: 请确认：
1. API Key有效且有余额
2. API Endpoint格式正确（以http://或https://开头）
3. 模型ID正确

### Q: 记忆增强启用后无效？

A: 请确认：
1. 数据库连接正常
2. LLM服务配置正确
3. API Key有效

---

## 相关文档

- [云上Hermes快速部署说明](/ulhost/guide/openclaw_conf)
- [云上Hermes快速接入企业微信智能机器人](/ulhost/guide/openclaw_wecom)
- [云上Hermes快速接入飞书](/ulhost/guide/openclaw_feishu)
- [UCloud PostgreSQL产品文档](/udb-pg/README)

---

**注意**：本文档中部分图片为示意图，实际界面以控制台为准。
