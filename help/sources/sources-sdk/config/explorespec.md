---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK；SDK
title: 为自助源配置浏览规范(Batch SDK)
description: 本文档概述了要使用自助源(Batch SDK)需要准备的配置。
exl-id: 423a7e56-9dd1-4071-bd26-ee4f9f206122
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 1%

---

# 为自助源配置浏览规范(Batch SDK)

浏览规范定义浏览和检查源中包含的对象所需的参数。 浏览规范还定义了浏览和检查对象时返回的响应格式。

>[!TIP]
>
>浏览规范是硬编码的，您只需将以下有效负载复制并粘贴到连接规范中即可。

```json
"exploreSpec": {
  "name": "Resource",
  "type": "Resource",
  "requestSpec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object"
  },
  "responseSpec": {
    "$schema": "http: //json-schema.org/draft-07/schema#",
    "type": "object",
    "properties": {
      "format": {
        "type": "string"
      },
      "schema": {
        "type": "object",
        "properties": {
          "columns": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string"
                },
                "type": {
                  "type": "string"
                }
              }
            }
          }
        }
      },
      "data": {
        "type": "array",
        "items": {
          "type": "object"
        }
      }
    }
  }
}
```

| 浏览规范 | 描述 | 示例 |
| --- | --- | --- |
| `name` | 定义浏览规格的名称或标识符。 | `Resource` |
| `type` | 定义浏览规范的类型。 | `Resource` |
| `requestSpec` | 包含浏览连接中的对象所需的参数。 |
| `requestSpec.type` | 定义请求规范的数据类型。 | `object` |
| `responseSpec` | 包含定义针对浏览调用返回的响应消息的格式的参数。 |
| `responseSpec.type` | 定义响应规范的数据类型。 | `object` |
| `responseSpec.properties` | 包含与响应消息的格式相关的信息。 |
| `responseSpec.properties.format` | 定义响应架构的格式。 | `object` |
| `responseSpec.properties.format.type` | 定义属性的数据类型。 | `string` |
| `responseSpec.schema` | 包含与响应架构的格式相关的信息。 |
| `responseSpec.schema.type` | 定义架构的数据类型。 | `object` |
| `responseSpec.schema.properties` | 包含有关架构中保留的列、类型和项目的信息。 |
| `responseSpec.schema.properties.columns.items.properties.name` | 显示文件的名称。 |
| `responseSpec.schema.properties.columns.items.properties.name.type` | 定义文件名的数据类型。 | `string` |

{style="table-layout:auto"}

## 后续步骤

填充浏览规范后，您可以使用 [!DNL Flow Service] API。 请参见 [自助式源(Batch SDK) API指南](../api/api-overview.md) 了解更多信息。
