---
description: 此頁面是用來透過Adobe Experience Platform Destination SDK刪除現有對象範本的API呼叫的範例。
title: 刪除對象範本
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---


# 刪除對象範本

>[!IMPORTANT]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/audience-templates`

此頁面以範例說明可用來刪除對象範本的API請求和裝載，使用 `/authoring/audience-templates` api端點。

如需可透過此端點設定的功能的詳細說明，請參閱 [對象中繼資料管理](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值皆為 **區分大小寫**. 為避免區分大小寫錯誤，請完全按照檔案中所示使用引數名稱和值。

## 開始使用對象範本API作業 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 如需成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 刪除對象範本 {#delete}

您可以刪除 [現有](create-audience-template.md) 對象範本，做法是建立 `DELETE` 向以下專案提出的請求： `/authoring/audience-templates` 端點與 `{INSTANCE_ID}`要刪除的對象範本的URL。

若要取得現有的對象範本及其對應的 `{INSTANCE_ID}`，請參閱這篇文章，瞭解 [擷取對象範本](retrieve-audience-template.md).

**API格式**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 此 `ID` 要刪除的對象範本的URL。 |

+++请求

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++响应

成功的回應會傳回HTTP狀態200以及空的HTTP回應。

+++

## API錯誤處理 {#error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

## 后续步骤 {#next-steps}

閱讀本檔案後，您現在知道如何使用 `/authoring/audience-templates` api端點。 讀取 [如何使用Destination SDK設定您的目的地](../guides/configure-destination-instructions.md) 以瞭解此步驟在設定目的地的程式中的適用位置。
