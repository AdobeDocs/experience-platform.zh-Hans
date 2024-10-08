---
title: 筛选Reactor API中的响应
description: 了解在Reactor API中列出资源时如何筛选结果。
exl-id: 8a91f3dd-4ead-4a10-abb1-e71acb0d73b6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# 筛选Reactor API中的响应

在Reactor API中使用list (GET)端点时，您可能会发现有必要将返回的结果限制为记录的子集。 为实现此目的，API的很多列表端点都支持按特定属性进行筛选的功能。 如果您希望改为对API进行结构化查询，请参阅[搜索](./search.md)指南。

## 过滤语法

以下示例说明如何为GET请求实施过滤器。

**API格式**

要筛选给定列表端点的响应，必须在请求路径中提供`filter`查询参数。

>[!NOTE]
>
>下面的模板使用方括号(`[]`)和空格字符以提高可读性。 实际上，这些字符必须采用URI编码，如[RFC 3986](https://tools.ietf.org/html/rfc3986)中所述。 本指南的后面部分显示了正确编码的请求路径的示例。
>
>请注意，如果筛选器的结构不正确，则不会应用任何筛选器并返回完整结果集。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| 属性 | 描述 |
| --- | --- |
| `{ENDPOINT}` | Reactor API中支持过滤器参数的列表端点。 |
| `{ATTRIBUTE_NAME}` | 用于筛选结果的特定属性的名称。 请记住，不同的端点支持不同的筛选属性。 有关正在处理的端点的参考指南，以获取可用筛选属性的列表。 |
| `{OPERATOR}` | 确定如何针对提供的`{VALUE}`评估结果的运算符。 [附录部分](#supported-operators)列出了支持的运算符。 |
| `{VALUE}` | 返回结果要与之比较的值。 使用`EQ`运算符比较相等项时，该值必须是精确的、区分大小写的匹配项，才能包含在响应中。 |

{style="table-layout:auto"}

**请求**

下面的示例请求通过应用要求库的`state`属性等于`published`的筛选器来检索已发布的库的列表。

在URI编码之前，请求路径中此过滤器的语法将类似于以下内容：

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

对路径和查询参数进行URI编码后，它们便可用于API请求，如下所示：

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

## 筛选多个值 {#multiple-values}

要按单个属性的多个值进行筛选，请以逗号分隔列表的形式提供这些值。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## 使用多个过滤器

要为多个属性应用筛选器，请为每个属性提供一个`filter`参数。 参数必须用&amp;符号(`&`)分隔。

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>如果在同一请求的多个筛选器中指定同一属性，则仅会应用为该属性提供的最后一个筛选器。

## 附录

以下部分包含有关在Reactor API中使用过滤器的其他信息。

### 支持的筛选器运算符 {#operators}

下表列出了过滤器参数支持的运算符值。 请记住，根据筛选依据的属性，并非所有可用的筛选运算符都适用，例如对字符串属性使用“小于”或“大于”运算符。

| 操作员 | 描述 |
| --- | --- |
| `EQ` | 该属性必须等于提供的值。 |
| `NOT` | 属性不得等于提供的值。 |
| `LT` | 属性必须小于提供的值。 |
| `GT` | 属性必须大于提供的值。 |
| `BETWEEN` | 该属性必须在指定的值范围内。 使用此运算符时，必须提供[两个值](#multiple-values)以指示所需范围的最小值和最大值。 |
| `CONTAINS` | 该属性必须包含提供的值，如字符串属性中的一组字符。 |
