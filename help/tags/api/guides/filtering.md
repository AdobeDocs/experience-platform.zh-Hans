---
title: 在Reactor API中筛选响应
description: 了解在Reactor API中列出资源时如何过滤结果。
exl-id: 8a91f3dd-4ead-4a10-abb1-e71acb0d73b6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---

# 在Reactor API中筛选响应

在Reactor API中使用列表(GET)端点时，您可能会发现有必要将返回的结果限制为记录的子集。 要实现此目的，许多API的列表端点都支持按特定属性进行过滤的功能。 如果您希望改为对API进行结构化查询，请参阅 [搜索](./search.md).

## 过滤语法

以下示例说明如何为GET请求实施过滤器。

**API格式**

要过滤给定列表端点的响应，必须提供 `filter` 请求路径中的查询参数。

>[!NOTE]
>
>以下模板使用方括号(`[]`)和空格字符，以方便阅读。 实际上，这些字符必须采用URI编码，如 [RFC 3986](https://tools.ietf.org/html/rfc3986). 本指南后面显示了正确编码的请求路径的示例。
>
>请注意，如果过滤器的结构不正确，则不会应用任何过滤器，并返回完整的结果集。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| 属性 | 描述 |
| --- | --- |
| `{ENDPOINT}` | 支持过滤器参数的Reactor API中的列表端点。 |
| `{ATTRIBUTE_NAME}` | 要按过滤结果的特定属性的名称。 请记住，不同的端点支持用于筛选的不同属性。 有关可用筛选属性的列表，请参阅您正在使用的端点的参考指南。 |
| `{OPERATOR}` | 用于确定如何根据提供的评估结果的运算符 `{VALUE}`. 支持的运算符列在 [附录节](#supported-operators). |
| `{VALUE}` | 要比较返回结果的值。 当使用 `EQ` 运算符，值必须精确且区分大小写，才能包含在响应中。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下示例请求通过应用要求库 `state` 属性等于 `published`.

在URI编码之前，请求路径中此过滤器的语法类似于以下内容：

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

对路径和查询参数进行URI编码后，即可在API请求中使用，如下所示：

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

## 筛选多个值 {#multiple-values}

要按单个属性的多个值进行过滤，请以逗号分隔的列表形式提供这些值。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## 使用多个过滤器

要对多个属性应用过滤器，请提供 `filter` 参数。 参数必须以与号(`&`)字符。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>如果在同一请求的多个过滤器中指定同一属性，则将仅应用该属性最后提供的过滤器。

## 附录

以下部分包含有关在Reactor API中使用过滤器的其他信息。

### 支持的过滤器运算符 {#operators}

下表列出了支持的过滤器参数的运算符值。 请记住，根据过滤依据的属性，并非所有可用的过滤器运算符都适用，例如对字符串属性使用“小于”或“大于”运算符。

| 运算符 | 描述 |
| --- | --- |
| `EQ` | 属性必须等于提供的值。 |
| `NOT` | 属性不得等于提供的值。 |
| `LT` | 属性必须小于提供的值。 |
| `GT` | 属性必须大于提供的值。 |
| `BETWEEN` | 属性必须在指定的值范围内。 使用此运算符时， [两个值](#multiple-values) 必须提供以指示所需范围的最小值和最大值。 |
| `CONTAINS` | 属性必须包含提供的值，例如字符串属性中的一组字符。 |
