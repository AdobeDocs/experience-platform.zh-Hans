---
keywords: Experience Platform;home;popular topics;flow service;delete accounts;delete;api
solution: Experience Platform
title: Delete an Account Using the Flow Service API
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API删除帐户。
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 95f455bd03b7baefe0133a9818c9d048f36f9d38
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# Delete an account using the Flow Service API

您可以删除包含错误或已在使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

See the following tutorial for steps on how to delete an account using the API.

## 快速入门

本教程要求您具有有效的连接ID。 If you do not have a valid connection ID, select your connector of choice from the [sources overview](../../home.md) and follow the steps outlined before attempting this tutorial.

This tutorial also requires you to have a working understanding of the following components of Adobe Experience Platform:

* [源](../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] provides virtual sandboxes which partition a single [!DNL Platform] instance into separate virtual environments to help develop and evolve digital experience applications.

### 使用Platform API

For information on how to successfully make calls to Platform APIs, see the guide on [getting started with Platform APIs](../../../landing/api-guide.md).

## 删除帐户

>[!TIP]
>
>在删除源帐户之前，必须首先删除与源帐户关联的任何现有数据流。 要删除现有数据流，请参阅 [删除源数据流](./delete-dataflows.md).

要删除帐户，请向 [!DNL Flow Service] API，同时提供与要删除的帐户对应的基本连接ID。

**API format**

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

A successful response returns HTTP status 204 (No Content) and a blank body.

You can confirm the deletion by attempting a lookup (GET) request to the connection.

## 后续步骤

By following this tutorial, you have successfully used the [!DNL Flow Service] API to delete existing accounts.

有关如何使用用户界面执行这些操作的步骤，请参阅 [在UI中删除帐户](../../tutorials/ui/delete-accounts.md).
