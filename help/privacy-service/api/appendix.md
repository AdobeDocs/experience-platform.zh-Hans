---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Privacy ServiceAPI指南附录
description: 本文档包含有关使用Privacy ServiceAPI的其他信息。
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 7%

---

# Privacy ServiceAPI指南附录

以下部分包含有关使用Adobe Experience Platform Privacy Service API的其他信息。

## 标准身份命名空间 {#standard-namespaces}

发送到的所有身份 [!DNL Privacy Service] 必须在特定身份命名空间下提供。 身份命名空间是 [Adobe Experience Platform Identity Service](../../identity-service/home.md) 指示身份相关的上下文。

下表概述了提供的几种常用预定义身份类型 [!DNL Experience Platform]，及其关联的 `namespace` 值：

| 身份类型 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 电子邮件 | `Email` | `6` |
| Phone | `Phone` | `7` |
| Adobe Advertising Cloud ID | `AdCloud` | `411` |
| Adobe Audience Manager UUID | `CORE` | `0` |
| Adobe Experience Cloud ID | `ECID` | `4` |
| Adobe Target ID | `TNTID` | `9` |
| [!DNL Apple] 适用于广告商的ID | `IDFA` | `20915` |
| [!DNL Google] 广告 ID | `GAID` | `20914` |
| [!DNL Windows] AID | `WAID` | `8` |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>每个身份类型还具有 `namespaceId` 整数值，可用来代替 `namespace` 字符串 `type` 属性。 请参阅 [命名空间限定符](#namespace-qualifiers) 以了解更多信息。

您可以通过向 `idnamespace/identities` 的端点 [!DNL Identity Service] API。 请参阅 [Identity Service开发人员指南](../../identity-service/api/getting-started.md) 以了解更多信息。

## 命名空间限定符

指定 `namespace` 值 [!DNL Privacy Service] API， a **命名空间限定符** 必须包含在相应 `type` 参数。 下表概述了不同的已接受的命名空间限定符。

| 限定符 | 定义 |
| --------- | ---------- |
| `standard` | 全局定义的标准命名空间之一，不与单个组织数据集（例如，电子邮件、电话号码等）绑定。 提供了命名空间ID。 |
| `custom` | 在组织上下文中创建，且未在 [!DNL Experience Cloud]. 值表示要搜索的友好名称（“name”字段）。 提供了命名空间ID。 |
| `integrationCode` | 集成代码 — 与“自定义”类似，但明确定义为要搜索的数据源的集成代码。 提供了命名空间ID。 |
| `namespaceId` | 指示值是通过命名空间服务创建或映射的命名空间的实际ID。 |
| `unregistered` | 未在命名空间服务中定义且采用“原样”的自由格式字符串。 处理这些类型命名空间的任何应用程序都会针对它们进行检查，并在适当时处理公司上下文和数据集。 未提供命名空间ID。 |
| `analytics` | 在内部映射的自定义命名空间 [!DNL Analytics]，在命名空间服务中不能。 该ID将直接按照原始请求指定的方式传递，而不包含命名空间ID |
| `target` | 内部理解的自定义命名空间 [!DNL Target]，在命名空间服务中不能。 该ID将直接按照原始请求指定的方式传递，而不包含命名空间ID |

{style=&quot;table-layout:auto&quot;}

## 已接受的产品值

下表概述了在 `include` 作业创建请求的属性。

| 产品 | 在中使用的值 `include` 属性 |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform（数据湖） | `aepDataLake` |
| Adobe Experience Platform（实时客户资料） | `profileService` |
| Adobe Primetime身份验证 | `primetimeAuthentication` |
| Adobe Target | `target` |
| 客户属性(CRS) | `CRS` |
| Identity Service | `identity` |
| Marketo Engage | `marketo` |

{style=&quot;table-layout:auto&quot;}
