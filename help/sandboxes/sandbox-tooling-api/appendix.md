---
title: 沙盒工具API指南附录
description: 本文档提供有关使用沙盒工具API的补充信息。
exl-id: fdfa019d-ce0e-456b-b591-7d96d1115e02
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---

# 沙盒API指南附录

本文档提供有关使用[!DNL Sandbox] API的补充信息。

## 使用查询参数 {#query}

沙盒工具API支持在列出包时使用查询参数来分页和筛选结果。

>[!NOTE]
>
>可以单独传递和启动`limit`。

| 参数 | 描述 |
| --- | --- |
| `limit` | 响应中返回的最大记录数。 默认限制为20。 |
| `start` | 子设置的项目列表应从何处开始的开始。 |
| `targetSandbox` | 表示您要将工件导入到的沙盒名称。 |
| `jobType` | 作业类型。 此值可以是NEW、RESUME和ROLLBACK。 |
| `jobStatus` | 作业的状态。 此值可以是PENDING、IN_PROGRESS、SUCCESS、FAILED和CANCELED。 |
| `requestType` | 请求的类型。 此值可以是EXPORT、IMPORT和COPY。 |
| `expiryPeriod ` | 此用户指定的时间段定义从包发布之时起的包到期日期（以天为单位）。 该值不应为负。 默认值为调用更新或发布API后的90天。 |
