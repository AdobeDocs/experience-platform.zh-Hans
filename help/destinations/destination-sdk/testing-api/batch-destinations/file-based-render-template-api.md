---
description: 此頁面說明如何使用/authoring/testing/template/render端點，以視覺效果呈現目的地設定中定義的範本化客戶資料欄位外觀。
title: 驗證範本化客戶欄位
exl-id: 8ed93f0c-3439-4d11-bb2f-d417a1e0b6a8
source-git-commit: 6bd169075cd3826ae2a0907e6e624fd901076a4a
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---


# 驗證範本化客戶欄位

## 概述 {#overview}

此 `/authoring/testing/template/render` 端點可協助您視覺化範本化的方式 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 目的地設定中定義的變數會很類似。

端點會為您的客戶資料欄位產生隨機值，並在回應中傳回這些值。 這可協助您驗證客戶資料欄位的語意結構，例如貯體名稱或資料夾路徑。

## 快速入门 {#getting-started}

在繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 如需成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 先决条件 {#prerequisites}

開始使用 `/template/render` 端點，確定您符合以下條件：

* 您有一個透過Destination SDK建立的檔案型目的地，且您可以在下列位置中看到 [目的地目錄](../../../ui/destinations-workspace.md).
* 若要成功提出API請求，您需要與要測試的目的地執行個體對應的目的地執行個體ID。 在Platform UI中瀏覽與目的地的連線時，從URL取得應在API呼叫中使用的目的地執行個體ID。

   ![UI影像顯示如何從URL取得目的地執行個體ID。](../../assets/testing-api/get-destination-instance-id.png)

## 呈現範本化客戶欄位 {#render-customer-fields}

**API格式**

```http
POST /authoring/testing/template/render/destination
```

為了說明此API端點的行為，讓我們考慮具有下列客戶資料欄位設定的檔案型目的地：

```json
"fileBasedS3Destination":{
   "bucket":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.bucket}}"
   },
   "path":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.path}}"
   }
}
```

**请求**

以下請求會呼叫 `/authoring/testing/template/render` 端點，它會針對上述兩個客戶資料欄位，以隨機產生的值傳回回應。

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render/destination' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "destinationId": "{DESTINATION_CONFIGURATION_ID}",
    "templates": {
        "bucket": "{{customerData.bucket}}",
        "path": "{{customerData.bucket}}/{{customerData.path}}"
    }
}'
```

| 参数 | 描述 |
| -------- | ----------- |
| `destinationId` | 的ID [目的地設定](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) 您正在測試的專案。 |
| `templates` | 在中定義的範本化欄位名稱 [目的地伺服器設定](../../authoring-api/destination-server/create-destination-server.md). |

**响应**

成功的回應會傳回 `HTTP 200 OK` 狀態，而內文則包含範本化欄位隨機產生的值。

此回應可協助您驗證客戶資料欄位的正確結構，例如貯體名稱或檔案夾路徑。


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

## 后续步骤 {#next-steps}

閱讀本檔案後，您現在瞭解如何驗證中定義的客戶資料欄位設定 [目的地伺服器](../../authoring-api/destination-server/create-destination-server.md).
