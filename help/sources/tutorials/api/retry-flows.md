---
keywords: Experience Platform；主页；热门主题；流服务；
title: 重试失败的数据流运行
description: 本教程介绍了有关如何使用流服务API重试失败的数据流运行的步骤
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 2%

---

# 重试失败的数据流运行

>[!IMPORTANT]
>
>批处理源支持重试失败的数据流运行。 您只能重试失败的数据流运行。

本教程介绍了有关如何使用重试失败的数据流运行的步骤 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本教程要求您实际了解Adobe Experience Platform的以下组件：

* [源](../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).

## 重试失败的数据流运行

要重试失败的数据流运行，请POST请求 `/runs` 端点，同时提供数据流的运行ID和 `re-trigger` 操作作为查询参数的一部分。

**API格式**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| 参数 | 描述 |
| --- | --- |
| `{RUN_ID}` | 与要重试的数据流运行对应的运行ID。 |
| `op` | 确定要执行的操作的操作。 要重试失败的数据流运行，必须指定 `re-trigger` 作为你的行动。 |

**请求**

以下请求将重试为运行ID运行的数据流 `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

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

成功的响应将返回新创建的流运行ID及其对应的etag版本。

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
