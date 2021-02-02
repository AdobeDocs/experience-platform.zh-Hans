---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Privacy ServiceAPI开发人员指南附录
topic: developer guide
description: 此文档包含有关使用Privacy ServiceAPI的其他信息。
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 9%

---


# 附录

以下各节包含有关使用Adobe Experience Platform Privacy ServiceAPI的其他信息。

## 标准标识命名空间{#standard-namespaces}

发送到[!DNL Privacy Service]的所有身份必须在特定身份命名空间下提供。 身份命名空间是[Adobe Experience Platform身份服务](../../identity-service/home.md)的一个组件，用于指示与身份相关的上下文。

下表概述了[!DNL Experience Platform]提供的几种常用预定义身份类型及其关联的`namespace`值：

| 身份类型 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 电子邮件 | 电子邮件 | 6 |
| Phone | 电话 | 7 |
| Adobe Advertising CloudID | AdCloud | 411 |
| Adobe Audience ManagerUUID | CORE | 0 |
| Adobe Experience CloudID | ECID | 4 |
| Adobe TargetID | TNTID | 9 |
| [!DNL Apple] 广告商的ID | IDFA | 20915 |
| [!DNL Google] 广告 ID | GAID | 20914 |
| [!DNL Windows] AID | WAID | 8 |

>[!NOTE]
>
>每个标识类型还有一个`namespaceId`整数值，当将标识的`type`属性设置为“namespaceId”时，可以使用该值代替`namespace`字符串。 有关详细信息，请参阅[命名空间限定符](#namespace-qualifiers)一节。

通过向[!DNL Identity Service] API中的`idnamespace/identities`端点发出GET请求，可以检索您的组织正在使用的列表身份命名空间。 有关详细信息，请参阅[Identity Service开发人员指南](../../identity-service/api/getting-started.md)。

## 命名空间限定符

当在[!DNL Privacy Service] API中指定`namespace`值时，必须在相应的`type`参数中包含&#x200B;**命名空间限定符**。 下表概述了不同的已接受命名空间限定符。

| 限定符 | 定义 |
| --------- | ---------- |
| 标准 | 全球定义的标准命名空间之一，不与单个组织数据集（例如，电子邮件、电话号码等）关联。 命名空间ID已提供。 |
| 自定义 | 在组织上下文中创建的唯一命名空间，不在[!DNL Experience Cloud]中共享。 该值表示要搜索的友好名称（“名称”字段）。 命名空间ID已提供。 |
| integrationCode | 集成代码——与“自定义”类似，但明确定义为要搜索的数据源的集成代码。 命名空间ID已提供。 |
| namespaceId | 指示该值是通过命名空间服务创建或映射的命名空间的实际ID。 |
| 未注册 | 未在命名空间服务中定义且采用“原样”的自由形式字符串。 处理这些命名空间的任何应用程序都会针对它们进行检查，并根据公司上下文和数据集进行处理。 未提供命名空间ID。 |
| analytics | 在[!DNL Analytics]内部映射的自定义命名空间，而不是在命名空间服务中。 它直接按原始请求指定的方式传递，没有命名空间ID |
| Target | [!DNL Target]在内部理解的自定义命名空间，而不是命名空间服务中。 它直接按原始请求指定的方式传递，没有命名空间ID |

## 接受的产品值

下表概述了在作业创建请求的`include`属性中指定Adobe产品的已接受值。

| 产品 | 用于`include`属性的值 |
--- | ---
| Adobe Advertising Cloud | &quot;AdCloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | “AudienceManager” |
| Adobe Campaign | &quot;Campaign&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Adobe Primetime认证 | “primetime身份验证” |
| Adobe Target | &quot;Target&quot; |
| 客户记录服务 | &quot;CRS&quot; |
| 实时客户资料 | &quot;ProfileService&quot; |