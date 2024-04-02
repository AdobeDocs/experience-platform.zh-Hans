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
ht-degree: 6%

---

# Privacy ServiceAPI指南附录

以下部分包含有关使用Adobe Experience Platform Privacy Service API的其他信息。

## 标准身份命名空间 {#standard-namespaces}

所有发送到的身份 [!DNL Privacy Service] 必须在特定的身份命名空间下提供。 身份命名空间是的组件 [Adobe Experience Platform Identity服务](../../identity-service/home.md) 指示与身份相关的上下文。

下表概述了由提供的几种常用的预定义身份类型 [!DNL Experience Platform]，以及与其关联的 `namespace` 值：

| 标识类型 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 电子邮件 | `Email` | `6` |
| 电话 | `Phone` | `7` |
| ADOBE ADVERTISING CLOUD ID | `AdCloud` | `411` |
| ADOBE AUDIENCE MANAGER UUID | `CORE` | `0` |
| Adobe Experience Cloud ID | `ECID` | `4` |
| ADOBE TARGET ID | `TNTID` | `9` |
| [!DNL Apple] 广告商的ID | `IDFA` | `20915` |
| [!DNL Google] 广告ID | `GAID` | `20914` |
| [!DNL Windows] AID | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>每个标识类型还具有 `namespaceId` 整数值，可用于代替 `namespace` 设置标识时的字符串 `type` 属性到“namespaceId”。 请参阅以下部分 [命名空间限定符](#namespace-qualifiers) 以了解更多信息。

您可以通过向以下网站发出GET请求，检索贵组织正在使用的身份命名空间列表： `idnamespace/identities` 中的端点 [!DNL Identity Service] API。 请参阅 [Identity Service开发人员指南](../../identity-service/api/getting-started.md) 以了解更多信息。

## 命名空间限定符

指定 `namespace` 中的值 [!DNL Privacy Service] API， a **命名空间限定符** 必须包含在相应的 `type` 参数。 下表概述了不同的已接受命名空间限定符。

| 限定符 | 定义 |
| --------- | ---------- |
| `standard` | 全局定义的标准命名空间之一，不绑定到单个组织数据集（例如，电子邮件、电话号码等）。 提供了命名空间ID。 |
| `custom` | 在组织上下文中创建的唯一命名空间，未在之间共享 [!DNL Experience Cloud]. 值表示要搜索的友好名称（“name”字段）。 提供了命名空间ID。 |
| `integrationCode` | 集成代码 — 类似于“自定义”，但特别定义为要搜索的数据源的集成代码。 提供了命名空间ID。 |
| `namespaceId` | 指示该值是通过命名空间服务创建或映射的命名空间的实际ID。 |
| `unregistered` | 一个自由格式字符串，未在命名空间服务中定义并“按原样”使用。 任何处理此类命名空间的应用程序都会针对此类命名空间进行检查，并在适合公司上下文和数据集时进行处理。 未提供命名空间ID。 |
| `analytics` | 内部映射的自定义命名空间 [!DNL Analytics]，不在命名空间服务中。 它是按照原始请求指定的方式直接传入的，没有命名空间ID |
| `target` | 内部可理解的自定义命名空间 [!DNL Target]，不在命名空间服务中。 它是按照原始请求指定的方式直接传入的，没有命名空间ID |

{style="table-layout:auto"}

## 接受的产品值

下表概述了在中指定Adobe产品的接受值 `include` 作业创建请求的属性。

>[!NOTE]
>
>产品列表的值不区分大小写。 建议使用驼峰式大小写，但不强制使用。

| 产品 | 在中使用的值 `include` 属性 |
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
