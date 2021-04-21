---
keywords: Experience Platform；主页；热门主题；身份命名空间；身份命名空间
solution: Experience Platform
title: Identity Service疑难解答指南
topic-legacy: troubleshooting
description: 本文档提供有关Adobe Experience Platform Identity Service的常见问题解答以及常见错误的疑难解答指南。
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2189'
ht-degree: 0%

---

# Identity Service疑难解答指南

本文档提供有关Adobe Experience Platform [!DNL Identity Service]的常见问题解答，以及常见错误的疑难解答指南。 有关[!DNL Platform] API的一般问题和疑难解答，请参阅[Adobe Experience Platform API疑难解答指南](../landing/troubleshooting.md)。

确定单个客户的数据通常在他们用于与您的品牌互动的各种设备和系统中分散。 [!DNL Identity Service] 将这些分散的身份收集在一起，促进对客户行为的全面了解，以便您能够实时提供有影响力的数字体验。有关详细信息，请参阅[Identity Service概述](./home.md)。

## 常见问题解答

以下是有关[!DNL Identity Service]的常见问题解答列表。

## 什么是身份数据？

身份数据是指可用于识别个人身份的任何数据。 根据您组织中数据使用方式的上下文，身份数据可以包括CRM系统中的用户名、电子邮件地址和ID。 身份数据不仅限于网站或服务的注册用户，因为匿名用户也可以通过其设备或Cookie ID进行标识。

## 将数据字段标记为身份有哪些好处？

将某些数据字段标记为记录和时间序列数据中的身份，使您能够在数据的自然结构中映射身份关系并协调重复数据跨渠道。 有关详细信息，请参阅[Identity Service概述](./home.md)。

## 什么是已知身份和匿名身份？

已知标识是指可以单独使用或与其他信息一起使用的标识值，用于标识、联系或定位个人。 已知身份的示例可能包括电子邮件地址、电话号码和CRM ID。

匿名身份是指不能单独使用或与其他信息一起使用的身份值，用于标识、联系或定位个人（如Cookie ID）。

## 什么是私人身份图？

私人身份图是拼接和链接身份之间关系的私人图，仅对您的组织可见。

当从流端点摄取或发送到为[!DNL Identity Service]启用的数据集的任何数据中包含多个标识时，这些标识将链接在“私有标识图”中。 [!DNL Identity Service] 利用此图表为给定的消费者或实体收集身份，允许身份拼接和用户档案合并。

## 如何在XDM模式中创建多个标识字段？

[体验数据模型(XDM)](../xdm/home.md) 模式支持多个标识字段。实现XDM单个用户档案或XDM ExperienceEvent类的模式中类型`string`的任何数据字段都可以标记为标识字段。 标记后，这些字段中包含的任何数据都将添加到用户档案的标识映射中。

有关如何使用用户界面将XDM字段标记为标识字段的步骤，请参阅模式编辑器教程中的[标识部分](../xdm/tutorials/create-schema-ui.md)。 如果您使用的是API，请参阅模式 Registry API教程中的[Identity描述符部分](../xdm/tutorials/create-schema-api.md)。

## 某些字段是否不应标记为身份的上下文?

标识字段应保留为每个个人唯一的值。 例如，考虑客户忠诚度项目的数据集。 “忠诚度级别”字段（金、银、铜）将不是有用的身份域，而忠诚度ID（唯一值）将是。

不应将邮政编码和IP地址等字段标记为个人身份，因为这些值可以应用于多个个人。 这些类型的领域只应被标记为家庭级营销策略的身份。

## 为什么我的身份域没有按我期望的方式链接？

使用Identity Service API中的[`/cluster/members` endpoint](./api/list-cluster-identites.md)，可以视图一个或多个标识字段的关联标识。 如果响应未返回您期望的链接身份，请确保您在XDM数据中提供适当的身份信息。 有关详细信息，请参阅Identity Service概述中关于[向Identity Service](./home.md)提供XDM数据的部分。

## 什么是身份命名空间?

身份命名空间提供了有关身份字段如何与客户身份相关的上下文。 例如，“电子邮件”命名空间下的标识字段应符合标准电子邮件格式(名称<span>@emailprovider.com)，而使用“电话”命名空间的字段应符合标准电话号码(如北美的987-555-1234)。

命名空间区分不同CRM系统之间的相似标识值。 例如，考虑包含与用户档案奖励项目关联的数字忠诚度ID的公司。 命名空间“Loyalty”会将此值与同一用户档案中显示的电子商务系统的类似数字ID分开。

有关详细信息，请参阅[标识命名空间概述](./home.md)。

## 如何将身份与身份命名空间关联？

创建身份字段时，必须将其与现有身份命名空间关联。 在将任何新命名空间与标识字段关联之前，必须使用API](#how-do-i-create-a-custom-namespace-for-my-organization)创建它们。[

有关在使用API创建标识描述符时定义命名空间的分步说明，请参阅《模式注册表开发人员指南》中有关创建描述符](../xdm/tutorials/create-schema-ui.md)的部分。 [要在UI中将模式字段标记为标识，请按照[模式编辑器教程](../xdm/tutorials/create-schema-api.md)中的步骤操作。

## Experience Platform提供了哪些标准身份命名空间?{#standard-namespaces}

标准身份命名空间是所有组织都可用的命名空间。 有关可用标准命名空间的完整列表，请参阅[标识命名空间概述](./namespaces.md)。

## 在哪里可以找到适用于我的组织的身份命名空间列表?

使用[Identity Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)，您可以通过向`/idnamespace/identities`端点发出GET请求，列表组织的所有可用标识命名空间。 有关详细信息，请参阅Identity Service API概述中的[列出可用命名空间](./api/list-namespaces.md)部分。

## 如何为我的组织创建自定义命名空间?

使用[Identity Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)，可以通过向`/idnamespace/identities`端点发出POST请求，为组织创建自定义标识命名空间。 有关详细信息，请参阅Identity Service API概述中关于[创建自定义命名空间](./api/create-custom-namespace.md)的部分。

## 什么是复合身份和XID?

身份在API调用中由其复合身份或XID引用。 组合标识是包含ID值和命名空间的标识的表示。 XID是单值标识符，它表示与复合标识(ID和命名空间)相同的构造，并在由标识服务保留时自动分配给新标识。 有关详细信息，请参阅[Identity Service API概述](./home.md)。

## Identity Service如何处理个人身份信息(PII)?

Identity Service在保持值之前创建PII的强单向加密哈希。 “电话”和“电子邮件”命名空间中的标识数据使用SHA-256自动进行散列处理，“电子邮件”值在散列处理之前自动转换为小写。

## 我是否应在发送到平台之前加密所有PII?

在将PII数据引入平台之前，您无需手动加密它。 通过将`I1`数据使用标签应用于所有适用的数据字段，平台在摄取时会自动将这些字段转换为散列ID值。

有关如何应用和管理数据使用标签的步骤，请参阅[数据使用标签教程](../data-governance/labels/user-guide.md)。

## 在散列基于PII的身份时是否有考虑事项？

如果要将哈希PII值发送到Identity Service，则必须在数据集上使用相同的加密方法。 这可确保数据集中相同的身份值生成相同的哈希值，并能够在身份图中正确匹配和链接。

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

以下部分针对使用[!DNL Identity Service] API时可能遇到的特定错误代码和意外行为提供疑难解答建议。

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

当请求路径中未包含所需的查询参数时，将显示此错误。 错误消息的`detail`提供缺失参数的名称。 此错误消息的变体包括：

- 缺少必需的查询参数 — nsId
- 缺少必需的查询参数 — id
- 缺少必需的查询参数 — xid或(nsid，id)
- 缺少必需的查询参数 — targetNs
- 缺少必需的查询参数 — xids或compositeXids

在重试之前，请检查是否在请求路径中正确地包含指示的参数。

### 时间戳应在最近180天内

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] 清除180天以上的数据。当您尝试访问早于此的数据时，将显示此错误消息。

### 单次呼叫中最多有1000个XID

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

当您尝试检索单个API调用中允许的超过最大数量[XID](#what-are-composite-identities-and-xids)的身份信息时，将显示此错误消息。 将请求中的XID数量减少到所显示限制以解决此问题。


### 单次调用中限制为1000个compositeXids

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

当您尝试检索单个API调用中允许的超过最大数量的[复合身份](#what-are-composite-identities-and-xids)的身份信息时，将显示此错误消息。 将请求中的复合身份数量减少到所显示的限制以下以解决此问题。

### 指定的图形类型无效

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

当在请求路径中为`graph-type`查询参数赋值时，将显示此错误消息。 请参见[!DNL Identity Service]概述中[标识图形](./home.md)的部分，了解支持哪些图形类型。

### 服务令牌没有有效范围

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

当您的IMS组织尚未设置对[!DNL Identity Service]的适当权限时，将显示此错误消息。 请联系您的系统管理员以解决此问题。

### 网关服务令牌无效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

如果出现此错误，则您的访问令牌无效。 访问令牌每24小时过期一次，必须重新生成才能继续使用[!DNL Platform] API。 有关生成新访问令牌的说明，请参见[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。

### 授权服务令牌无效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

如果出现此错误，则您的访问令牌无效。 访问令牌每24小时过期一次，必须重新生成才能继续使用[!DNL Platform] API。 有关生成新访问令牌的说明，请参见[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。

### 用户令牌没有有效的产品上下文

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

当尚未从[!DNL Experience Platform]集成生成访问令牌时，将显示此错误消息。 有关为[!DNL Experience Platform]集成生成新访问令牌的说明，请参阅[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。

### 从标识和命名空间代码获取本机XID时出现内部错误

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

当[!DNL Identity Service]持续存在标识时，将为标识的ID和关联的命名空间ID分配一个称为XID的唯一标识符。 在查找给定ID值和命名空间的XID过程中发生错误时，将显示此消息。

### 未针对[!DNL Identity Service]使用情况设置IMS组织

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

当您的IMS组织尚未设置对[!DNL Identity Service]的适当权限时，将显示此错误消息。 请联系您的系统管理员以解决此问题。

### 内部服务器错误

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

当执行[!DNL Platform]服务调用时发生意外异常时，将显示此错误。 最佳实践是，在收到此错误时，项目自动调用以在定时间隔内重试其请求几次。 如果问题仍然存在，请与系统管理员联系。

## 批摄取错误代码

[!DNL Identity Service] 使用批处理摄取从上载到的记录和时间序列数据 [!DNL Platform] 中摄取标识数据。由于批处理是异步过程，因此必须将批处理的详细信息视图为视图错误。 错误将随着批处理进行而累积，直到批处理完成。

以下是使用[数据摄取API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)时可能遇到的与[!DNL Identity Service]相关的错误消息列表。

### 未知的XDM模式

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] 仅为分别符合或类的记录或时间序列数 [!DNL Profile] 据 [!DNL ExperienceEvent] 消耗标识。尝试为未符合任何类的[!DNL Identity Service]收录数据将触发此错误。

### 处理的批处理的前100行中有0个有效身份

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

当批的前100行未显示身份时，将显示此错误。 但是，此错误没有明确表明在后续记录中未找到任何身份。

### 跳过记录，因为每个XDM记录只有1个标识

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] 仅当单个记录显示两个或更多标识值时链接标识。对于每个摄取的批次，此错误消息发生一次，并显示记录数，其中只能找到一个标识，导致对标识图没有更改。

### 命名空间代码未注册到此IMS组织

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

当收录的记录显示其关联命名空间不存在或IMS组织无法访问的标识时，将显示此错误。

### 正在跳过批摄取，因为IMS组织未针对专用标识图设置

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

在摄取批处理数据时，当您的IMS组织尚未设置对[!DNL Identity Service]的适当权限时，将显示此错误消息。 请联系您的系统管理员以解决此问题。

### 内部错误

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

当批处理摄取期间发生意外异常时，将显示此错误。 最佳实践是，在收到此错误时，项目自动调用以在定时间隔内重试其请求几次。 如果问题仍然存在，请与系统管理员联系。
