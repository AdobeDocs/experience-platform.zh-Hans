---
keywords: Experience Platform；首頁；熱門主題；流程服務；API；API；刪除；刪除資料流程
solution: Experience Platform
title: 使用流量服務API刪除資料流
type: Tutorial
description: 瞭解如何使用流量服務API刪除批次和串流資料流。
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 2%

---

# 使用流量服務API刪除資料流

您可以使用來刪除包含錯誤或已過時的批次和串流資料流。 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

本教學課程涵蓋刪除使用批次和串流來源建立的資料流的步驟，這些資料流使用 [!DNL Flow Service].

## 快速入门

本教學課程要求您具備有效的流量ID。 如果您沒有有效的流量ID，請從「 」中選擇您選擇的聯結器 [來源概觀](../../home.md) 並依照在嘗試本教學課程之前概述的步驟進行。

本教學課程也要求您實際瞭解Adobe Experience Platform的下列元件：

* [來源](../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../landing/api-guide.md).

## 刪除資料流

有了現有的流量ID，您可以透過對執行DELETE請求來刪除資料流 [!DNL Flow Service] API。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FLOW_ID}` | 唯一 `id` 您要刪除之資料流的值。 |

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

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。 您可以嘗試對資料流進行查詢(GET)請求以確認刪除。 API將傳回HTTP 404 （找不到）錯誤，這表示資料流已刪除。

## 后续步骤

依照本教學課程，您已成功使用 [!DNL Flow Service] 要刪除現有資料流的API。

如需如何使用使用者介面執行這些操作的步驟，請參閱以下教學課程： [在UI中刪除資料流](../../tutorials/ui/delete.md)
