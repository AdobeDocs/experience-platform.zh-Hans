---
keywords: Experience Platform；首頁；熱門主題；流量服務；刪除帳戶；刪除；api
solution: Experience Platform
title: 使用流程服務API刪除帳戶
type: Tutorial
description: 瞭解如何使用Flow Service API刪除帳戶。
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# 使用流程服務API刪除帳戶

您可以使用刪除包含錯誤或已過時的來源帳戶 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

請參閱下列教學課程，以瞭解如何使用API刪除帳戶的步驟。

## 快速入门

本教學課程要求您具備有效的連線ID。 如果您沒有有效的連線ID，請從 [來源概觀](../../home.md) 並依照在嘗試本教學課程之前概述的步驟進行。

本教學課程也要求您實際瞭解Adobe Experience Platform的下列元件：

* [來源](../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../landing/api-guide.md).

## 刪除帳戶

>[!TIP]
>
>在刪除來源帳戶之前，您必須先刪除與來源帳戶關聯的任何現有資料流。 若要刪除現有的資料流，請參閱上的教學課程 [刪除來源資料流](./delete-dataflows.md).

若要刪除帳戶，請向發出DELETE要求 [!DNL Flow Service] API，同時提供與您要刪除的帳戶對應的基本連線ID。

**API格式**

```http
DELETE /connections/{BASE_CONNECTION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 您要刪除之來源帳戶的基本連線ID。 |

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

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。

您可以嘗試向連線查詢(GET)要求以確認刪除。

## 后续步骤

依照本教學課程，您已成功使用 [!DNL Flow Service] 用於刪除現有帳戶的API。

如需如何使用使用者介面執行這些操作的步驟，請參閱以下教學課程： [在UI中刪除帳戶](../../tutorials/ui/delete-accounts.md).
