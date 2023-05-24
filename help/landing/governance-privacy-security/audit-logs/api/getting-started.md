---
title: 開始使用稽核查詢API
description: 稽核查詢API可讓您擷取各種Adobe Experience Platform功能的量度資料。 本檔案會介紹您在嘗試呼叫Audit Query API之前需要瞭解的核心概念。
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 9%

---

# 開始使用稽核查詢API

Adobe Experience Platform可讓您以稽核事件記錄檔的形式，稽核各種服務和功能的使用者活動。 日志中记录的每个操作都包含元数据，这些元数据可指示操作类型、日期和时间、执行操作的用户的电子邮件 ID 以及与操作类型相关的其他属性。

稽核查詢API可讓您以稽核事件記錄檔的形式，稽核各種服務和功能的使用者活動。 本檔案會介紹您在嘗試呼叫Audit Query API之前需要瞭解的核心概念。

## 先决条件

若要管理稽核事件，您必須擁有 **[!UICONTROL 檢視使用者活動記錄]** 已授予存取控制許可權(可在 [!UICONTROL 資料控管] 類別)。 若要瞭解如何管理Platform功能的個別許可權，請參閱 [存取控制檔案](../../../../access-control/home.md).

### 讀取範例API呼叫

本指南提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑難排解指南中。

### 收集必要標題的值

本指南會要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 才能成功呼叫平台API。 完成驗證教學課程後，會提供所有Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

* 授權：持有人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱。 如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

包含裝載(POST、PUT和PATCH)的所有請求都需要額外的標頭：

* Content-Type： application/json

## 后续步骤

若要開始使用進行呼叫 [!DNL Audit Query] API，請參閱 [事件端點指南](./events.md) 和 [匯出端點指南](./export.md).
