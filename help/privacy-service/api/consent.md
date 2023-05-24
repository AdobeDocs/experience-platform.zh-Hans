---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 同意API端點
description: 瞭解如何使用Privacy Service API管理Experience Cloud應用程式的客戶同意請求。
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 1%

---

# 同意端點

某些法規要求客戶明確同意才能收集其個人資料。 此 `/consent` 中的端點 [!DNL Privacy Service] API可讓您處理客戶同意請求，並將其整合至您的隱私權工作流程。

在使用本指南之前，請參閱 [快速入門](./getting-started.md) 指南，以瞭解有關以下範例API呼叫中顯示的所需驗證標頭的資訊。

## 處理客戶同意請求

處理同意請求的方式為向發出POST請求 `/consent` 端點。

**API格式**

```http
POST /consent
```

**请求**

以下請求會針對中提供的使用者ID建立新的同意工作 `entities` 陣列。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "optOutOfSale": true,
        "entities": [
          {
            "nameSpace": "email",
            "values": [
              "dsmith@acme.com",
              "ajones@acme.com"
            ]
          },
          {
            "nameSpace": "ECID",
            "values": [
              "443636576799758681021090721276"
            ]
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `optOutOfSale` | 若設為true，表示使用者提供在 `entities` 希望選擇退出銷售或分享其個人資料。 |
| `entities` | 表示同意要求套用至之使用者的物件陣列。 每個物件都包含 `namespace` 和陣列 `values` 將個別使用者與該名稱空間比對。 |
| `nameSpace` | 中的每一個物件 `entities` 陣列必須包含一個 [標準身分名稱空間](./appendix.md#standard-namespaces) 由Privacy ServiceAPI識別。 |
| `values` | 每個使用者的值陣列，對應提供的 `nameSpace`. |

{style="table-layout:auto"}

>[!NOTE]
>
>如需如何判斷要傳送至哪些客戶身分值的詳細資訊 [!DNL Privacy Service]，請參閱以下內容的相關指南： [提供身分資料](../identity-data.md).

**响应**

成功的回應會傳回HTTP狀態202 （已接受），而且沒有裝載，表示已接受要求 [!DNL Privacy Service] 且正在處理中。
