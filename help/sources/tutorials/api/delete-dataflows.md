---
keywords: Experience Platform；主页；热门主题；流程服务；API;API；删除；删除数据流
solution: Experience Platform
title: 使用流服务API删除数据流
topic-legacy: overview
type: Tutorial
description: 了解如何使用流服务API删除批处理数据流和流数据流。
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 2%

---

# 使用流服务API删除数据流

您可以删除包含错误或已在使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

本教程介绍了如何使用 [!DNL Flow Service].

## 快速入门

本教程要求您拥有有效的流程ID。 如果您没有有效的流量ID，请从 [源概述](../../home.md) ，然后按照在尝试使用本教程之前列出的步骤操作。

此外，本教程还要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).

## 删除数据流

使用现有的流ID，您可以通过对执行DELETE请求来删除数据流 [!DNL Flow Service] API。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 独特 `id` 值。 |

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

成功响应会返回HTTP状态204（无内容）和空白正文。 您可以通过尝试对数据流进行查找(GET)请求来确认删除。 该API将返回HTTP 404（未找到）错误，表示数据流已被删除。

## 后续步骤

通过阅读本教程，您已成功使用 [!DNL Flow Service] 用于删除现有数据流的API。

有关如何使用用户界面执行这些操作的步骤，请参阅 [删除UI中的数据流](../../tutorials/ui/delete.md)
