---
keywords: IP位址、IP範圍、允許清單目的地、允許清單
title: 雲端儲存空間目的地的IP位址允許清單
type: Documentation
description: 此頁面提供您可新增至允許清單的IP範圍，以便安全地從Experience Platform匯出資料至SFTP伺服器、Amazon S3或Azure Blob儲存體。
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: c4d8ae6de2e1bbf23a25a66bde5dc88c13a13402
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 雲端儲存空間目的地的IP位址允許清單 {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe建議您將此頁面加入書籤，每三個月重新造訪一次，以檢查最新的IP位址。 Adobe不提供新IP範圍的通知。
> * 雖然Adobe支援將資料匯出至SFTP伺服器，但建議匯出資料的雲端儲存位置為 [!DNL Amazon S3] 和 [!DNL Azure Blob].


## 概述 {#overview}

此頁面提供您可新增至允許清單的IP範圍，以便安全地從Experience Platform匯出資料至您的 [SFTP伺服器](./sftp.md).

您可以透過網路防火牆定義網路存取控制。 透過指定適當的IP範圍，您可以允許資料傳輸服務的流量。

Adobe建議您在使用雲端儲存空間目的地連線之前，先將下列IP範圍新增至允許清單。 使用雲端儲存體目的地連線時，如果無法將您區域專屬的IP範圍新增至允許清單，可能會導致錯誤或效能不佳。

## 所有客戶均需要

* `52.247.108.70`

## 美國客戶

* `52.252.71.64/29`

## EMEA客戶

* `51.137.8.208/29`

## APAC客戶

* `20.53.201.168/29`
