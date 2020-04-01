---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform查询服务疑难解答指南
topic: troubleshooting
translation-type: tm+mt
source-git-commit: c5bb112220b40fa6c2adfa89c80ddb87d382fbda

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
| **28P01** 开始-身份验证 | 密码无效 | 身份验证令牌无效 |
| **28000** 开始-身份验证 | 授权类型无效 | 授权类型无效。 一定是 `AuthenticationCleartextPassword`的。 |
| **42P12开始** -身份验证 | 找不到表 | 找不到要使用的表 |
| **小行星** 42601 | 语法错误 | 命令或语法错误无效 |
| **58000查询** | 系统错误 | 内部系统故障 |
| **42P01** 查询 | 找不到表 | 找不到在查询中指定的表 |
| **42P07** 查询 | 表存在 | 同名表已存在(CREATE TABLE) |
| **小行星** 53400 | LIMIT超出最大值 | 用户指定的LIMIT子句大于100,000 |
| **小行星** 53400 | 语句超时 | 提交的实时语句所花费的时间超过10分钟 |
| **08P01** N/A | 不支持的消息类型 | 不支持的消息类型 |
