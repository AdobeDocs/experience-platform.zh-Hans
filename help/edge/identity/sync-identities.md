---
title: 使用Platform Web SDK在Audience Manager和Adobe Experience Platform之間同步身分
description: 瞭解如何使用Platform Web SDK在Audience Manager和Adobe Experience Platform之間同步身分
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager；aam；身分；同步身分；名稱空間；
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# 在Audience Manager和Experience Platform之間同步身分

Adobe Experience Platform Web SDK支援透過 [sendEvent](./overview.md#syncing-identities) 命令。

從中選擇您的名稱空間 [Identity Service名稱空間](../../identity/../identity-service/namespaces.md) 若要指示與身分相關的內容，請使用「身分符號」欄中的值：

![名稱空間UI的檢視](../assets/identity/edge_namespaceUI_identity-symbol.png)

身為Audience Manager客戶，您所有使用ID型別：跨裝置的現有資料來源都會自動擁有對應的身分名稱空間。 若要尋找Audience Manager資料來源對應的身分名稱空間，請登入Adobe Experience Platform並導覽至「身分」區段。

任何新增 [!DNL Audience Manager] 使用ID型別的資料來源：跨裝置將產生對應的身分名稱空間。 目前不支援資料來源ID型別Cookie和裝置廣告ID。 此外，在Adobe Experience Platform中建立的任何身分名稱空間都會產生相應的 [!DNL Audience Manager] 資料來源，但請注意，syncIdentity方法僅支援名稱空間身分識別符號。
