---
title: 身份图形链接规则疑难解答指南
description: 了解如何解决身份图关联规则中的常见问题。
badge: Beta 版
source-git-commit: cb0e229ac68f53d33b83d54df4062469252f06a3
workflow-type: tm+mt
source-wordcount: '2019'
ht-degree: 0%

---

# 身份图链接规则疑难解答指南

>[!AVAILABILITY]
>
>身份图链接规则功能目前处于测试阶段。 有关参与标准的信息，请与您的Adobe客户团队联系。 该功能和文档可能会发生更改。

在测试和验证身份图形链接规则时，您可能会遇到一些与数据摄取和图形行为相关的问题。 请阅读本文档，了解如何解决您在使用身份图链接规则时可能遇到的一些常见问题。

## 数据摄取流概述 {#data-ingestion-flow-overview}

下图是数据如何流入Adobe Experience Platform和应用程序的简化表示形式。 使用此图表作为参考，以帮助您更好地了解此页面的内容。

![Identity Service中数据摄取的流程图表。](../images/troubleshooting/dataflow_in_identity.png)

请务必注意以下因素：

* 对于流式传输数据，Real-time Customer Profile、Identity Service和Data Lake将在数据发送后开始处理数据。 但是，完成数据处理所需的延迟取决于该服务。 通常，与个人资料和身份相比，数据湖处理时间更长。
   * 如果即使在数小时后，对数据集运行查询时也没有显示数据，则数据可能没有摄取到Experience Platform中。
* 对于批处理数据，所有数据将先流入数据湖，然后如果为配置文件和身份启用数据集，数据将传播到配置文件和身份。
* 对于摄取相关问题，请务必在服务级别隔离问题，以便进行准确调试和故障排除。 需要考虑三种潜在问题类型：

| 摄取问题类型 | 数据是否会摄取到数据湖中？ | 数据是否会摄取到配置文件中？ | 数据是否会在Identity Service中引入？ |
| --- | --- | --- | --- |
| 常规摄取问题 | 否 | 否 | 否 |
| 图表问题 | 是 | 是 | 否 |
| 配置文件片段问题 | 是 | 否 | 是 |

## 数据摄取问题 {#data-ingestion-issues}

>[!NOTE]
>
>* 此部分假设数据已成功摄取到数据湖中，并且没有语法或其他错误会阻止数据首先被摄取到Experience Platform中。
>
>* 这些示例使用ECID作为Cookie命名空间，使用CRMID作为人员命名空间。

### 我的身份未摄取到Identity服务{#my-identities-are-not-getting-ingested-into-identity-service}

发生这种情况的原因有多种，包括但不限于以下各项：

* [未为配置文件](../../catalog/datasets/enable-for-profile.md)启用数据集。
* 跳过该记录，因为事件中只有一个标识。
* [身份服务中发生验证失败](../guardrails.md#identity-value-validation)。
   * 例如，ECID可能超过最大长度38个字符。
* 默认情况下，[AAID被阻止引入](../guardrails.md#identity-namespace-ingestion)。
* 身份因[系统护栏](../guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated)而被删除。

在身份图链接规则的上下文中，可能会拒绝来自Identity Service的记录，因为传入事件具有两个或多个具有相同唯一命名空间但身份值不同的身份。 这种情况通常因实施错误而发生。

用两个假设来考虑以下事件：

* 字段名称CRMID标记为具有命名空间CRMID的标识。
* 命名空间CRMID被定义为唯一的命名空间。

以下事件将返回一条错误消息，指示引入失败。

<!-- because the ingestion of this erroneous event would have resulted in graph collapse. In the following event, two entities (Alice and Bob) are both associated with the same namespace (CRMID). -->

```json
{ 
  "_id": "random_string", 
  "eventType": "web browsing event", 
  "identityMap": { 
    "ECID": [ 
      { 
        "id": "11111111111111111111111111111111111111", 
        "primary": false 
      } 
    ], 
    "CRMID": [ 
      { 
        "id": "Alice", 
        "primary": true 
      } 
    ] 
  }, 
  "CRMID": "Bob", 
  "timestamp": "2024-08-17T15:22:51+00:00", 
  "web": { 
    "webPageDetails": { 
      "URL": "https://www.adobe.com/acrobat.html", 
      "name": "Adobe Acrobat" 
    } 
  } 
} 
```

**疑难解答步骤**

要解决此错误，必须首先收集以下信息：

* 您应在身份图表中摄取的身份值(`identity_value`)。
* 发送事件的数据集(`dataset_name`)。

接下来，使用[Adobe Experience Platform查询服务](../../query-service/home.md)并运行以下查询：

>[!TIP]
>
>将`dataset_name`和`identity_value`替换为您收集的信息。

```sql
  SELECT key, col.id as identityValue, timestamp, _id, identityMap, * 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id = 'identity_value' 
```

运行查询后，查找预期生成图形的事件记录，然后验证同一行中的标识值是否不同。 查看以下图像的示例：

![一个无标题的查询产生了重复的命名空间。](../images/troubleshooting/duplicated_unique_namespace.png)

>[!NOTE]
>
>如果两个身份完全相同，并且事件是通过流式摄取的，则身份和配置文件都将删除重复身份。

### 我的体验事件片段未摄取到配置文件 {#my-experience-event-fragments-are-not-getting-ingested-into-profile}

您的体验事件片段未摄取到配置文件中的原因有多种，包括但不限于：

* [未为配置文件](../../catalog/datasets/enable-for-profile.md)启用数据集。
* [配置文件](../../xdm/classes/experienceevent.md)上可能发生了验证失败。
   * 例如，体验事件必须同时包含`_id`和`timestamp`。
   * 此外，每个事件（记录）的`_id`必须是唯一的。

在命名空间优先级上下文中，配置文件将拒绝任何包含两个或更多具有最高命名空间优先级的身份的事件。 例如，如果GAID未标记为唯一的命名空间，并且有两个同时具有GAID命名空间和不同的标识值的标识，则Profile将不存储任何事件。

**疑难解答步骤**

要解决此错误，请阅读上述指南中概述的有关[有关未摄取到Identity服务的数据的错误疑难解答的步骤](#my-identities-are-not-getting-ingested-into-identity-service)。

### 我的体验事件片段已摄取，但在配置文件中具有“错误”的主要身份

命名空间优先级在事件片段确定主要身份的方式中发挥重要作用。

* 配置并保存给定沙盒的[身份设置](./identity-settings-ui.md)后，配置文件将使用[命名空间优先级](namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events)确定主要身份。 在使用identityMap时，配置文件将不再使用`primary=true`标志。
* 虽然配置文件将不再引用此标志，但Experience Platform上的其他服务可能会继续使用`primary=true`标志。

为了将[经过身份验证的用户事件](configuration.md#ingest-your-data)绑定到人员命名空间，所有经过身份验证的事件都必须包含人员命名空间(CRMID)。 这意味着即使用户登录后，人员命名空间仍必须存在于每个已验证的事件中。

在配置文件查看器中查找配置文件时，您可能会继续看到`primary=true`个“事件”标记。 但是，这将被忽略并且不会被配置文件使用。

默认情况下，会阻止AAID。 因此，如果您使用的是[Adobe Analytics源连接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)，则必须确保ECID的优先级高于ECID，以便未经身份验证的事件将具有ECID的主标识。

**疑难解答步骤**

* 要验证经过身份验证的事件是否同时包含人员和Cookie命名空间，请阅读[中有关未摄取到Identity服务的数据的错误疑难解答部分概述的步骤](#my-identities-are-not-getting-ingested-into-identity-service)。
* 要验证经过身份验证的事件是否具有人员命名空间的主要身份（例如CRMID），请使用无拼接合并策略（这是不使用专用图的合并策略）在配置文件查看器中搜索人员命名空间。 此搜索将仅返回与人员命名空间关联的事件。

## 与图表行为相关的问题 {#graph-behavior-related-issues}

本节概述您可能会遇到的有关身份图行为方式的常见问题。

### 该身份已链接到“错误”人员

标识优化算法将执行[最近建立的链接并删除最早的链接](./identity-optimization-algorithm.md#identity-optimization-algorithm-details)。 因此，启用此功能后，可以将ECID从一个人重新分配（重新链接）到另一个人。 要了解标识如何随时间链接的历史记录，请执行以下步骤：

**疑难解答步骤**

>[!NOTE]
>
>以下步骤将根据以下假设检索信息：
>
>* 单个数据集正在使用中（这不会查询多个数据集）。
>
>* 由于[高级数据生命周期管理](../../hygiene/home.md)、[Privacy Service](../../privacy-service/home.md)或执行删除的其他服务删除了数据，因此数据不会从数据湖中删除。

首先，您必须收集以下信息：

* 已发送的Cookie命名空间（例如ECID）和人员命名空间（例如CRMID）的标识符号(namespaceCode)。
   * 对于Web SDK实施，这些通常是identityMap中包含的命名空间。
   * 对于Analytics源连接器实施，这些是identityMap中包含的Cookie标识符。 人员标识符是标记为身份的eVar字段。
* 在中发送事件的数据集(dataset_name)。
* 要查找的Cookie命名空间的身份值(identity_value)。

身份符号(namespaceCode)区分大小写。 要检索identityMap中给定数据集的所有标识符号，请运行以下查询：

```sql
SELECT distinct explode(*)FROM (SELECT map_keys(identityMap) FROM dataset_name)
```

如果您不知道Cookie标识符的标识值，并且希望搜索已链接到多个人员标识符的Cookie ID，则必须运行以下查询。 此查询假定ECID作为Cookie命名空间，CRMID作为人员命名空间。

>[!BEGINTABS]

>[!TAB Web SDK实施]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct identityMap['CRMID'][0]['id']) as crmidCount FROM dataset_name GROUP BY identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

>[!TAB Analytics源连接器实施]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct personID) as crmidCount FROM dataset_name group by identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

**注意：**&#x200B;人员ID引用描述符的路径。 您可以在架构下找到此信息。

>[!ENDTABS]

接下来，通过运行以下查询来按时间戳顺序检查Cookie命名空间的关联：

>[!BEGINTABS]

>[!TAB Web SDK实施]

```sql
  SELECT identityMap['CRMID'][0]['id'] as personEntity, * 
  FROM dataset_name 
  WHERE identitymap['ECID'][0].id ='identity_value' 
  ORDER BY timestamp desc 
```

>[!TAB Analytics源连接器实施]

```sql
SELECT _experience.analytics.customDimensions.eVars.eVar10 as personEntity, * 
FROM dataset_name 
WHERE identitymap['ECID'][0].id ='identity_value' 
ORDER BY timestamp desc 
```

**注意**：此示例假定`eVar10`被标记为身份。 对于配置，必须根据您自己组织的实施更改eVar。

>[!ENDTABS]

### 身份优化算法未按预期“工作”

**疑难解答步骤**

请参阅有关[标识优化算法](./identity-optimization-algorithm.md)的文档，以及支持的图形结构类型。

* 有关支持的图形结构的示例，请阅读[图形配置指南](./example-configurations.md)。
* 您还可以阅读[实施指南](./configuration.md#appendix)以了解不支持的图形结构的示例。 有两种情况可能会发生：
   * 您的所有配置文件中没有单个命名空间。
   * 出现[“挂起ID”](./configuration.md#dangling-loginid-scenario)方案。 在此方案中，Identity Service无法确定挂起ID是否与图形中的任何人员实体相关联。

您还可以使用UI](./graph-simulation.md)中的[图形模拟工具来模拟事件并配置您自己的唯一命名空间和命名空间优先级设置。 这样做有助于您基本了解身份优化算法的行为。

如果仿真结果符合图形行为预期，则可以检查[身份设置](./identity-settings-ui.md)是否与您在模拟中配置的设置匹配。

### 即使在配置身份设置后，我仍会在沙盒中看到折叠的图形

在保存设置后&#x200B;_身份图形将遵循您配置的唯一命名空间和命名空间优先级_。 任何在&#x200B;_之前存在_&#x200B;的“折叠”图形都不会受到影响，除非引入新数据以更新折叠的图形。 即使命名空间优先级发生更改，实时客户配置文件上事件片段的主要标识也不会更新。

**疑难解答步骤**

您可以使用[身份图形查看器](../features/identity-graph-viewer.md)来检查您的图形是在设置之前还是之后摄取。 检查[!UICONTROL 链接属性]下的上次更新时间戳，以查看Identity Service何时摄取该图形。 如果时间戳在配置之前，则表示在启用该功能之前创建了“折叠”图。

![具有示例图的身份图查看器。](../images/troubleshooting/graph_viewer.png)

### 我想知道我的沙盒中有多少个“折叠”的图表

使用身份仪表板可以查看身份图的状态，如身份计数和图形。 请参阅量度“具有多个命名空间的图形计数”，了解已折叠的图形计数 — 这些图形包含两个或多个具有相同命名空间的身份。 假定沙盒没有数据，并且您已将命名空间（例如CRMID）配置为唯一，则预期应存在具有两个或更多CRMID的零个图形。 在下面的示例中，有两个包含两个或更多电子邮件地址的图表。

![身份仪表板，其中包含关于两个以上命名空间的身份计数、图形计数、按命名空间计数、按大小划分图形计数和图形计数的量度。](../images/troubleshooting/identity_dashboard.png)

通过运行以下查询，您可以在Data Lake的[配置文件快照导出数据集](../../dashboards/query.md)中找到详细细分：

>[!NOTE]
>
>* 将`dataset_name`替换为数据集的实际名称。
>
>* 这些数量可能并不完全匹配。 身份仪表板基于身份图计数，以下查询基于具有两个或多个身份的配置文件计数。 数据由服务独立处理和更新。

```sql
  SELECT key, identityCountInGraph, count(identityCountInGraph) as graphCount 
  FROM (SELECT key, cardinality(value) as identityCountInGraph 
  FROM (SELECT explode(identityMap) 
  FROM dataset_name 
  WHERE cardinality(identityMap) > 1)) /* by definition, graphs have 2 or more identities */ 
  WHERE key not in ('ecid', 'aaid', 'idfa', 'gaid') /* filter out common device/cookie namespaces */ 
  GROUP BY 1, 2 
  ORDER BY 1, 2 asc 
```

您可以在配置文件快照导出数据集中使用以下查询，以从“折叠”的图形获取示例身份。

```sql
  SELECT identityMap 
  FROM dataset_name 
  WHERE cardinality(identityMap['CRMID'])>1 /* any graphs with 2+ CRMID. Change CRMID namespace if needed */ 
```

>[!TIP]
>
>如果没有为共享设备临时方法启用沙盒，上面列出的两个查询将产生预期结果，并且其行为与标识图链接规则有所不同。