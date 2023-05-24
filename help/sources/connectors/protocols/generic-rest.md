---
keywords: Experience Platform；首頁；熱門主題；一般REST；一般rest
solution: Experience Platform
title: 一般REST API來源聯結器概述
description: 瞭解如何使用API或使用者介面將Generic REST API連線到Adobe Experience Platform。
exl-id: e3449e33-7261-4aa2-bce9-5530eb4fcc68
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# (Beta) [!DNL Generic REST API]

>[!NOTE]
>
>此 [!DNL Generic REST API] 來源為測試版。 請參閱 [來源概觀](../../home.md#terms-and-conditions) 以取得使用Beta標籤聯結器的詳細資訊。

Adobe Experience Platform可從外部來源擷取資料，同時讓您能夠使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Platform支援從通訊協定應用程式擷取資料，包括 [!DNL Generic REST API].

此 [!DNL Generic REST API] 來源可讓您將資料從REST型應用程式帶入Platform。 [!DNL Generic REST API] 支援基本驗證和OAuth 2重新整理程式碼型驗證。

## IP位址允許清單

在使用來源聯結器之前，必須將IP位址清單新增至允許清單。 使用來源時，若未將您地區專屬的IP位址新增至允許清單，可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

以下檔案提供如何連線的相關資訊 [!DNL Generic REST API] 使用API的平台原始碼。

## Connect [!DNL Generic REST API] 至 [!DNL Platform] 使用API

- [使用流程服務API建立一般REST API基本連線](../../tutorials/api/create/protocols/generic-rest.md)
- [使用Flow Service API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流量服務API為通訊協定來源建立資料流](../../tutorials/api/collect/protocols.md)
