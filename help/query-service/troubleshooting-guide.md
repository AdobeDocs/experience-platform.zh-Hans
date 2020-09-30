---
keywords: Experience Platform;home;popular topics;query service;Query service;troubleshooting guide;faq;troubleshooting;
solution: Experience Platform
title: Adobe Experience Platform查询服务疑难解答指南
topic: troubleshooting
description: 此文档包含有关您遇到的常见错误代码以及可能原因的信息。
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 2%

---


# 错误和疑难解答

## REST API错误

| HTTP状态代码 | 描述 | 可能的原因 |
| ---------------- | ----------- | --------------- |
| 400 | 错误请求 | 格式错误或非法查询 |
| 401 | 身份验证失败 | 身份验证令牌无效 |
| 500 | 内部服务器错误 | 内部系统故障 |

## PostgreSQL API错误

| 错误代码和连接状态 | 描述 | 可能的原因 |
| ------------------------------- | ----------- | -------------- |
| **28P01开始** -身份验证 | 密码无效 | 身份验证令牌无效 |
| **28000** 开始-身份验证 | 授权类型无效 | 授权类型无效。 一定是 `AuthenticationCleartextPassword`的。 |
| **42P12开始** -身份验证 | 找不到表 | 找不到要使用的表 |
| **42601** 查询 | 语法错误 | 命令或语法错误无效 |
| **58000** 查询 | 系统错误 | 内部系统故障 |
| **42P01** 查询 | 找不到表 | 找不到在查询中指定的表 |
| **42P07** 查询 | 表存在 | 同名表已存在(CREATE TABLE) |
| **53400** 查询 | LIMIT超出最大值 | 用户指定的LIMIT子句大于100,000 |
| **53400** 查询 | 语句超时 | 提交的实时语句所花的时间超过最长10分钟 |
| **08P01** N/A | 不支持的消息类型 | 不支持的消息类型 |
