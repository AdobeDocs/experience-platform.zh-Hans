---
description: 此頁面是用來透過Adobe Experience Platform Destination SDK刪除現有目的地伺服器設定的API呼叫的範例。
title: 刪除目的地伺服器設定
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 2%

---


# 刪除目的地伺服器設定

此頁面以範例說明可用來刪除現有目的地伺服器設定的API請求和裝載，使用 `/authoring/destination-servers` api端點。

如需可透過此端點刪除的功能的詳細說明，請閱讀以下文章：

* [以Destination SDK建立的目的地的伺服器規格](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [以Destination SDK建立的目的地的範本規格](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [消息格式](../../../destination-sdk/functionality/destination-server/message-format.md)
* [檔案格式設定](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值皆為 **區分大小寫**. 為避免區分大小寫錯誤，請完全按照檔案中所示使用引數名稱和值。

## 開始使用目的地伺服器API作業 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 如需成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 刪除目的地伺服器設定 {#delete}

您可以刪除 [現有](create-destination-server.md) 目標伺服器設定，方法是將 `DELETE` 向以下專案提出的請求： `/authoring/destination-servers` 端點與 `{INSTANCE_ID}`要刪除的目的地伺服器組態。

>[!TIP]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/destination-servers`

若要取得現有的目的地伺服器組態及其對應的 `{INSTANCE_ID}`，請參閱這篇文章，瞭解 [擷取目的地伺服器組態](retrieve-destination-server.md).

**API格式**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 此 `ID` 要刪除的目的地伺服器組態。 |

+++请求

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++响应

成功的回應會傳回HTTP狀態200以及空的HTTP回應。

## API錯誤處理 {#error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

## 后续步骤 {#next-steps}

閱讀本檔案後，您現在知道如何透過Destination SDK刪除現有的目的地伺服器 `/authoring/destination-servers` api端點。

若要進一步瞭解您可以使用此端點做什麼，請參閱下列文章：

* [建立目的地伺服器設定](create-destination-server.md)
* [擷取目的地伺服器設定](retrieve-destination-server.md)
* [更新目的地伺服器設定](update-destination-server.md)

