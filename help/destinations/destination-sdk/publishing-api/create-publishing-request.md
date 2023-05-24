---
description: 瞭解如何格式化API呼叫，以透過Adobe Experience Platform Destination SDK提交目的地發佈請求。
title: 建立目的地發佈請求
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---


# 建立目的地發佈請求

>[!IMPORTANT]
>
>只有在您提交產品化（公用）目的地以供其他Experience Platform客戶使用時，才需要使用此API端點。 如果您要建立私人目的地以供自己使用，則不需要使用發佈API正式提交目的地。

>[!IMPORTANT]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/destinations/publish`

設定並測試目的地後，您可以將其提交至Adobe以供稽核和發佈。 讀取 [提交以Destination SDK撰寫的目的地，以供複查](../guides/submit-destination.md) 至於所有其他步驟，您必須在目的地提交程式中執行。

在下列情況下，使用發佈目的地API端點提交發佈請求：

* 身為Destination SDK合作夥伴，您想要讓所有Experience Platform組織都能提供已生產化的目的地，以供所有Experience Platform客戶使用；
* 您製作 *任何更新* 至您的設定。 只有在您提交經Experience Platform團隊核准的新發佈請求後，設定更新才會反映在目的地中。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值皆為 **區分大小寫**. 為避免區分大小寫錯誤，請完全按照檔案中所示使用引數名稱和值。

## Destination Publishing API操作快速入門 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 如需成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 提交目標設定以進行發佈 {#create}

您可以透過向發出POST請求來提交要發佈的目的地設定 `/authoring/destinations/publish` 端點。

**API格式**

```http
POST /authoring/destinations/publish
```

+++请求

以下請求會針對由裝載中提供的引數所設定的組織，提交要發佈的目的地。 以下裝載包含 `/authoring/destinations/publish` 端點。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"ALL"
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `destinationId` | 字符串 | 您要提交以進行發佈的目的地設定的目的地ID。 使用取得目的地設定的目的地ID [擷取目的地設定](../authoring-api/destination-configuration/retrieve-destination-configuration.md) API呼叫。 |
| `destinationAccess` | 字符串 | 使用 `ALL` ，讓您的目的地出現在所有Experience Platform客戶的目錄中。 |

{style="table-layout:auto"}

+++响应

成功的回應會傳回HTTP狀態201以及目的地發佈請求的詳細資料。

## API錯誤處理

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

## 后续步骤

閱讀本檔案後，您現在知道如何提交目的地的發佈請求。 Adobe Experience Platform團隊將在五個工作日內稽核您的發佈請求並回覆您。