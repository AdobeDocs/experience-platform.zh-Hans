---
title: 对流量服务API中的响应进行排序和筛选
description: 本教程介绍了使用流量服务API中的查询参数进行排序和过滤的语法，包括一些高级用例。
source-git-commit: ccca81357bd7d7083abd3f395aa547c85ebf65fd
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 6%

---

# 在流量服务API中对响应进行排序和过滤

在[流量服务API](https://www.adobe.io/experience-platform-apis/references/flow-service/)中执行列表(GET)请求时，可以使用查询参数对响应进行排序和筛选。 本指南提供了如何将这些参数用于不同用例的参考。

## 排序

您可以使用`orderby`查询参数对响应进行排序。 可以在API中对以下资源进行排序：

* [连接](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [源连接](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [目标连接](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [流量](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [运行](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

要使用参数，必须将其值设置为要按排序的特定属性（例如，`?orderby=name`）。 您可以在值前面添加加号(`+`)以表示升序，或者在减号(`-`)以表示降序。 如果未提供排序前缀，则默认情况下，列表将以升序排序。

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

您还可以使用“and”符号(`&`)将排序参数与筛选参数组合使用。

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## 筛选

您可以使用带键值表达式的`property`参数来筛选响应。 例如， `?property=id==12345`仅返回其`id`属性恰好等于`12345`的资源。

只要该属性的有效路径已知，则通常可以对实体中的任何属性应用筛选。

>[!NOTE]
>
>如果属性嵌套在数组项中，则必须在路径的数组后面附加方括号(`[]`)。 有关示例，请参阅[筛选数组属性](#arrays)一节。

**返回源表名称为的所有源连 `lead`接：**

```http
GET /sourceConnections?property=params.tableName==lead
```

**返回特定区段ID的所有流：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### 组合过滤器

查询中可以包含多个`property`过滤器，前提是它们之间以“and”字符(`&`)分隔。 组合过滤器时假定为“与”关系，这意味着实体必须满足所有过滤器，才能将其包含在响应中。

**返回区段ID的所有已启用流：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### 筛选数组属性 {#arrays}

您可以根据数组中项目的属性进行筛选，方法是将`[]`附加到数组属性的名称。

**与特定源连接关联的返回流：**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**具有包含特定选择器值ID的转换的返回流：**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**返回具有特定值列的源连 `name` 接：**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**通过过滤区段ID来查找目标的流程运行ID:**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

任何筛选查询都可附加`count`查询参数，其值为`true`，以返回结果计数。 API响应包含`count`属性，其值表示过滤项目总数的计数。 此调用中不会返回实际的过滤项目。

**返回系统中已启用流的计数：**

```http
GET /flows?property=state==enabled&count=true
```

对上述查询的响应如下所示：

```json
{
  "count": 95
}
```

### 按资源划分的可过滤属性

根据要检索的流量服务实体，可以使用不同的属性进行筛选。 下表对筛选用例中常用的每个资源的根级别字段进行划分。

**`connectionSpec`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style=&quot;table-layout:auto&quot;}

**`flowSpec`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style=&quot;table-layout:auto&quot;}

**`connection`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style=&quot;table-layout:auto&quot;}

**`sourceConnection`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

**`targetConnection`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

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

{style=&quot;table-layout:auto&quot;}

**`run`**

| 属性 | 示例 |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style=&quot;table-layout:auto&quot;}

## 后续步骤

本指南介绍了如何使用`orderby`和`property`查询参数对流量服务API中的响应进行排序和筛选。 有关如何在Platform中将API用于常见工作流的分步指南，请参阅[sources](../../sources/home.md)和[目标](../../destinations/home.md)文档中包含的API教程。
