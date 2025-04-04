---
title: 重试失败的数据流运行
description: 了解如何使用流服务API重试失败的数据流运行。
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 2%

---

# 重试失败的数据流运行

>[!IMPORTANT]
>
>对重试失败的数据流运行支持适用于批处理源。 您只能重试失败的数据流运行。

本教程介绍有关如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)重试失败的数据流运行的步骤。

## 快速入门

本教程要求您实际了解Adobe Experience Platform的以下组件：

* [源](../../home.md)： Experience Platform允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../sandboxes/home.md)： Experience Platform提供了将单个[!DNL Experience Platform]实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../landing/api-guide.md)指南。

## 重试失败的数据流运行

要重试失败的数据流运行，请在提供数据流的运行ID以及`re-trigger`操作作为查询参数的一部分时，向`/runs`端点发出POST请求。

**API格式**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| 参数 | 描述 |
| --- | --- |
| `{RUN_ID}` | 与要重试的数据流运行对应的运行ID。 |
| `op` | 确定要执行的操作的操作。 要重试失败的数据流运行，必须指定`re-trigger`作为您的操作。 |

**请求**

>[!NOTE]
>
>鉴于成功的数据流运行没有引入记录，您也可以使用`re-trigger`操作重试成功的数据流运行。

以下请求为运行ID `4fb0418e-1804-45d6-8d56-dd51f05c0baf`重试数据流运行。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs/4fb0418e-1804-45d6-8d56-dd51f05c0baf/action?op=re-trigger' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
```

**响应**

成功的响应会返回新创建的流运行ID及其对应的电子标记版本。

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
