---
keywords: Experience Platform；主页；映射器；映射集；映射；
solution: Experience Platform
title: 映射集概述
description: 了解如何将映射集与Adobe Experience Platform数据准备结合使用。
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: 660948b7a43ed3c18feb74cccf8f9c607470759c
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# 映射集概述

映射集是一组映射，用于将数据从一个架构转换为另一个架构。 本文档提供有关映射集如何构成的信息，包括输入架构、输出架构和映射。

## 快速入门

此概述需要您对Adobe Experience Platform的以下组件有一定的了解：

- [数据准备](./home.md)：数据准备允许数据工程师映射、转换和验证进出体验数据模型(XDM)的数据。
- [数据流](../dataflows/home.md)：数据流表示跨Platform移动数据的数据作业。 数据流在不同的服务之间配置，有助于将数据从源连接器移动到目标数据集，以 [!DNL Identity] 和 [!DNL Profile]、和 [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md)：将数据发送到的方法 [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。

## 映射集语法

映射集由ID、名称、输入架构、输出架构和关联映射列表组成。

以下JSON是典型映射集的示例：

```json
{
    "id": "cbb0da769faa48fcb29e026a924ba29d",
    "name": "Demo Mapping Set",
    "inputSchema": {
        "id": "a167ff2947ff447ebd8bcf7ef6756232",
        "version": 0
    },
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/6dd1768be928c36d58ad4897219bb52d491671f966084bc0",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "Id",
            "destination": "_id",
            "name": "Id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "FirstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "LastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 映射集的唯一标识符。 |
| `name` | 映射集的名称。 |
| `inputSchema` | 传入数据的XDM架构。 |
| `outputSchema` | 输入数据将转换为符合的XDM架构。 |
| `mappings` | 从源架构到目标架构的字段到字段映射数组。 |
| `sourceType` | 对于列出的每个映射，其 `sourceType` attribute指示要映射的源类型。 可以是以下之一 `ATTRIBUTE`， `STATIC`，或 `EXPRESSION`： <ul><li> `ATTRIBUTE` 用于源路径中找到的任何值。 </li><li>`STATIC` 用于插入目标路径中的值。 该值保持不变，不受源架构的影响。</li><li> `EXPRESSION` 用于表达式，该表达式将在运行时解析。 可用表达式的列表可在 [映射函数指南](./functions.md).</li> </ul> |
| `source` | 对于每个列出的映射， `source` attribute表示要映射的字段。 有关如何配置源的详细信息，请参见 [源概述](../sources/home.md). |
| `destination` | 对于每个列出的映射， `destination` attribute表示字段或字段的路径，其中值是从 `source` 将放置字段。 有关如何配置目标的更多信息，请参阅 [目标概述](../destinations/home.md). |
| `mappings.name` | (*可选*)映射的名称。 |
| `mappings.description` | (*可选*)映射的说明。 |

## 配置映射源

在映射中， `source` 可以是字段、表达式或静态值。 根据给定的源类型，可以通过多种方式提取该值。

### 列数据中的字段

在列数据（如CSV文件）中映射字段时，请使用 `ATTRIBUTE` 源类型。 如果字段包含 `.` 在其名称内，使用 `\` 以转义值。 此映射的示例如下所示：

**示例CSV文件：**

```csv
Full.Name, Email
John Smith, js@example.com
```

**示例映射**

```json
{
    "source": "Full.Name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**转换后的数据**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 嵌套数据中的字段

在嵌套数据（如JSON文件）中映射字段时，请使用 `ATTRIBUTE` 源类型。 如果字段包含 `.` 在其名称内，使用 `\` 以转义值。 此映射的示例如下所示：

**示例JSON文件**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**示例映射**

```json
{
    "source": "customerInfo.name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**转换后的数据**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 数组中的字段

在数组中映射字段时，可以使用索引检索特定值。 要执行此操作，请使用 `ATTRIBUTE` 源类型和要映射的值的索引。 此映射的示例如下所示：

**示例JSON文件**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**示例映射**

```json
{
    "source": "customerInfo.emails[0].email",
    "destination": "pi.email",
    "sourceType": "ATTRIBUTE"
}
```

**转换后的数据**

```json
{
    "pi": {
        "email": "js@example.com"
    }
}
```

### 数组到数组或对象到对象

使用 `ATTRIBUTE` 源类型，您还可以直接将数组映射到数组，或将对象映射到对象。 此映射的示例如下所示：

**示例JSON文件**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**示例映射**

```json
{
    "source": "customerInfo.emails",
    "destination": "pi.emailList",
    "sourceType": "ATTRIBUTE"
}
```

**转换后的数据**

```json
{
    "pi": {
        "emailList": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

### 阵列上的迭代运算

使用 `ATTRIBUTE` 源类型时，可以使用通配符索引(`[*]`)。 此映射的示例如下所示：

**示例JSON文件**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**示例映射**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**转换后的数据**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

### 常量值

如果要映射常量或静态值，请使用 `STATIC` 源类型。  使用时 `STATIC` 源类型， `source` 表示要分配到的硬编码值 `destination`. 此映射的示例如下所示：

**示例JSON文件**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**示例映射**

```json
{
    "source": "CUSTOMER",
    "destination": "userType",
    "sourceType": "STATIC"
}
```

**转换后的数据**

```json
{
    "userType:": "CUSTOMER"
}
```

### 表达式

如果要映射表达式，请使用 `EXPRESSION` 源类型。 接受的函数列表可在 [映射函数指南](./functions.md). 使用时 `EXPRESSION` 源类型， `source` 表示要解析的功能。 此映射的示例如下所示：

**示例JSON文件**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**示例映射**

```json
{
    "source": "concat(upper(lastName), upper(firstName), now())",
    "destination": "pi.created",
    "sourceType": "EXPRESSION"
}
```

**转换后的数据**

```json
{
    "pi": {
        "created": "SMITHJOHNFri Sep 25 15:17:31 PDT 2020"
    }
}
```

## 配置映射目标

在映射中， `destination` 是从中提取值的位置 `source` 将被插入。

### 根级别的字段

当您想要映射 `source` 值到转换后数据的根级别，请遵循以下示例：

**示例JSON文件**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**示例映射**

```json
{
    "source": "customerInfo.name",
    "destination": "name",
    "sourceType": "ATTRIBUTE"
}
```

**转换后的数据**

```json
{
    "name": "John Smith"
}
```

### 嵌套字段

当您想要映射 `source` 值转换为转换后的数据中的嵌套字段，请遵循以下示例：

**示例JSON文件**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**示例映射**

```json
{
    "source": "name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**转换后的数据**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 特定数组索引处的字段

当您想要映射 `source` 值到转换后的数据阵列中的特定索引时，请遵循以下示例：

**示例JSON文件**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**示例映射**

```json
{
    "source": "customerInfo.name",
    "destination": "piList[0]",
    "sourceType": "ATTRIBUTE"
}
```

**转换后的数据**

```json
{
    "piList": ["John Smith"]
}
```

### 迭代阵列运算

如果要循环遍历数组并将值映射到目标，可以使用通配符索引(`[*]`)。 下面显示了这方面的示例：

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**示例映射**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**转换后的数据**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

## 后续步骤

通过阅读本文档，您现在应该了解如何构建映射集，包括如何在映射集中配置各个映射。 有关其他数据准备功能的详细信息，请阅读 [数据准备概述](./home.md). 要了解如何在数据准备API中使用映射集，请参阅 [数据准备开发人员指南](./api/overview.md).
