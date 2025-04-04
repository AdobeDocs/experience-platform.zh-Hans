---
keywords: Experience Platform；主页；热门主题；流服务；删除帐户；删除；API
solution: Experience Platform
title: 使用流服务API删除帐户
type: Tutorial
description: 了解如何使用流服务API删除帐户。
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# 使用流服务API删除帐户

您可以使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)删除包含错误或已过期的源帐户。

有关如何使用API删除帐户的步骤，请参阅以下教程。

## 快速入门

本教程要求您具有有效的连接ID。 如果您没有有效的连接ID，请从[源概述](../../home.md)中选择您选择的连接器，并按照尝试本教程之前概述的步骤操作。

本教程还要求您实际了解Adobe Experience Platform的以下组件：

* [源](../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../landing/api-guide.md)指南。

## 删除帐户

>[!TIP]
>
>在删除源帐户之前，必须首先删除与源帐户关联的任何现有数据流。 要删除现有数据流，请参阅有关[删除源数据流](./delete-dataflows.md)的教程。

要删除帐户，请提供与要删除的帐户对应的基本连接ID时，向[!DNL Flow Service] API发出DELETE请求。

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

您可以通过尝试向连接发送查找(GET)请求来确认删除。

## 后续步骤

通过完成本教程，您已成功使用[!DNL Flow Service] API删除现有帐户。

有关如何使用用户界面执行这些操作的步骤，请参阅有关在UI](../../tutorials/ui/delete-accounts.md)中删除[帐户的教程。
