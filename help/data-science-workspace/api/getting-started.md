---
keywords: Experience Platform；開發人員指南；端點；資料科學工作區；熱門主題；資料科學工作區；資料科學
solution: Experience Platform
title: Sensei Machine Learning API指南
description: Sensei機器學習API可讓開發人員對各種資料科學工作區資源執行CRUD操作。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 9%

---

# [!DNL Sensei Machine Learning] API指南

此 [!DNL Sensei Machine Learning] API為資料科學家提供了一種機制，可用於組織和管理機器學習服務，從演演算法上線到實驗，再到服務部署。

本開發人員指南提供步驟，協助您開始使用 [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)、和示範對各種資料科學工作區資源執行CRUD作業的API呼叫。

## 快速入门

您必須完成 [驗證](https://www.adobe.com/go/platform-api-authentication-en) 教學課程，以便存取以下請求標頭來呼叫 [!DNL Adobe Experience Platform] API：

* 授權：持有人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的標頭：

* Content-Type： application/json

## 后续步骤

收集完所需的驗證認證後，您可以繼續參閱本開發人員指南的後續章節，以取得對以下端點群組的範例API呼叫：

* [引擎](./engines.md)
* [實驗](./experiments.md)
* [见解](./insights.md)
* [MLInstances （配方）](./mlinstances.md)
* [MLServices](./mlservices.md)
* [模型](./models.md)
* [附录](./appendix.md)
