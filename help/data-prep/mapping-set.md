---
keywords: Experience Platform;home;mapper;mapping set;mapping;
solution: Experience Platform
title: 映射集概述
topic: 概述
description: 了解如何将映射集与Adobe Experience Platform Data Prep结合使用。
translation-type: tm+mt
source-git-commit: 4c06f621eb6fba8daa6501d56255cddbbcfdbda2
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---


# 映射集概述

映射集是一组映射，可将模式从一个映射转换到另一个映射。 此文档提供有关映射集的构成方式的信息，包括输入模式、输出模式和映射。

## 入门指南

此概述需要对Adobe Experience Platform的以下组件有充分的了解：

- [数据准备](./home.md):数据准备使数据工程师能够映射、转换和验证数据到体验数据模型(XDM)和从体验数据模型(XDM)的数据。
- [数据流](../dataflows/home.md):数据流是跨平台移动数据的数据作业的表示。跨不同的服务配置数据流，从而帮助将数据从源连接器移动到目标数据集、到[!DNL Identity]和[!DNL Profile]以及[!DNL Destinations]。
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md):数据发送方 [!DNL Experience Platform]法
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。

## 映射集语法

映射集由ID、名称、输入模式、输出模式和关联映射的列表组成。

以下JSON是典型映射集的示例：

```json
{
    "id" : "cbb0da769faa48fcb29e026a924ba29d",
    "name" : "Demo Mapping Set",
    "inputSchema" : {
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
            "name" : "Id",
            "description" : "Identifier field"
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
| `inputSchema` | 传入数据的XDM模式。 |
| `outputSchema` | 将转换输入数据的XDM模式以符合。 |
| `mappings` | 从源模式到目标模式的字段到字段映射的数组。 |
| `sourceType` | 对于列出的每个映射，其`sourceType`属性指示要映射的源的类型。 可以是`ATTRIBUTE`、`STATIC`或`EXPRESSION`之一： <ul><li> `ATTRIBUTE` 用于在源路径中找到的任何值。 </li><li>`STATIC` 用于注入到目标路径中的值。此值保持不变，不受源模式的影响。</li><li> `EXPRESSION` 用于表达式，将在运行时解析。[映射函数指南](./functions.md)中可找到可用表达式的列表。</li> </ul> |
| `source` | 对于每个列出的映射，`source`属性指示要映射的字段。 有关如何配置源的详细信息，请参阅[源部分](#sources)。 |
| `destination` | 对于列出的每个映射，`destination`属性指示字段或字段的路径，将放置从`source`字段提取的值。 有关如何配置目标的详细信息，请参阅[目标部分](#destination)。 |
| `mappings.name` | （*可选*）映射的名称。 |
| `mappings.description` | （*可选*）映射的说明。 |

## 配置映射源

在映射中，`source`可以是字段、表达式或静态值。 根据给定的源类型，可以采用多种方式提取值。

### 柱状数据字段

在柱形数据（如CSV文件）中映射字段时，请使用`ATTRIBUTE`源类型。 如果字段名称中包含`.`，请使用`\`转义该值。 以下是此映射的示例：

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

**转换的数据**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 嵌套数据中的字段

在映射嵌套数据（如JSON文件）中的字段时，请使用`ATTRIBUTE`源类型。 如果字段名称中包含`.`，请使用`\`转义该值。 以下是此映射的示例：

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

**转换的数据**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 数组中的字段

在数组内映射字段时，可以使用索引检索特定值。 为此，请使用`ATTRIBUTE`源类型和要映射的值的索引。 以下是此映射的示例：

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

**转换的数据**

```json
{
    "pi": {
        "email": "js@example.com"
    }
}
```

### 数组到数组或对象到对象

使用`ATTRIBUTE`源类型，还可以将数组直接映射到数组，或将对象映射到对象。 以下是此映射的示例：

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

### 对数组进行迭代操作

使用`ATTRIBUTE`源类型，您可以反复循环使用数组，并通过使用通配符索引(`[*]`)将它们映射到目标模式。 以下是此映射的示例：

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

如果要映射常量或静态值，请使用`STATIC`源类型。  使用`STATIC`源类型时，`source`表示要分配给`destination`的硬编码值。 以下是此映射的示例：

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

**转换的数据**

```json
{
    "userType:": "CUSTOMER"
}
```

### 表达式

如果要映射表达式，请使用`EXPRESSION`源类型。 [映射函数指南](./functions.md)中可找到已接受函数的列表。 使用`EXPRESSION`源类型时，`source`表示要解析的函数。 以下是此映射的示例：

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

**转换的数据**

```json
{
    "pi": {
        "created": "SMITHJOHNFri Sep 25 15:17:31 PDT 2020"
    }
}
```

## 配置映射目标

在映射中，`destination`是将插入从`source`提取的值的位置。

### 根级别的字段

当要将`source`值映射到转换后数据的根级别时，请遵循以下示例：

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

**转换的数据**

```json
{
    "name": "John Smith"
}
```

### 嵌套字段

当要将`source`值映射到转换后数据中的嵌套字段时，请遵循以下示例：

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

**转换的数据**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### 特定数组索引处的字段

当要将`source`值映射到转换后数据中数组中的特定索引时，请遵循以下示例：

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

**转换的数据**

```json
{
    "piList": ["John Smith"]
}
```

### 迭代数组操作

如果要迭代循环遍历数组并将值映射到目标，可以使用通配符索引(`[*]`)。 下面可以看到此示例：

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

通过阅读此文档，您现在应该了解如何构建映射集，包括如何在映射集内配置单个映射。 有关其他数据准备功能的详细信息，请阅读[数据准备概述](./home.md)。 要了解如何使用数据准备API中的映射集，请阅读[数据准备开发人员指南](./api/overview.md)。