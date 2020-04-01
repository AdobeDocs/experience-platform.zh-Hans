---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 接受的身份命名空间和限定符
topic: developer guide
translation-type: tm+mt
source-git-commit: d0fcae6b1b75584a2c26d6eee5b47e0d60a142ba

---


# 附录

## 标准标识命名空间

发送到隐私服务的所有身份必须根据特定身份命名空间提供。 标识命名空间是 [Adobe Experience Platform Identity Service的一个组件](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_services_architectural_overview/identity_services_architectural_overview.md) ，用于指示标识与之相关的上下文。

下表概述了Experience Platform提供的几种常用预定义标识类型及其关联 `namespace` 值：

| 身份类型 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 电子邮件 | 电子邮件 | 6 |
| Phone | Phone | 7 |
| Adobe Advertising Cloud ID | AdCloud | 411 |
| Adobe受众管理器UUID | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe目标ID | TNTID | 9 |
| 面向广告商的Apple ID | IDFA | 20915 |
| Google广告ID | GAID | 20914 |
| Windows AID | WAID | 8 |

>[!NOTE] 每个标识类型还有一个整 `namespaceId` 数值，当将标识的属性设置为“namespaceId”时，可以使用该整 `namespace``type` 数值代替字符串。 有关详细信息，请参 [阅命名空间限定](#namespace-qualifiers) 符一节。

您可以通过向Identity Service API中的端点发出GET请求，检索您的组 `idnamespace/identities` 织正在使用的标识命名空间。 有关详细 [信息，请参阅Identity Service开发人员指南](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_services_architectural_overview/identity_services_api.md) 。

## 命名空间限定词

在隐私 `namespace` 服务API中指定值时，命名空间限 **定符必须包含在相应的参**`type` 数中。 下表概述了不同的已接受命名空间限定符。

| 限定符 | 定义 |
| --------- | ---------- |
| 标准 | 全球定义的标准命名空间之一，不绑定到单个组织数据集（例如，电子邮件、电话号码等）。 提供命名空间ID。 |
| 自定义 | 在组织上下文中创建的唯一命名空间，未在Experience Cloud中共享。 该值表示要搜索的友好名称（“名称”字段）。 提供命名空间ID。 |
| integrationCode | 集成代码——与“自定义”类似，但明确定义为要搜索的数据源的集成代码。 提供命名空间ID。 |
| namespaceId | 指示该值是通过命名空间服务创建或映射的命名空间的实际ID。 |
| 未注册 | 未在命名空间服务中定义且采用“原样”的自由格式字符串。 处理这些命名空间的任何应用程序都会针对它们进行检查，并在适合公司上下文和数据集时进行处理。 不提供命名空间ID。 |
| analytics | 自定义命名空间，它在Analytics中内部映射，而不是在命名空间服务中映射。 这是按原始请求指定的直接传递的，没有命名空间ID |
| Target | 自定义命名空间由目标内部理解，而不是在命名空间服务中。 这是按原始请求指定的直接传递的，没有命名空间ID |

## 接受的产品值

下表概述了在作业创建请求的属性中指定Adobe `include` 产品的已接受值。

| 产品 | 在属性中使用的 `include` 值 |
--- | ---
| Adobe Advertising Cloud | &quot;AdCloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | “AudienceManager” |
| Adobe Campaign | &quot;Campaign&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Adobe Primetime身份验证 | “primetimeAuthentication” |
| Adobe Target | &quot;Target&quot; |
| 客户记录服务 | “CRS” |
| 实时客户资料 | “ProfileService” |