---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 接受的身份命名空间和限定符
topic: developer guide
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 10%

---


# 附录

## 标准身份命名空间 {#standard-namespaces}

发送到的所有身份 [!DNL Privacy Service] 必须在特定身份命名空间下提供。 Identity namespaces are a component of [Adobe Experience Platform Identity Service](../../identity-service/home.md) that indicate the context to which an identity relates.

下表概述了几种常用的预定义身份类型及其 [!DNL Experience Platform]关联值的可 `namespace` 用性：

| 身份类型 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 电子邮件 | 电子邮件 | 6 |
| Phone | Phone | 7 |
| Adobe Advertising CloudID | AdCloud | 411 |
| Adobe Audience ManagerUUID | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe TargetID | TNTID | 9 |
| [!DNL Apple] 广告商的ID | IDFA | 20915 |
| [!DNL Google] 广告 ID | GAID | 20914 |
| [!DNL Windows] AID | WAID | 8 |

>[!NOTE]
>
>每个标识类型还有 `namespaceId` 一个整数值，在将标识的属性设置为 `namespace` “namespaceId”时，可以使用 `type` 它代替字符串。 有关详细信息，请参 [阅命名空间限](#namespace-qualifiers) 定符一节。

您可以通过向API中的端点发出列表请求，检索您的组织所使 `idnamespace/identities` 用的一GET标 [!DNL Identity Service] 识命名空间。 有关详细 [信息，请参阅Identity](../../identity-service/api/getting-started.md) Service开发人员指南。

## 命名空间限定符

在API中指 `namespace` 定值时， [!DNL Privacy Service] 命名空间限定符必 **须包含在相应的**`type` 参数中。 下表概述了不同的已接受命名空间限定符。

| 限定符 | 定义 |
| --------- | ---------- |
| 标准 | 全球定义的标准命名空间之一，不与单个组织数据集（例如，电子邮件、电话号码等）关联。 命名空间ID已提供。 |
| 自定义 | 在组织上下文中创建的唯一命名空间，不在整个组织中共享 [!DNL Experience Cloud]。 该值表示要搜索的友好名称（“名称”字段）。 命名空间ID已提供。 |
| integrationCode | 集成代码——与“自定义”类似，但明确定义为要搜索的数据源的集成代码。 命名空间ID已提供。 |
| namespaceId | 指示该值是通过命名空间服务创建或映射的命名空间的实际ID。 |
| 未注册 | 未在命名空间服务中定义且采用“原样”的自由形式字符串。 处理这些命名空间的任何应用程序都会针对它们进行检查，并根据公司上下文和数据集进行处理。 未提供命名空间ID。 |
| analytics | 在内部映射的自定义命名空间, [!DNL Analytics]而不是在命名空间服务中。 它直接按原始请求指定的方式传递，没有命名空间ID |
| Target | 内部理解的自定义命名空间 [!DNL Target]，而不是命名空间服务中理解的。 它直接按原始请求指定的方式传递，没有命名空间ID |

## 接受的产品值

下表概述了在作业创建请求的属性中指定Adobe产品 `include` 的已接受值。

| 产品 | 在属性中使用的 `include` 值 |
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