---
keywords: Experience Platform;home;popular topics;identity namespace;Identity namespace
solution: Experience Platform
title: Adobe Experience Platform身份服务疑难解答指南
topic: troubleshooting
description: 本文档提供有关Adobe Experience Platform身份服务的常见问题解答，以及常见错误的疑难解答指南。
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '2248'
ht-degree: 1%

---


# Identity Service疑难解答指南

此文档提供有关Adobe Experience Platform的常见问题的 [!DNL Identity Service]解答，以及常见错误的疑难解答指南。 有关API的一般问题 [!DNL Platform] 和疑难解答，请参阅 [Adobe Experience PlatformAPI疑难解答指南](../landing/troubleshooting.md)。

识别单个客户的数据通常在他们用于与您的品牌互动的各种设备和系统中分散。 [!DNL Identity Service] 将这些分散的身份汇集在一起，以便全面了解客户行为，从而实时提供有影响力的数字体验。 有关详细信息，请参 [阅Identity Service概述](./home.md)。

## 常见问题解答

以下是关于常见问题的一列表答案 [!DNL Identity Service]。

## 什么是身份数据？

身份数据是可用于识别个人的任何数据。 根据组织中数据使用方式的上下文，标识数据可以包括CRM系统中的用户名、电子邮件地址和ID。 身份数据不仅限于网站或服务的注册用户，因为匿名用户也可以通过其设备或cookie ID进行标识。

## 将数据字段标记为身份有何好处？

将某些数据字段标记为记录和时间序列数据中的身份，使您能够在数据的自然结构中映射身份关系并协调重复数据的跨渠道。 有关详细 [信息，请参阅](./home.md) Identity Service概述。

## 什么是已知和匿名身份？

已知身份是指可以单独使用或与其他信息一起使用的身份值，用于识别、联系或定位个人。 已知身份的示例可能包括电子邮件地址、电话号码和CRM ID。

匿名身份是指不能单独使用或与其他信息一起使用的身份值，用于识别、联系或定位个人（如cookie ID）。

## 什么是私人身份图？

私人身份图是拼接和链接身份之间关系的私人地图，仅对您的组织可见。

当从流端点摄取或发送到启用的数据集的任何数据中包含多个标识时，这些标识 [!DNL Identity Service]会在“专用标识图”中链接。 [!DNL Identity Service] 利用此图表为给定的消费者或实体收集身份，允许身份拼接和用户档案合并。

## 如何在XDM模式中创建多个标识字段？

[体验数据模型(XDM)模式](../xdm/home.md) 支持多个身份字段。 实现XDM个人 `string` 用户档案或XDM ExperienceEvent类的模式中任何类型的数据字段都可以标记为标识字段。 标记后，这些字段中包含的任何数据都将添加到用户档案的标识图中。

有关如何使用用户界面将XDM字段标记为标识字段的步骤，请参阅模式编 [辑器教程](../xdm/tutorials/create-schema-ui.md) 中的“标识”部分。 如果您正在使用API，请参阅模式 [注册表API教程](../xdm/tutorials/create-schema-api.md) 中的“标识描述符”部分。

## 某些字段不应标记为身份的上下文是否存在？

标识字段应保留为每个个人唯一的值。 例如，考虑客户忠诚度项目的数据集。 “忠诚度级别”字段（金、银、铜牌）不是有用的身份领域，而忠诚度ID（唯一值）则是。

ZIP代码和IP地址等字段不应标记为个人身份，因为这些值可以应用于多个个人。 这些领域只应被标记为家庭级营销策略的标识。

## 为什么我的身份字段没有按我期望的方式链接？

使用 [`/cluster/members` Identity Service](./api/list-cluster-identites.md) API中的端点，您可以视图一个或多个标识字段的关联标识。 如果响应未返回您期望的链接身份，请确保您在XDM数据中提供适当的身份信息。 有关详细信息，请 [参阅“标识服务”概述](./home.md) ，参阅将XDM数据提供到标识服务一节。

## 什么是身份命名空间?

标识命名空间提供了标识字段如何与客户标识相关的上下文。 例如，“电子邮件”命名空间下的标识字段应符合标准电子邮件格式(名称<span>@emailprovider.com)，而使用“电话”命名空间的字段应符合标准电话号码（如北美的987-555-1234）。

命名空间区分不同CRM系统之间的相似标识值。 例如，考虑一个用户档案，其中包含与公司奖励项目关联的数字忠诚度ID。 命名空间为“Loyalty”会将此值与同一用户档案中显示的电子商务系统的类似数字ID相分离。

有关更多 [信息，请参阅](./home.md) “身份命名空间概述”。

## 如何将身份与身份命名空间关联？

创建身份字段时，必须将其与现有身份命名空间关联。 在将任何新命名空间与标 [识字段关联之前](#how-do-i-create-a-custom-namespace-for-my-organization) ，必须使用API创建这些。

有关在使用API创建标识描述符时定义命名空间的分步说明，请参阅《模式注册表开 [发人员指南](../xdm/tutorials/create-schema-ui.md) 》中有关创建描述符的一节。 要在UI中将模式字段标记为标识，请按照模式编辑器教程中 [的步骤操作](../xdm/tutorials/create-schema-api.md)。

## Experience Platform提供的标准身份命名空间是什么？ {#standard-namespaces}

以下标准命名空间供Experience Platform内的所有组织使用：

| 显示名称 | ID | 代码 | 描述 |
| ------------ | --- | --- | ----------- |
| CORE | 0 | CORE | 旧名称：“Adobe AudienceManager” |
| ECID | 4 | ECID | 别名：&quot;Adobe Marketing CloudID&quot;、&quot;Adobe Experience CloudID&quot;、&quot;Adobe Experience PlatformID&quot; |
| 电子邮件 | 6 | 电子邮件 |  |
| 电子邮件（SHA256，小写） | 11 | 电子邮件 | 预散列电子邮件的标准命名空间。 此命名空间中提供的值在使用SHA-256进行哈希处理前转换为小写。 |
| Phone | 7 | Phone |  |
| Windows AID | 8 | WAID |  |
| AdCloud | 411 | AdCloud | 别名：Ad Cloud |
| Adobe Target | 9 | TNTID | 目标ID |
| Google广告ID | 20914 | GAID | GAID |
| Apple IDFA | 20915 | IDFA | 广告商的ID |

## 在哪里可以找到可用于我的组织的身份命名空间的列表?

使用 [Identity Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)，您可以通过向端点发出GET请求来列表组织的所有可用标识 `/idnamespace/identities` 命名空间。 有关详细信息， [请参阅](./api/list-namespaces.md) Identity Service API概述中列出可用命名空间的部分。

## 如何为我的组织创建自定义命名空间?

使用 [Identity Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)，您可以通过向端点发出POST请求为组织创建自定义标识 `/idnamespace/identities` 命名空间。 有关详细信息， [请参阅Identity](./api/create-custom-namespace.md) Service API概述中有关创建自定义命名空间的部分。

## 什么是组合身份和XID?

标识在API调用中由其组合标识或XID引用。 组合标识是包含ID值和命名空间的标识的表示。 XID是表示与组合标识(ID和命名空间)相同的构造的单值标识符，当由标识服务保留时，会自动将其分配给新标识。 有关更 [多信息，请参阅](./home.md) Identity Service API概述。

## Identity Service如何处理个人身份信息(PII)?

Identity Service在持久值之前创建PII的强单向加密哈希。 “电话”和“电子邮件”命名空间中的标识数据使用SHA-256自动散列，“电子邮件”值在散列之前自动转换为小写。

## 我是否应在发送到平台之前加密所有PII?

在将PII数据引入平台之前，您无需手动加密它。 通过将数据 `I1` 使用标签应用于所有适用的数据字段，平台在获取时自动将这些字段转换为散列ID值。

有关如何应用和管理数据使用标签的步骤，请参阅数 [据使用标签教程](../data-governance/labels/user-guide.md)。

## 在散列基于PII的身份时，是否有考虑事项？

如果要将散列PII值发送到Identity Service，则必须在数据集中使用相同的加密方法。 这可确保数据集中相同的身份值生成相同的哈希值，并能够在身份图中正确匹配和链接。

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

## 故障诊断

以下部分提供了有关使用API时可能遇到的特定错误代码和意外行为的疑难解答 [!DNL Identity Service] 建议。

## [!DNL Identity Service] 错误消息

以下是您在使用API时可能遇到的一列表错误 [!DNL Identity Service] 消息。

### 缺少必需的查询参数

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

当请求路径中未包括所需的查询参数时，将显示此错误。 错 `detail` 误消息的名称提供了缺少的参数的名称。 此错误消息的变体包括：

- 缺少必需的查询参数- nsId
- 缺少必需的查询参数- id
- 缺少必需的查询参数- xid或(nsid,id)
- 缺少必需的查询参数- targetNs
- 缺少必需的查询参数- xids或compositeXids

再次尝试之前，请检查是否在请求路径中正确包含指示的参数。

### 时间戳应在最近180天内

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] 清除180天以上的数据。 当您尝试访问早于此版本的数据时，将显示此错误消息。

### 单次呼叫中限制1000个XID

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

当您尝试检索超过单个API调用中允许的最大XID数的身 [份信息](#what-are-composite-identities-and-xids) 时，会显示此错误消息。 将请求中的XID数量减少到显示的限制以解决此问题。


### 单个呼叫中限制1000个compositeXid

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

当您尝试检索超过单个API调用中允许的最大组合身份数的身 [份信息时](#what-are-composite-identities-and-xids) ，会显示此错误消息。 将请求中的复合身份数量减少到显示的限制以下，以解决此问题。

### 指定的图形类型无效

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

当请求路径中给 `graph-type` 定查询参数的值无效时，将显示此错误消息。 请参阅概述 [中的标](./home.md) 识图 [!DNL Identity Service] 一节，了解支持哪些图形类型。

### 服务令牌没有有效范围

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

未为您的IMS组织设置适当的权限时，将显示此错误消息 [!DNL Identity Service]。 请与系统管理员联系以解决此问题。

### 网关服务令牌无效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

如果出现此错误，则您的访问令牌无效。 访问令牌每24小时过期一次，必须重新生成才能继续使用 [!DNL Platform] API。 有关生成 [新访问令牌](../tutorials/authentication.md) ，请参阅身份验证教程。

### 授权服务令牌无效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

如果出现此错误，则您的访问令牌无效。 访问令牌每24小时过期一次，必须重新生成才能继续使用 [!DNL Platform] API。 有关生成 [新访问令牌](../tutorials/authentication.md) ，请参阅身份验证教程。

### 用户令牌没有有效的产品上下文

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

集成尚未生成访问令牌时，将显示此错误 [!DNL Experience Platform] 消息。 有关为集 [成生成新访问令牌](../tutorials/authentication.md) ，请参阅身份验证教程 [!DNL Experience Platform] 。

### 从标识和命名空间代码获取本机XID时出现内部错误

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

当 [!DNL Identity Service] 持续存在身份时，将为该身份的ID和关联的命名空间ID分配一个称为XID的唯一标识符。 当在查找给定ID值和命名空间的XID过程中发生错误时，将显示此消息。

### IMS组织未设置用 [!DNL Identity Service] 途

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

未为您的IMS组织设置适当的权限时，将显示此错误消息 [!DNL Identity Service]。 请与系统管理员联系以解决此问题。

### 内部服务器错误

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

执行服务调用时发生意外异常时，将显 [!DNL Platform] 示此错误。 最佳实践是在收到此错误时，项目自动调用以在定时间隔内重试其请求几次。 如果问题仍然存在，请与系统管理员联系。

## 批摄取错误代码

[!DNL Identity Service] 使用批处理摄取从上传到的记录和时间序列数据中摄取 [!DNL Platform] 标识数据。 由于批处理摄取是一个异步过程，因此必须将批处理的详细信息视图为视图错误。 错误会随着批处理的进行而累积，直到批处理完成为止。

以下是使用数据摄取API时 [!DNL Identity Service] 可能遇到的一列表 [错误消息](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)。

### 未知XDM模式

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] 只为分别符合或类的记录或时间序列数 [!DNL Profile] 据 [!DNL ExperienceEvent] 使用标识。 尝试为不符合 [!DNL Identity Service] 任何类的数据摄取数据将触发此错误。

### 已处理批处理的前100行中有0个有效身份

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

当批的前100行未显示身份时，将显示此错误。 但是，此错误没有明确表示在后续记录中未找到任何身份。

### 跳过记录，因为每个XDM记录只有1个标识

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] 仅当单个记录显示两个或更多标识值时链接标识。 对于每个摄取的批次，此错误消息发生一次，并显示记录数，其中只能找到一个身份，并导致对身份图没有更改。

### 命名空间代码未注册到此IMS组织

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

当收录的记录显示其关联命名空间不存在或IMS组织无法访问的标识时，将显示此错误。

### 由于IMS组织未针对专用标识图提供配置，正在跳过批摄取

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

在摄取批处理数据时，当IMS组织尚未为其设置适当的权限时，将显示此错误消息 [!DNL Identity Service]。 请与系统管理员联系以解决此问题。

### 内部错误

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

在批处理摄取期间发生意外异常时，将显示此错误。 最佳实践是在收到此错误时，项目自动调用以在定时间隔内重试其请求几次。 如果问题仍然存在，请与系统管理员联系。
