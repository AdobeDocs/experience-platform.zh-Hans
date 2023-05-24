---
title: Data Lake移轉至Gen2
description: 瞭解將Data Lake移轉至Adobe Experience Platform中的Gen2所提供的新功能。
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Adobe Experience Platform Data Lake移轉至Gen2

Adobe Experience Platform正在移轉至Gen2 Data Lake。 這是新一代的資料湖，可為Platform使用者提供地理區域複製、更精細的角色型存取控制(RBAC)和更好的擴充等多項優勢。

## 使用者影響

當Adobe將Data Lake從Gen1移轉至Gen 2時，使用者將能夠 **讀取** 來自Data Lake，但所有 **寫入** 資料湖中的區段將會受到影響。 以下是受影響的功能清單：

- **來源**：來自來源和各種資料擷取工作流程的資料將延遲。 移轉完成後，使用者將看到其資料。
- **查詢服務**：使用者可以執行查詢，但無法將查詢輸出寫入資料集。
- **即時客戶個人檔案**：透過擷取至設定檔存放區的資料 **批次** 移轉期間將無法使用內嵌。 不過，資料擷取自 **串流** 內嵌作業將在移轉期間提供。 此外，在移轉期間將無法使用設定檔匯出。
- **資料科學工作區**：從Data Science Workspace寫入將會失敗。
- **細分服務**：衍生自下列專案的對象： **批次** 移轉期間無法啟用分段。 衍生自的對象 **串流** 區段不受影響。
- **Customer Journey Analytics**：Customer Journey Analytics報表資料可能已過期，移轉期間不會重新整理，因為批次未擷取至Data Lake。

## 與Platform使用者的通訊

Adobe將會聯絡系統管理員，詳細討論移轉的影響，並確認特定組織的移轉日期和時間。
