---
keywords: Experience Platform；主页；热门主题；身份命名空间；身份命名空间
solution: Experience Platform
title: Identity Service疑难解答指南
topic-legacy: troubleshooting
description: 本文档提供了有关Adobe Experience Platform Identity Service的常见问题解答，以及常见错误的疑难解答指南。
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '2185'
ht-degree: 0%

---

# Identity Service疑难解答指南

本文档提供了有关Adobe Experience Platform [!DNL Identity Service]的常见问题解答，以及常见错误的疑难解答指南。 有关[!DNL Platform] API的一般问题和疑难解答，请参阅[Adobe Experience Platform API疑难解答指南](../landing/troubleshooting.md)。

识别单个客户的数据通常会在他们用于与您的品牌互动的各种设备和系统中分散。 [!DNL Identity Service] 将这些分散的身份收集在一起，以促进对客户行为的完整了解，从而实时提供有影响的数字体验。有关更多信息，请参阅[Identity Service概述](./home.md)。

## 常见问题解答

以下是有关[!DNL Identity Service]的常见问题解答列表。

## 什么是身份数据？

身份数据是指可用于识别个人的任何数据。 根据组织内数据使用方式的上下文，身份数据可以包含CRM系统中的用户名、电子邮件地址和ID。 身份数据不限于您网站或服务的注册用户，因为匿名用户也可以通过其设备或Cookie ID进行标识。

## 将数据字段标记为身份有何好处？

将某些数据字段标记为记录和时间系列数据中的标识后，您可以在数据的自然结构中映射标识关系，并协调跨渠道的重复数据。 有关更多信息，请参阅[Identity Service概述](./home.md)。

## 什么是已知身份和匿名身份？

已知身份是指身份值，可单独或与其他信息一起使用来识别、联系或查找个人。 已知身份的示例可能包括电子邮件地址、电话号码和CRM ID。

匿名身份是指身份值，不能单独使用或与其他信息一起使用来识别、联系或查找个人（如Cookie ID）。

## 什么是专用身份图？

专用身份图是拼合和关联身份之间关系的专用映射，仅对您的组织可见。

如果从流端点摄取的任何数据中包含多个标识，或者将这些标识发送到为[!DNL Identity Service]启用的数据集，则这些标识会关联到专用标识图中。 [!DNL Identity Service] 利用此图表来收集给定消费者或实体的身份，从而允许身份拼合和配置文件合并。

## 如何在XDM架构中创建多个身份字段？

[体验数据模型(XDM)](../xdm/home.md) 架构支持多个身份字段。在实施XDM个人配置文件或XDM ExperienceEvent类的架构中，任何类型为`string`的数据字段均可标记为标识字段。 标记后，这些字段中包含的任何数据都会添加到用户档案的标识映射中。

有关如何使用用户界面将XDM字段标记为标识字段的步骤，请参阅架构编辑器教程中的[标识部分](../xdm/tutorials/create-schema-ui.md)。 如果您使用的是API，请参阅架构注册表API教程中的[标识描述符部分](../xdm/tutorials/create-schema-api.md)。

## 是否有某些字段不应标记为标识的上下文？

对于每个人都唯一的值，应保留标识字段。 例如，以客户忠诚度计划的数据集为例。 “忠诚度级别”字段（金、银、铜）将不是有用的身份字段，而忠诚度ID（唯一值）将是。

邮政编码和IP地址等字段不应标记为个人的身份，因为这些值可以应用于多个个人。 此类字段只应标记为家庭级营销策略的标识。

## 为什么我的身份字段没有按我预期的方式关联？

在Identity Service API中使用[`/cluster/members`端点](./api/list-cluster-identites.md)，可以查看一个或多个标识字段的关联标识。 如果响应未返回您预期的链接身份，请确保您在XDM数据中提供了相应的身份信息。 有关更多信息，请参阅Identity Service概述中的[将XDM数据提供给Identity Service](./home.md)部分。

## 什么是身份命名空间？

身份命名空间提供了身份字段如何与客户身份关联的上下文。 例如，“Email”命名空间下的身份字段应符合标准电子邮件格式(名称<span>@emailprovider.com)，而使用“Phone”命名空间的字段应符合标准电话号码(例如北美的987-555-1234)。

命名空间可区分不同CRM系统之间的相似身份值。 例如，假定用户档案包含与贵公司的奖励计划关联的会员ID数字。 命名空间“忠诚度”会将此值与同一用户档案中显示的电子商务系统类似数字ID分开。

有关更多信息，请参阅[标识命名空间概述](./home.md)。

## 如何将身份与身份命名空间关联？

标识字段在创建时必须与现有标识命名空间关联。 任何新命名空间都必须使用API](#how-do-i-create-a-custom-namespace-for-my-organization)创建[，然后才能与标识字段关联。

有关在使用API创建标识描述符时定义命名空间的分步说明，请参阅《架构注册开发人员指南》中[创建描述符](../xdm/tutorials/create-schema-ui.md)部分。 要在UI中将架构字段标记为标识，请按照[架构编辑器教程](../xdm/tutorials/create-schema-api.md)中的步骤操作。

## Experience Platform提供的标准身份命名空间是什么？ {#standard-namespaces}

标准身份命名空间是所有组织都可用的命名空间。 有关可用标准命名空间的完整列表，请参阅[身份命名空间概述](./namespaces.md)。

## 在哪里可以找到适用于我的组织的身份命名空间列表？

使用[Identity Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)，您可以通过向`/idnamespace/identities`端点发出GET请求，列出组织的所有可用身份命名空间。 有关更多信息，请参阅Identity Service API概述中的[列出可用命名空间](./api/list-namespaces.md)部分。

## 如何为我的组织创建自定义命名空间？

使用[Identity Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)，您可以通过向`/idnamespace/identities`端点发出POST请求，为组织创建自定义身份命名空间。 有关更多信息，请参阅Identity Service API概述中关于创建自定义命名空间](./api/create-custom-namespace.md)的部分。[

## 什么是复合身份和XID?

身份在API调用中通过其复合身份或XID引用。 组合标识是包含ID值和命名空间的身份的表示形式。 XID是单值标识符，它表示与复合身份（ID和命名空间）相同的结构，并在Identity服务保留时自动将其分配给新身份。 有关更多信息，请参阅[Identity Service API概述](./home.md) 。

## Identity Service如何处理个人身份信息(PII)?

Identity Service在保留值之前创建PII的强单向加密哈希。 “Phone”和“Email”命名空间中的身份数据将使用SHA-256自动进行哈希处理，在进行哈希处理之前，“Email”值会自动转换为小写。

## 在发送到Platform之前，是否应加密所有PII?

在将PII数据摄取到Platform之前，您无需手动加密该数据。 通过将`I1`数据使用标签应用于所有适用的数据字段，Platform会在摄取数据时自动将这些字段转换为经过哈希处理的ID值。

有关如何应用和管理数据使用情况标签的步骤，请参阅[数据使用情况标签教程](../data-governance/labels/user-guide.md)。

## 对基于PII的身份进行哈希处理时，是否考虑任何事项？

如果要将经过哈希处理的PII值发送到Identity Service，则必须在数据集中使用相同的加密方法。 这可确保跨数据集的相同身份值生成相同的哈希值，并能够在身份图中正确匹配和链接这些值。

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

## 疑难解答

以下部分提供了有关使用[!DNL Identity Service] API时可能遇到的特定错误代码和意外行为的故障诊断建议。

## [!DNL Identity Service] 错误消息

以下是使用[!DNL Identity Service] API时可能遇到的错误消息列表。

### 缺少必需的查询参数

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

请求路径中未包含必需的查询参数时，将显示此错误。 错误消息的`detail`提供缺少参数的名称。 此错误消息的变体包括：

- 缺少必需的查询参数 — nsId
- 缺少必需的查询参数 — id
- 缺少必需的查询参数 — xid或(nsid，id)
- 缺少必需的查询参数 — targetNs
- 缺少必需的查询参数 — xid或compositeXid

再次尝试之前，请检查请求路径中是否正确包含了指示的参数。

### 时间戳应在最近180天内

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] 清除超过180天的数据。当您尝试访问低于此值的数据时，会显示此错误消息。

### 单次调用中的XID限制为1000个

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

当您尝试检索的身份信息数量超过单个API调用中允许的最大数量[XID](#what-are-composite-identities-and-xids)时，将显示此错误消息。 将请求中的XID数量减少到显示的限制以下，以解决此问题。


### 单次调用中限制为1000个compositeXid

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

当您尝试检索的身份信息超过单个API调用中允许的最大数量[复合身份](#what-are-composite-identities-and-xids)时，将显示此错误消息。 将请求中的复合身份数量减少到显示的限制以下，以解决此问题。

### 指定的图形类型无效

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

在请求路径中为`graph-type`查询参数指定无效值时，将显示此错误消息。 请参阅[!DNL Identity Service]概述中[标识图形](./home.md)的部分，以了解支持哪些图形类型。

### 服务令牌没有有效范围

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

当您的IMS组织未配置[!DNL Identity Service]的适当权限时，会显示此错误消息。 请联系您的系统管理员以解决此问题。

### 网关服务令牌无效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

如果出现此错误，您的访问令牌无效。 访问令牌每24小时过期一次，必须重新生成，才能继续使用[!DNL Platform] API。 有关生成新访问令牌的说明，请参阅[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。

### 授权服务令牌无效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

如果出现此错误，您的访问令牌无效。 访问令牌每24小时过期一次，必须重新生成，才能继续使用[!DNL Platform] API。 有关生成新访问令牌的说明，请参阅[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。

### 用户令牌没有有效的产品上下文

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

未从[!DNL Experience Platform]集成生成访问令牌时，将显示此错误消息。 有关为[!DNL Experience Platform]集成生成新访问令牌的说明，请参阅[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。

### 从身份和命名空间代码获取本机XID时出现内部错误

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

当[!DNL Identity Service]保留标识时，该标识的ID和关联的命名空间ID会被分配一个称为XID的唯一标识符。 当在查找给定ID值和命名空间的XID过程中出错时，将显示此消息。

### 未针对[!DNL Identity Service]使用情况设置IMS组织

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

当您的IMS组织未配置[!DNL Identity Service]的适当权限时，会显示此错误消息。 请联系您的系统管理员以解决此问题。

### 内部服务器错误

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

当执行[!DNL Platform]服务调用时发生意外异常时，将显示此错误。 最佳实践是对自动调用进行编程，以在收到此错误时在定时间隔内重试其请求几次。 如果问题仍然存在，请与系统管理员联系。

## 批量摄取错误代码

[!DNL Identity Service] 从使用批量摄取的已上传到的记录和时间系列数据中摄取 [!DNL Platform] 身份数据。由于批量摄取是一个异步流程，因此您必须查看批量的详细信息才能查看错误。 错误将随着批处理的进行而累积，直到批处理完成为止。

以下是使用[数据摄取API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/)时可能遇到的与[!DNL Identity Service]相关的错误消息列表。

### 未知的XDM架构

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] 仅对符合或类的记录或时间系列数据使 [!DNL Profile] 用 [!DNL ExperienceEvent] 标识。尝试为不符合任一类的[!DNL Identity Service]摄取数据将触发此错误。

### 已处理批处理的前100行中有0个有效标识

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

当批次的前100行未显示任何标识时，将显示此错误。 但是，此错误没有明确表示在后续记录中未找到任何身份。

### 跳过了记录，因为每个XDM记录只有1个标识

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] 仅当单个记录存在两个或更多标识值时，才会链接标识。此错误消息针对每个摄取的批次发生一次，并显示只能找到一个身份的记录数，并且不会导致对身份图进行更改。

### 未为此IMS组织注册命名空间代码

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

当摄取的记录显示的标识的关联命名空间不存在或IMS组织无法访问，则会显示此错误。

### 由于未为专用身份图配置IMS组织，因此正在跳过批量摄取

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

在摄取批量数据时，当您的IMS组织未配置[!DNL Identity Service]的适当权限时，会显示此错误消息。 请联系您的系统管理员以解决此问题。

### 内部错误

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

当批量摄取期间发生意外异常时，会显示此错误。 最佳实践是对自动调用进行编程，以在收到此错误时在定时间隔内重试其请求几次。 如果问题仍然存在，请与系统管理员联系。
