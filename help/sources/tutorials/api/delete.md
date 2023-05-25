---
keywords: Experience Platform；主页；热门主题；流服务；删除帐户；删除；API
solution: Experience Platform
title: 使用流服务API删除帐户
type: Tutorial
description: 了解如何使用流服务API删除帐户。
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# 使用流服务API删除帐户

您可以使用删除包含错误或已过期的源帐户 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

有关如何使用API删除帐户的步骤，请参阅以下教程。

## 快速入门

本教程要求您拥有有效的连接ID。 如果您没有有效的连接ID，请从 [源概述](../../home.md) 并按照尝试阅读本教程之前概述的步骤操作。

本教程还要求您实际了解Adobe Experience Platform的以下组件：

* [源](../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../landing/api-guide.md).

## 删除帐户

>[!TIP]
>
>在删除源帐户之前，必须首先删除与源帐户关联的任何现有数据流。 要删除现有数据流，请参阅上的教程 [删除源数据流](./delete-dataflows.md).

DELETE要删除帐户，请向 [!DNL Flow Service] API，同时提供与要删除的帐户对应的基本连接ID。

**API格式**

```http
DELETE /connections/{BASE_CONNECTION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 要删除的源帐户的基本连接ID。 |

**请求**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容）和一个空白正文。

您可以通过尝试对连接进行查找(GET)请求来确认删除。

## 后续步骤

按照本教程中的说明，您已成功使用了 [!DNL Flow Service] 用于删除现有帐户的API。

有关如何使用用户界面执行这些操作的步骤，请参阅关于的教程 [在UI中删除帐户](../../tutorials/ui/delete-accounts.md).
