---
keywords: Experience Platform；首頁；熱門主題；流量服務；
title: 重試失敗的資料流執行
description: 本教學課程涵蓋如何使用流量服務API重試失敗的資料流執行的步驟
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 2%

---

# 重試失敗的資料流執行

>[!IMPORTANT]
>
>批次來源可支援重試失敗的資料流執行。 您只能重試失敗的資料流執行。

本教學課程涵蓋如何使用重試失敗的資料流執行的步驟。 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本教學課程需要您實際瞭解Adobe Experience Platform的下列元件：

* [來源](../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../landing/api-guide.md).

## 重試失敗的資料流執行

若要重試失敗的資料流執行，請向發出POST要求 `/runs` 端點，同時提供資料流的執行ID和 `re-trigger` 作業做為查詢引數的一部分。

**API格式**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| 参数 | 描述 |
| --- | --- |
| `{RUN_ID}` | 與您要重試的資料流執行對應的執行ID。 |
| `op` | 決定要執行之動作的作業。 若要重試失敗的資料流執行，您必須指定 `re-trigger` 作為您的作業。 |

**请求**

以下要求會重試針對執行ID執行的資料流 `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

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

成功的回應會傳回新建立的流程執行ID及其對應的etag版本。

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
