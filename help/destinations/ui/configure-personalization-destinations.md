---
keywords: 個人化；目標；目的地；個人化目的地；設定個人化目的地；相同頁面；下一頁；
title: 設定相同頁面和下一頁個人化的個人化目的地
type: Tutorial
description: 瞭解如何設定相同頁面和下一頁個人化的個人化目的地。
exl-id: 7d7b6869-bd59-4766-a044-f449396f6524
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# 設定相同頁面和下一頁個人化的個人化目的地

## 概述 {#overview}

>[!NOTE]
>
>時間 [設定Adobe Target連線](../catalog/personalization/adobe-target-connection.md) 若不使用資料串流ID，即不支援本文所述的使用案例。

Adobe Experience Platform使用 [邊緣細分](../../segmentation/ui/edge-segmentation.md) 可讓客戶即時大規模建立及鎖定受眾區段。

此功能可協助您設定相同頁面和下一頁個人化使用案例。

本文提供逐步指示，說明如何針對這些使用案例設定Experience Platform和個人化目的地。

此外，請觀看以下影片，瞭解端對端設定程式的概述。

>[!VIDEO](https://video.tv.adobe.com/v/340091/)

>[!NOTE]
>
>Experience Platform使用者介面經常更新，自從錄製此影片後，可能有所變更。 如需最新資訊，請參閱以下章節中所述的設定步驟。

## 步驟1：在資料收集UI中設定資料串流 {#configure-datastream}

設定個人化目的地的第一個步驟，是為Experience PlatformWeb SDK設定資料流。 這可在資料收集UI中完成。

設定資料串流時，在 **[!UICONTROL Adobe Experience Platform]** 請確定兩者 **[!UICONTROL 邊緣細分]** 和 **[!UICONTROL 個人化目的地]** 已選取。

![資料流設定](../assets/ui/configure-personalization-destinations/datastream-config.png)

如需如何設定資料串流的詳細資訊，請依照 [Platform Web SDK檔案](../../edge/datastreams/overview.md).

## 步驟2：設定您的個人化目的地 {#configure-destination}

設定資料串流後，您就可以開始設定個人化目的地。

請遵循 [目的地連線建立教學課程](../ui/connect-destination.md) 以取得有關如何建立新目的地連線的詳細說明。

根據您設定的目的地，請參閱下列文章以取得目的地特定先決條件及相關資訊：

* [Adobe Target連線](../catalog/personalization/adobe-target-connection.md)
* [自訂個人化連線](../catalog/personalization/custom-personalization.md)

## 步驟3：建立 [!DNL Active-On-Edge] 合併原則 {#create-merge-policy}

建立目的地連線後，您必須建立 [!DNL Active-On-Edge] 合併原則。

請依照以下說明操作： [建立合併原則](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)，並確保啟用 **[!UICONTROL Active-On-Edge合併原則]** 切換。

## 步驟4：在Platform中建立新區段 {#create-segment}

在您建立 [!DNL Active-On-Edge] 合併原則，您必須在Platform中建立新區段。

請遵循 [區段產生器](../../segmentation/ui/segment-builder.md) 指南來建立您的新區段，並確定 [指派它](../../segmentation/ui/segment-builder.md#merge-policies) 此 [!DNL Active-On-Edge] 您在步驟3建立的合併原則。

## 步驟5：對目的地啟用區段

設定程式的最後一個步驟是啟動您在步驟4中建立的區段至您在步驟2中建立的目的地。

若要這麼做，請遵循以下步驟 [啟動教學課程](../ui/activate-profile-request-destinations.md).

## 验证配置 {#validate-configuration}

成功執行上述步驟後，您應該會在個人化目的地中看到新區段。
