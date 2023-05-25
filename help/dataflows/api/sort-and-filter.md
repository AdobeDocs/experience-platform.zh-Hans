---
title: 在流服务API中对响应进行排序和筛选
description: 本教程介绍了使用流服务API中的查询参数进行排序和过滤的语法，包括一些高级用例。
exl-id: 029c3199-946e-4f89-ba7a-dac50cc40c09
source-git-commit: ef8db14b1eb7ea555135ac621a6c155ef920e89a
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 3%

---

# 对流量服务API中的响应进行排序和筛选

在中执行列表(GET)请求时 [流服务API](https://www.adobe.io/experience-platform-apis/references/flow-service/)，则可以使用查询参数来排序和筛选响应。 本指南提供了有关如何针对不同用例使用这些参数的参考。

## 排序

您可以使用对响应进行排序 `orderby` 查询参数。 可在API中对以下资源排序：

* [连接](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [源连接](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Target连接](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [流](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [运行](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

要使用参数，必须将其值设置为要作为排序依据的特定属性(例如， `?orderby=name`)。 您可以在该值前面添加一个加号(`+`)表示升序或减号(`-`)，以按降序排列。 如果未提供排序前缀，则默认情况下按升序对列表进行排序。

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

您还可以使用“和”符号(`&`)。

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## 正在筛选

您可以使用过滤响应 `property` 键值表达式的参数。 例如， `?property=id==12345` 仅返回满足以下条件的资源： `id` 属性完全等于 `12345`.

只要知晓实体的任何属性的有效路径，就可以对该属性普遍应用筛选。

>[!NOTE]
>
>如果某个属性嵌套在数组项中，则必须附加方括号(`[]`)到路径中的数组。 请参阅以下部分： [按数组属性筛选](#arrays) 例如。

**返回源表名称为的所有源连接 `lead`：**

```http
GET /sourceConnections?property=params.tableName==lead
```

**返回特定区段ID的所有流：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### 组合筛选器

多个 `property` 过滤器可以包含在查询中，但必须以“和”字符(`&`)。 组合筛选器时假设为AND关系，这意味着实体必须满足所有筛选器才能将其包含在响应中。

**返回一个区段ID的所有已启用的流：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### 对数组属性进行筛选 {#arrays}

您可以通过附加，根据数组中项的属性进行筛选 `[]` 到数组属性的名称。

**与特定源连接关联的返回流：**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**返回其转换包含特定选择器值ID的流：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**返回具有带特定列的源连接 `name` 值：**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**通过对区段ID进行筛选来查找目标的流运行ID：**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

任何筛选查询都可以附加 `count` 值为的查询参数 `true` 以返回结果的计数。 API响应包含 `count` 其值表示已筛选项目总数的属性。 此调用中未返回实际过滤的项目。

**返回系统中已启用的流的计数：**

```http
GET /flows?property=state==enabled&count=true
```

对上述查询的响应如下所示：

```json
{
  "count": 95
}
```

### 可按资源筛选的属性

根据要检索的流服务实体，可以使用不同的属性进行筛选。 下表列出了每个资源的根级别字段，这些字段通常用于筛选用例。

**`connectionSpec`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style="table-layout:auto"}

**`flowSpec`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style="table-layout:auto"}

**`connection`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style="table-layout:auto"}

**`sourceConnection`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`targetConnection`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`flow`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/flows?property=id==736873,9485095` |
| `name` | `/flows?property=name==TestFlow` |
| `description` | `/flows?property=description==Test%20description` |
| `flowSpec.id` | `/flows?property=flowSpec.id==938903,849048` |
| `state` | `/flows?property=state==enabled` |
| `sourceConnectionIds` | `/flows?property=sourceConnectionIds[]==9874984,6980696` |
| `targetConnectionIds` | `/flows?property=targetConnectionIds[]==598590,690666` |

{style="table-layout:auto"}

**`run`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style="table-layout:auto"}

## 后续步骤

本指南介绍了如何使用 `orderby` 和 `property` 用于在流服务API中对响应进行排序和筛选的查询参数。 有关如何将API用于Platform中的常见工作流程的分步指南，请参阅 [源](../../sources/home.md) 和 [目标](../../destinations/home.md) 文档。
