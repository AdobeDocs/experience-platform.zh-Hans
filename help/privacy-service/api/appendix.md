---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Privacy ServiceAPI指南附录
description: 本文档包含有关使用Privacy ServiceAPI的其他信息。
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 644e85fe5c9b1a37f69c75755713e929736c2e89
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 5%

---

# Privacy ServiceAPI指南附录

以下部分包含有关使用Adobe Experience Platform Privacy Service API的其他信息。

## 标准身份命名空间 {#standard-namespaces}

发送到[!DNL Privacy Service]的所有标识必须在特定的标识命名空间下提供。 身份命名空间是[Adobe Experience Platform Identity Service](../../identity-service/home.md)的组件，它指示与身份相关的上下文。

下表概述了[!DNL Experience Platform]提供的几种常用预定义标识类型及其关联的`namespace`值：

| 标识类型 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 电子邮件 | `Email` | `6` |
| 电话 | `Phone` | `7` |
| ADOBE ADVERTISING CLOUD ID | `AdCloud` | `411` |
| ADOBE AUDIENCE MANAGER UUID | `CORE` | `0` |
| ADOBE EXPERIENCE CLOUD ID | `ECID` | `4` |
| ADOBE TARGET ID | `TNTID` | `9` |
| 广告商的[!DNL Apple] ID | `IDFA` | `20915` |
| [!DNL Google]广告ID | `GAID` | `20914` |
| [!DNL Windows]辅助 | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>每个标识类型还具有`namespaceId`整数值，在将该标识的`type`属性设置为“namespaceId”时，可以使用该整数值代替`namespace`字符串。 有关详细信息，请参阅有关[命名空间限定符](#namespace-qualifiers)的部分。

您可以通过向[!DNL Identity Service] API中的`idnamespace/identities`端点发出GET请求来检索您的组织正在使用的身份命名空间列表。 有关详细信息，请参阅[Identity Service开发人员指南](../../identity-service/api/getting-started.md)。

## 命名空间限定符

在[!DNL Privacy Service] API中指定`namespace`值时，必须在相应的`type`参数中包含&#x200B;**命名空间限定符**。 下表概述了不同的已接受命名空间限定符。

| 限定符 | 定义 |
| --------- | ---------- |
| `standard` | 全局定义的标准命名空间之一，不绑定到单个组织数据集（例如，电子邮件、电话号码等）。 提供了命名空间ID。 |
| `custom` | 在组织上下文中创建的唯一命名空间，未在[!DNL Experience Cloud]之间共享。 值表示要搜索的友好名称（“name”字段）。 提供了命名空间ID。 |
| `integrationCode` | 集成代码 — 类似于“自定义”，但特别定义为要搜索的数据源的集成代码。 提供了命名空间ID。 |
| `namespaceId` | 指示该值是通过命名空间服务创建或映射的命名空间的实际ID。 |
| `unregistered` | 一个自由格式字符串，未在命名空间服务中定义并“按原样”使用。 任何处理此类命名空间的应用程序都会针对此类命名空间进行检查，并在适合公司上下文和数据集时进行处理。 未提供命名空间ID。 |
| `analytics` | 自定义命名空间在[!DNL Analytics]中内部映射，而不是在命名空间服务中映射。 它是按照原始请求指定的方式直接传入的，没有命名空间ID |
| `target` | [!DNL Target]内部理解的自定义命名空间，而不是命名空间服务中的自定义命名空间。 它是按照原始请求指定的方式直接传入的，没有命名空间ID |

{style="table-layout:auto"}

## 接受的产品值

下表概述了在作业创建请求的`include`属性中指定Adobe产品时接受的值。

>[!NOTE]
>
>产品列表的值不区分大小写。 建议使用驼峰式大小写，但不强制使用。

| 产品 | 在`include`属性中使用的值 |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `audienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform（数据湖） | `aepDataLake` |
| Adobe Experience Platform （实时客户资料） | `profileService` |
| Adobe Pass 身份验证 | `primetimeAuthentication` |
| Adobe Target | `target` |
| 客户属性(CRS) | `CRS` |
| 客户历程管理 | `cjm` |
| 身份服务 | `identity` |
| Marketo Engage | `marketo` |
| Marketo Measure | `marketomeasure` |

{style="table-layout:auto"}
