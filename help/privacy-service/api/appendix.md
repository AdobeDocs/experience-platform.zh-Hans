---
keywords: Experience Platform；首页；热门话题
solution: Experience Platform
title: Privacy Service API指南附录
description: 本文档包含有关使用Privacy Service API的其他信息。
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 9b3fb0d545408369d96a3fc7c5c6e9c098af9933
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 6%

---

# Privacy Service API指南附录

以下部分包含有关使用Adobe Experience Platform Privacy Service API的其他信息。

## 标准身份命名空间 {#standard-namespaces}

发送到[!DNL Privacy Service]的所有标识必须在特定的标识命名空间下提供。 身份命名空间是[Adobe Experience Platform Identity Service](../../identity-service/home.md)的组件，它指示与身份相关的上下文。

下表概述了[!DNL Experience Platform]提供的几种常用预定义标识类型及其关联的`namespace`值：

| 身份标识类型 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 电子邮件 | `Email` | `6` |
| 电话 | `Phone` | `7` |
| Adobe Advertising Cloud ID | `AdCloud` | `411` |
| ADOBE AUDIENCE MANAGER UUID | `CORE` | `0` |
| ADOBE EXPERIENCE CLOUD ID | `ECID` | `4` |
| ADOBE TARGET ID | `TNTID` | `9` |
| 广告商的[!DNL Apple] ID | `IDFA` | `20915` |
| [!DNL Google]广告ID | `GAID` | `20914` |
| [!DNL Windows]辅助 | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>每个标识类型还具有`namespaceId`整数值，在将该标识的`namespace`属性设置为“namespaceId”时，可以使用该整数值代替`type`字符串。 有关详细信息，请参阅有关[命名空间限定符](#namespace-qualifiers)的部分。

您可以通过向`idnamespace/identities` API中的[!DNL Identity Service]端点发出GET请求，检索您的组织正在使用的身份命名空间列表。 有关详细信息，请参阅[Identity Service开发人员指南](../../identity-service/api/getting-started.md)。

## 命名空间限定符 {#namespace-qualifiers}

在`namespace` API中指定[!DNL Privacy Service]值时，必须在相应的&#x200B;**参数中包含**&#x200B;命名空间限定符`type`。 下表概述了不同的已接受命名空间限定符。

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

## 接受的产品值 {#accepted-product-values}

此部分列出了创建Privacy Service作业（API或UI）时在`include`属性中接受的产品标识符值。 在作业请求的`include`数组中使用这些值。

下表列出了支持的产品、其UI显示名称及其相应的代码值。

>[!NOTE]
>
>- 产品值不区分大小写；为保持一致性，建议使用驼峰式大小写。
>- UI和API仅支持上面列出的产品。 如果没有为您的组织配置产品，则它可能会被忽略或导致验证错误 — 请参阅Adobe合同或配置文档以确认权利。

| 品牌产品名称 | UI显示名称 | `include` 值 |
| ------------------------------------------------------ | -------------------------- | ---------------------------------------- |
| Adobe Analytics | [!UICONTROL Analytics] | `analytics` |
| Adobe Audience Manager | [!UICONTROL Audience Manager] | `audienceManager` |
| Adobe Advertising | [!UICONTROL Ad Cloud] | `adCloud` |
| Adobe Experience Platform (Profile store) | [!UICONTROL Profile] | `profileService` |
| Adobe Experience Platform（数据湖） | [!UICONTROL AEP Data Lake] | `aepDataLake` |
| Adobe Campaign | [!UICONTROL Campaign] | `campaign` |
| Adobe Target | [!UICONTROL Target] | `target` |
| 客户属性 | [!UICONTROL Customer Attributes (CRS)] | `CRS` |
| Adobe Journey Optimizer | [!UICONTROL Adobe Journey Optimizer] | `cjm` |
| Marketo Engage | [!UICONTROL Marketo Engage / AJO B2B] | `marketo` |
| 身份标识服务 | [!UICONTROL Identity] | `identity` |
| Marketo Measure | [!UICONTROL Marketo Measure] | `marketomeasure` |
| Adobe Commerce | [!UICONTROL Commerce (Personalization)] | `commerceMarketingData` |

{style="table-layout:auto"}
