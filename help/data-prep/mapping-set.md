---
keywords: Experience Platform；主页；映射器；映射集；映射；
solution: Experience Platform
title: 映射集概述
description: 了解如何将映射集与Adobe Experience Platform数据准备结合使用。
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# 映射集概述

映射集是一组映射，用于将数据从一个架构转换到另一个架构。 本文档提供了有关如何构成映射集的信息，包括输入架构、输出架构和映射。

## 快速入门

此概述需要对Adobe Experience Platform的以下组件有一定的了解：

- [数据准备](./home.md):数据准备允许数据工程师映射、转换和验证来自体验数据模型(XDM)的数据。
- [数据流](../dataflows/home.md):数据流是跨平台移动数据的数据作业的表示形式。 数据流是跨不同的服务进行配置的，有助于将数据从源连接器移动到目标数据集，并 [!DNL Identity] 和 [!DNL Profile]和 [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md):将数据发送到的方法 [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。

## 映射集语法

映射集由ID、名称、输入模式、输出模式和关联映射的列表组成。

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
| `outputSchema` | 将转换输入数据所符合的XDM模式。 |
| `mappings` | 从源架构到目标架构的字段到字段映射数组。 |
| `sourceType` | 对于列出的每个映射，其 `sourceType` 属性指示要映射的源类型。 可以是 `ATTRIBUTE`, `STATIC`或 `EXPRESSION`: <ul><li> `ATTRIBUTE` 用于在源路径中找到的任何值。 </li><li>`STATIC` 用于插入到目标路径中的值。 此值保持不变，不受源架构的影响。</li><li> `EXPRESSION` 用于表达式，该表达式将在运行时解析。 可在 [映射函数指南](./functions.md).</li> </ul> |
| `source` | 对于列出的每个映射， `source` 属性表示要映射的字段。 有关如何配置源的更多信息，请参阅 [源部分](#sources). |
| `destination` | 对于列出的每个映射， `destination` 属性指示字段或字段路径，其中从 `source` 字段。 有关如何配置目标的更多信息，请参阅 [目标部分](#destination). |
| `mappings.name` | (*可选*)映射的名称。 |
| `mappings.description` | (*可选*)映射的描述。 |

## 配置映射源

在映射中， `source` 可以是字段、表达式或静态值。 根据给定的源类型，可以通过各种方式提取值。

### 柱状数据中的字段

在柱状数据（如CSV文件）中映射字段时，请使用 `ATTRIBUTE` 源类型。 如果字段包含 `.` 在其名称中，使用 `\` 以转义值。 以下是此映射的示例：

**CSV文件示例：**

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

**转换的数据**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 嵌套数据中的字段

在嵌套数据（如JSON文件）中映射字段时，请使用 `ATTRIBUTE` 源类型。 如果字段包含 `.` 在其名称中，使用 `\` 以转义值。 以下是此映射的示例：

**JSON文件示例**

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

**转换的数据**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 数组中的字段

在数组中映射字段时，可以使用索引检索特定值。 为此，请使用 `ATTRIBUTE` 源类型和要映射的值的索引。 以下是此映射的示例：

**JSON文件示例**

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

**转换的数据**

```json
{
    "pi": {
        "email": "js@example.com"
    }
}
```

### 数组到数组或对象到对象

使用 `ATTRIBUTE` 源类型中，您还可以将数组直接映射到数组或对象。 以下是此映射的示例：

**JSON文件示例**

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

**转换的数据**

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

使用 `ATTRIBUTE` 源类型，您可以通过数组迭代循环并使用通配符索引(`[*]`)。 以下是此映射的示例：

**JSON文件示例**

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

**转换的数据**

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

如果要映射常量或静态值，请使用 `STATIC` 源类型。  使用 `STATIC` 源类型， `source` 表示要分配给的硬编码值 `destination`. 以下是此映射的示例：

**JSON文件示例**

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

**转换的数据**

```json
{
    "userType:": "CUSTOMER"
}
```

### 表达式

如果要映射表达式，请使用 `EXPRESSION` 源类型。 可在 [映射函数指南](./functions.md). 使用 `EXPRESSION` 源类型， `source` 表示要解析的函数。 以下是此映射的示例：

**JSON文件示例**

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

**转换的数据**

```json
{
    "pi": {
        "created": "SMITHJOHNFri Sep 25 15:17:31 PDT 2020"
    }
}
```

## 配置映射目标

在映射中， `destination` 是从 `source` 中，将被插入。

### 根级别的字段

当您想要映射 `source` 值到转换后数据的根级别，请遵循以下示例：

**JSON文件示例**

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

**转换的数据**

```json
{
    "name": "John Smith"
}
```

### 嵌套字段

当您想要映射 `source` 值，请按照以下示例操作：

**JSON文件示例**

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

**转换的数据**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 特定数组索引处的字段

当您想要映射 `source` 值到转换数据中数组中的特定索引，请遵循以下示例：

**JSON文件示例**

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

**转换的数据**

```json
{
    "piList": ["John Smith"]
}
```

### 迭代阵列运算

当您想通过数组迭代循环并将值映射到目标时，可以使用通配符索引(`[*]`)。 示例如下所示：

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

**转换的数据**

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

通过阅读本文档，您现在应该了解如何构建映射集，包括如何在映射集中配置单个映射。 有关其他数据准备功能的更多信息，请阅读 [数据准备概述](./home.md). 要了解如何在数据准备API中使用映射集，请阅读 [数据准备开发人员指南](./api/overview.md).
