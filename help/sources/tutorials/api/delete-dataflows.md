---
keywords: Experience Platform；主页；热门主题；流服务；API；API；删除；删除数据流
solution: Experience Platform
title: 使用流服务API删除数据流
type: Tutorial
description: 了解如何使用流服务API删除批处理数据流和流式数据流。
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 2%

---

# 使用流服务API删除数据流

您可以使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)删除包含错误或已过期的批处理数据流和流式数据流。

本教程介绍如何使用[!DNL Flow Service]删除通过批处理源和流源创建的数据流的步骤。

## 快速入门

本教程要求您拥有有效的流ID。 如果您没有有效的流ID，请从[源概述](../../home.md)中选择您选择的连接器，并按照尝试本教程之前概述的步骤操作。

本教程还要求您实际了解Adobe Experience Platform的以下组件：

* [源](../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../landing/api-guide.md)指南。

## 删除数据流

使用现有的流ID，您可以通过对[!DNL Flow Service] API执行DELETE请求来删除数据流。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 要删除的数据流的唯一`id`值。 |

**请求**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容）和一个空白正文。 您可以通过尝试向数据流发送查找(GET)请求来确认删除。 该API将返回HTTP 404（未找到）错误，指示数据流已被删除。

## 后续步骤

通过完成本教程，您已成功使用[!DNL Flow Service] API删除现有数据流。

有关如何使用用户界面执行这些操作的步骤，请参阅有关[在UI中删除数据流](../../tutorials/ui/delete.md)的教程
