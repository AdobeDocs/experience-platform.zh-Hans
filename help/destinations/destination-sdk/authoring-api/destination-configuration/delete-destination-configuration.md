---
description: 此頁面是用來透過Adobe Experience Platform Destination SDK刪除現有目的地設定的API呼叫的範例。
title: 刪除目的地設定
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 2%

---


# 刪除目的地設定

此頁面透過以下範例說明您可用來刪除現有目的地設定的API請求和裝載： `/authoring/destinations` api端點。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值皆為 **區分大小寫**. 為避免區分大小寫錯誤，請完全按照檔案中所示使用引數名稱和值。

## 目的地設定API操作快速入門 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 如需成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 刪除目的地設定 {#delete}

您可以刪除 [現有](create-destination-configuration.md) 目標伺服器設定，方法是將 `DELETE` 向以下專案提出的請求： `/authoring/destinations` 端點與 `{INSTANCE_ID}`要刪除的目的地組態。

>[!TIP]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/destinations`

若要取得現有的目的地組態及其對應的 `{INSTANCE_ID}`，請參閱這篇文章，瞭解 [擷取目的地設定](retrieve-destination-configuration.md).

**API格式**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 此 `ID` 要刪除的目的地組態。 |

+++请求

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++响应

成功的回應會傳回HTTP狀態200以及空的HTTP回應。


## API錯誤處理 {#error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

## 后续步骤

閱讀本檔案後，您現在知道如何透過Destination SDK刪除現有的目的地設定 `/authoring/destinations` api端點。

若要進一步瞭解您可以使用此端點做什麼，請參閱下列文章：

* [建立目的地設定](create-destination-configuration.md)
* [擷取目的地設定](retrieve-destination-configuration.md)
* [更新目的地設定](update-destination-configuration.md)

