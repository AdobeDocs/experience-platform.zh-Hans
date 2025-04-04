---
keywords: Experience Platform；主页；热门主题；身份命名空间；身份命名空间
solution: Experience Platform
title: Identity Service故障排除指南
description: 本文档提供了有关Adobe Experience Platform Identity服务的常见问题解答，以及常见错误的疑难解答指南。
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2168'
ht-degree: 0%

---

# Identity Service故障排除指南

本文档提供了有关Adobe Experience Platform [!DNL Identity Service]的常见问题解答以及常见错误的疑难解答指南。 有关[!DNL Experience Platform] API的一般问题和疑难解答，请参阅[Adobe Experience Platform API疑难解答指南](../landing/troubleshooting.md)。

用于识别单个客户的数据通常分散在客户用于与您的品牌互动的各种设备和系统中。 [!DNL Identity Service]将这些分散的标识集合在一起，便于全面了解客户行为，以便您实时提供有影响力的数字体验。 有关详细信息，请参阅[Identity Service概述](./home.md)。

## 常见问题解答

以下是有关[!DNL Identity Service]的常见问题解答列表。

## 什么是身份数据？

身份数据是指可用于识别个人的任何数据。 根据组织中如何使用数据的上下文，身份数据可以包括CRM系统中的用户名、电子邮件地址和ID。 身份数据不仅限于网站或服务的注册用户，因为匿名用户也可以通过其设备或Cookie ID进行标识。

## 将数据字段标记为身份有什么好处？

通过将某些数据字段标记为记录和时间序列数据中的身份，您可以在数据的自然结构中映射身份关系，并跨渠道协调重复数据。 有关详细信息，请参阅[Identity Service概述](./home.md)。

## 什么是已知身份和匿名身份？

已知身份是指可以单独使用或与其他信息一起用于识别、联系或查找个人的身份值。 已知身份的示例可能包括电子邮件地址、电话号码和CRMID。

匿名身份是指无法单独使用或与其他信息配合使用来识别、联系或查找个人（例如Cookie ID）的身份值。

## 什么是专用身份图？

专用身份图是缝合身份和链接身份之间关系的专用映射，仅对您的组织可见。

在从流端点摄取的任何数据中包含多个身份或将这些身份发送到为[!DNL Identity Service]启用的数据集时，这些身份将在专用身份图中进行链接。 [!DNL Identity Service]利用此图形获取给定使用者或实体的身份，从而允许身份拼接和配置文件合并。

## 如何在XDM架构中创建多个标识字段？

[体验数据模型(XDM)](../xdm/home.md)架构支持多个标识字段。 实现XDM个人配置文件或XDM ExperienceEvent类的架构中类型为`string`的任何数据字段都可以标记为标识字段。 标记后，这些字段中包含的任何数据都会添加到用户档案的标识映射中。

有关如何使用用户界面将XDM字段标记为标识字段的步骤，请参阅架构编辑器教程中的[标识部分](../xdm/tutorials/create-schema-ui.md)。 如果您正在使用API，请参阅架构注册表API教程中的[身份描述符部分](../xdm/tutorials/create-schema-api.md)。

## 是否存在某些字段不应标记为标识的上下文？

应为每个人的唯一值保留标识字段。 例如，考虑一个客户忠诚度计划的数据集。 “忠诚度级别”字段（金、银、铜）不是有用的标识字段，而“忠诚度ID”（唯一值）将是。

邮政编码和IP地址等字段不应标记为个人的身份，因为这些值可以应用于多个个人。 对于家庭级别的营销策略，这些类型的字段只应标记为身份。

## 为什么我的身份字段没有按预期方式关联？

使用标识服务API中的[`/cluster/members`终结点](./api/list-cluster-identites.md)，可以查看一个或多个标识字段的关联标识。 如果响应未返回预期的链接身份，请确保在XDM数据中提供相应的身份信息。 有关详细信息，请参阅Identity Service概述中有关[向Identity Service提供XDM数据](./home.md)的部分。

## 什么是身份命名空间？

身份命名空间为身份字段如何与客户身份关联提供了上下文。 例如，“电子邮件”命名空间下的身份字段应符合标准电子邮件格式(名称<span>@emailprovider.com)，而使用“电话”命名空间的字段应符合标准电话号码（例如，在北美为987-555-1234）。

命名空间可以区分不同CRM系统之间的相似标识值。 例如，假定某个用户档案包含与公司奖励计划关联的会员数字ID。 “忠诚度”命名空间会将此值与同样显示在同一配置文件中的电子商务系统的类似数值ID分隔开。

有关详细信息，请参阅[身份命名空间概述](./home.md)。

## 如何将身份与身份命名空间关联？

身份字段在创建时必须与现有的身份命名空间关联。 任何新命名空间必须是[使用API](#how-do-i-create-a-custom-namespace-for-my-organization)创建的，然后才能与标识字段关联。

有关在使用API创建身份描述符时定义命名空间的分步说明，请参阅架构注册表开发人员指南中有关[创建描述符](../xdm/tutorials/create-schema-ui.md)的部分。 要在UI中将架构字段标记为标识，请按照[架构编辑器教程](../xdm/tutorials/create-schema-api.md)中的步骤操作。

## Experience Platform提供的标准身份命名空间是什么？ {#standard-namespaces}

标准身份命名空间是适用于所有组织的命名空间。 有关可用标准命名空间的完整列表，请参阅[身份命名空间概述](./features/namespaces.md)。

## 在哪里可以找到可用于我的组织的身份命名空间列表？

使用[身份服务API](https://www.adobe.io/experience-platform-apis/references/identity-service)，您可以通过向`/idnamespace/identities`端点发出GET请求来列出组织的所有可用身份命名空间。 有关详细信息，请参阅Identity Service API概述中有关[列出可用命名空间](./api/list-namespaces.md)的部分。

## 如何为我的组织创建自定义命名空间？

使用[身份服务API](https://www.adobe.io/experience-platform-apis/references/identity-service)，您可以通过向`/idnamespace/identities`端点发出POST请求来为组织创建自定义身份命名空间。 有关详细信息，请参阅Identity Service API概述中有关[创建自定义命名空间](./api/create-custom-namespace.md)的部分。

## 什么是复合身份和XID？

API调用中由其复合身份或XID引用身份。 复合身份是包含ID值和命名空间的身份的表示形式。 XID是一个单值标识符，它表示与复合身份（ID和命名空间）相同的构造，当身份服务持久化时，它会自动分配给新身份。 有关详细信息，请参阅[Identity Service API概述](./home.md)。

## Identity Service如何处理个人身份信息(PII)？

Identity Service具有标准命名空间，可支持为电话号码和电子邮件摄取哈希身份值。 但是，您应负责值的哈希处理。 若要了解有关对摄取到Experience Platform中的数据执行哈希处理的详细信息，请参阅[[!DNL Data Prep] 映射函数指南](../data-prep/functions.md#hashing)。

## 对基于PII的标识进行哈希处理时是否有任何注意事项？

如果要将经过哈希处理的PII值发送到Identity Service，则必须在数据集中使用相同的加密方法。 这可确保跨数据集的相同身份值生成相同的哈希值，并能够在身份图中进行正确匹配和链接。

<!-- Documentation does not show any methods of editing the identityMap directly, and this table never overtly recommends using identityMap anyway. This should probably be removed unless PM thinks otherwise. -->
<!-- ## When should I use the Identity map rather than labeling individual XDM schema fields?

The following table describes when the recommended approach for including identity data in your XDM would be identity map and when an identity field is the better method.

>[!NOTE]
>
>An advantage `identityMap` has is the ability to include multiple identity values for a single namespace.

Write|XDM identity field|`identityMap`
---|---|---
UI|Supported|Supported
Developer|Recommended|Supported
ETL|Recommended|Avoid - While this is supported, data should be formatted naturally when using an ETL, favoring identity fields over `identityMap`.
Internal solutions|Preferred|Common

--- -->

## 为何无法访问身份图页面或API？

您的Experience Platform管理员必须为您预配`view-identity-graph`权限，以便您查看身份图数据。 如果没有此权限，您将在身份图查看器页面上以及调用Experience Platform API时收到权限被拒绝消息。 有关权限的详细信息，请参阅[访问控制概述](../access-control/home.md)。

## 故障排除

以下部分提供了有关在使用[!DNL Identity Service] API时可能遇到的具体错误代码和意外行为的故障排除建议。

## [!DNL Identity Service]条错误消息

以下是您在使用[!DNL Identity Service] API时可能遇到的错误消息列表。

### 缺少所需的查询参数

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

当请求路径中未包含所需的查询参数时，将显示此错误。 错误消息的`detail`提供了缺少参数的名称。 此错误消息的变体包括：

- 缺少所需的查询参数 — nsId
- 缺少所需的查询参数 — id
- 缺少所需的查询参数 — xid或(nsid，id)
- 缺少所需的查询参数 — targetNs
- 缺少所需的查询参数 — xids或compositeXids

在重试之前，请检查您在请求路径中是否正确包含了指示的参数。

### 时间戳应在最近180天内

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service]清除超过180天的数据。 当您尝试访问早于此日期的数据时，会显示此错误消息。

### 单个调用中存在1000个XID的限制

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

当您尝试检索的标识信息超过单个API调用中允许的最大[XID](#what-are-composite-identities-and-xids)数时，将显示此错误消息。 将请求中的XID数量减少到显示限制以下可解决此问题。


### 单个调用中存在1000个compositeXid的限制

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

当您尝试检索的标识信息超过单个API调用中允许的[复合标识](#what-are-composite-identities-and-xids)的最大数量时，将显示此错误消息。 将请求中的复合身份数减少到显示限制以下可解决此问题。

### 指定的图形类型无效

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

当请求路径中为`graph-type`查询参数提供了无效值时，将显示此错误消息。 请参阅[!DNL Identity Service]概述中有关[身份图](./home.md)的部分，了解支持的图形类型。

### 服务令牌没有有效的范围

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

如果您的组织尚未配置[!DNL Identity Service]的适当权限，则会显示此错误消息。 请与系统管理员联系以解决此问题。

### 网关服务令牌无效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

如果出现此错误，您的访问令牌无效。 访问令牌每24小时过期一次，必须重新生成才能继续使用[!DNL Experience Platform] API。 有关生成新访问令牌的说明，请参阅[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。

### 授权服务令牌无效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

如果出现此错误，您的访问令牌无效。 访问令牌每24小时过期一次，必须重新生成才能继续使用[!DNL Experience Platform] API。 有关生成新访问令牌的说明，请参阅[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。

### 用户令牌没有有效的产品上下文

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

当您的访问令牌不是从[!DNL Experience Platform]集成中生成时，显示此错误消息。 有关为[!DNL Experience Platform]集成生成新访问令牌的说明，请参阅[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。

### 从标识和命名空间代码获取本机XID时出现内部错误

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

当[!DNL Identity Service]保留一个标识时，该标识的ID和关联的命名空间ID将分配一个称为XID的唯一标识符。 在查找给定ID值和命名空间的XID的过程中发生错误时，将显示此消息。

### 没有为[!DNL Identity Service]使用情况配置IMS组织

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

如果您的组织尚未配置[!DNL Identity Service]的适当权限，则会显示此错误消息。 请与系统管理员联系以解决此问题。

### 内部服务器错误

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

执行[!DNL Experience Platform]服务调用时发生意外异常时，将显示此错误。 最佳实践是在收到此错误时，对自动调用进行编程，以按一定的时间间隔重试其请求。 如果问题仍然存在，请与系统管理员联系。

## 批量摄取错误代码

[!DNL Identity Service]使用批处理摄取从上载到[!DNL Experience Platform]的记录和时序数据中摄取身份数据。 由于批次摄取是异步过程，因此您必须查看批次的详细信息才能查看错误。 错误将随着批的进行而累积，直到批完成。

以下是使用[批次摄取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)时可能遇到的与[!DNL Identity Service]相关的错误消息列表。

### 未知XDM架构

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service]只使用分别符合[!DNL Profile]或[!DNL ExperienceEvent]类的记录或时序数据的标识。 尝试摄取不符合任一类的[!DNL Identity Service]的数据将触发此错误。

### 已处理批次的前100行中有0个有效标识

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

当批次的前100行不显示身份时，显示此错误。 但是，此错误并不表明在后续记录中找不到身份。

### 跳过了记录，因为每个XDM记录只有1个身份

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service]仅在单个记录存在两个或多个标识值时链接标识。 此错误消息针对每个摄取的批次出现一次，并显示仅能找到一个身份并导致身份图未发生更改的记录数。

### 未为此IMS组织注册命名空间代码

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

当摄取的记录呈现的标识关联命名空间不存在或您的组织无法访问时，将显示此错误。

### 正在跳过批量摄取，因为没有为专用身份图形配置IMS组织

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

当摄取批次数据时，如果您的组织尚未配置[!DNL Identity Service]的适当权限，则会显示此错误消息。 请与系统管理员联系以解决此问题。

### 内部错误

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

在批处理摄取期间发生意外异常时，将显示此错误。 最佳实践是在收到此错误时，对自动调用进行编程，以按一定的时间间隔重试其请求。 如果问题仍然存在，请与系统管理员联系。
