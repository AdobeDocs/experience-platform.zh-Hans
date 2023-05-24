---
keywords: Experience Platform；首頁；熱門主題；
title: (Beta) Mixpanel來源聯結器概觀
description: 瞭解如何使用API或使用者介面將Mixpanel連線至Adobe Experience Platform。
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: e44f6d5bb2fd891a3e3b3c5e4aed68e8d4687b53
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# (Beta) [!DNL Mixpanel]

>[!NOTE]
>
>此 [!DNL Mixpanel] 來源為測試版。 請參閱 [來源概觀](../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商Analytics應用程式擷取資料。 Analytics提供者的支援包括 [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) 是一款產品分析工具，可讓您擷取使用者與數位產品互動的相關資料。 Mixpanel可讓您使用簡單的互動式報表來分析此產品資料，讓您只需按幾下滑鼠即可查詢和視覺化資料。

來源會利用 [Mixpanel事件匯出API >下載](https://developer.mixpanel.com/reference/raw-event-export) 以下載您收到並儲存在中的事件資料 [!DNL Mixpanel]，以及所有事件屬性(包括 `distinct_id`)以及事件傳送至Experience Platform的確切時間戳記。 Mixpanel使用持有人權杖作為驗證機制，與Mixpanel事件匯出API通訊。

## IP位址允許清單

在使用來源聯結器之前，必須將IP位址清單新增至允許清單。 使用來源時，若未將您地區專屬的IP位址新增至允許清單，可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 驗證您的 [!DNL Mixpanel] 帳戶

本節概述驗證您的帳戶並帶上URL所需完成的先決條件步驟 [!DNL Mixpanel] 資料傳送至Platform。

為了建立 [!DNL Mixpanel] 來源連線和資料流，您必須先擁有有效的 [!DNL Mixpanel] 帳戶。 如果您沒有有效的 [!DNL Mixpanel] 帳戶，請參閱 [Mixpanel登入](https://mixpanel.com/register/) 頁面以建立您的帳戶。

當您成功建立 [!DNL Mixpanel] 帳戶，導覽至 [!DNL Project Details] 索引標籤中的 [!DNL Project Seettings] 第頁/ [!DNL Mixpanel] UI以擷取您的專案ID並設定您的時區。

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

接下來，導覽至 [!DNL Service Accounts] 索引標籤中的 [!DNL Project Settings] 中的頁面 [!DNL Mixpanel] 用於擷取您的服務帳戶憑證的UI。

>[!TIP]
>
>如需最佳實務，請選取服務帳戶， [不會過期](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Mixpanel服務帳戶](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

最後，建立平台 [綱要](../../../xdm/schema/composition.md) 以下專案需要 [!DNL Mixpanel Event Export API]. 如需結構描述所需對應的詳細資訊，請參閱以下指南中的 [建立 [!DNL Mixpanel] ui中的來源連線](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![建立結構描述](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Connect [!DNL Mixpanel] 使用API移至Platform

以下檔案提供有關如何連線的資訊 [!DNL Mixpanel] 使用API或使用者介面的to Platform：

* [建立來源連線和資料流，用於 [!DNL Mixpanel] 使用流量服務API](../../tutorials/api/create/analytics/mixpanel.md)

## Connect [!DNL Mixpanel] 使用UI移至Platform

* [建立 [!DNL Mixpanel] ui中的來源連線](../../tutorials/ui/create/analytics/mixpanel.md)
* [在UI中建立客戶成功來源連線的資料流](../../tutorials/ui/dataflow/analytics.md)
