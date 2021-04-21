---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；疑难解答指南；常见问题解答；疑难解答；
solution: Experience Platform
title: 查询服务疑难解答指南
topic-legacy: troubleshooting
description: 此文档包含有关您遇到的常见错误代码以及可能原因的信息。
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 3%

---

# [!DNL Query Service] 疑难解答指南

## REST API错误

| HTTP状态代码 | 描述 | 可能的原因 |
| ---------------- | ----------- | --------------- |
| 400 | 错误请求 | 格式错误或非法查询 |
| 401 | 身份验证失败 | 身份验证令牌无效 |
| 500 | 内部服务器错误 | 内部系统故障 |

## PostgreSQL API错误

| 错误代码和连接状态 | 描述 | 可能的原因 |
| ------------------------------- | ----------- | -------------- |
| **28P01** 开始 — 身份验证 | 密码无效 | 身份验证令牌无效 |
| **28000** 开始 — 身份验证 | 授权类型无效 | 授权类型无效。 必须为`AuthenticationCleartextPassword`。 |
| **42P12** 开始 — 身份验证 | 找不到表 | 未找到要使用的表 |
| **42601** 查询 | 语法错误 | 命令或语法错误无效 |
| **58000** 查询 | 系统错误 | 内部系统故障 |
| **42P01** 查询 | 找不到表 | 找不到在查询中指定的表 |
| **42P07** 查询 | 表存在 | 具有相同名称的表已存在(CREATE TABLE) |
| **53400** 查询 | LIMIT超过最大值 | 用户指定的LIMIT子句大于100,000 |
| **53400** 查询 | 语句超时 | 提交的实时语句最长需要10分钟 |
| **08P01** N/A | 不支持的消息类型 | 不支持的消息类型 |
