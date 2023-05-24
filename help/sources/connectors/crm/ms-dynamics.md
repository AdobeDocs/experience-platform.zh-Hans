---
keywords: Experience Platform；首頁；熱門主題；Microsoft Dynamics；microsoft dynamics；Dynamics；Dynamics
solution: Experience Platform
title: Microsoft Dynamics來源聯結器總覽
description: 瞭解如何使用API或使用者介面將Microsoft Dynamics連線至Adobe Experience Platform。
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# Microsoft Dynamics 连接器

Adobe Experience Platform可從外部來源擷取資料，同時讓您能夠使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

[!DNL Experience Platform] 支援從協力廠商CRM系統擷取資料。 CRM提供者的支援包括 [!DNL Microsoft Dynamics].

## IP位址允許清單

在使用來源聯結器之前，必須將IP位址清單新增至允許清單。 使用來源時，若未將您地區專屬的IP位址新增至允許清單，可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 欄位對應來源 [!DNL Microsoft Dynamics] 至XDM

若要建立來源連線，請執行下列步驟： [!DNL Microsoft Dynamics] 和Platform， [!DNL Microsoft Dynamics] 來源資料欄位必須先對應到適當的目標XDM欄位，才能內嵌至Platform。

如需以下欄位對應規則的詳細資訊，請參閱下列內容： [!DNL Microsoft Dynamics] 資料集和平台：

- [連絡人](../adobe-applications/mapping/dynamics.md#contacts)
- [銷售機會](../adobe-applications/mapping/dynamics.md#leads)
- [帐户](../adobe-applications/mapping/dynamics.md#accounts)
- [機會](../adobe-applications/mapping/dynamics.md#opportunities)
- [機會聯絡人角色](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [营销活动](../adobe-applications/mapping/dynamics.md#campaigns)
- [行銷清單](../adobe-applications/mapping/dynamics.md#marketing-list)
- [行銷清單成員](../adobe-applications/mapping/dynamics.md#marketing-list-members)

以下檔案提供有關如何連線的資訊 [!DNL Microsoft Dynamics] 至 [!DNL Platform] 使用API或使用者介面：

## Connect [!DNL Microsoft Dynamics] 至 [!DNL Platform] 使用API

- [使用Flow Service API建立Microsoft Dynamics基本連線](../../tutorials/api/create/crm/ms-dynamics.md)
- [使用Flow Service API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流量服務API為CRM來源建立資料流](../../tutorials/api/collect/crm.md)

## Connect [!DNL Microsoft Dynamics] 至 [!DNL Platform] 使用UI

- [在使用者介面中建立Microsoft Dynamics來源連線](../../tutorials/ui/create/crm/dynamics.md)
- [在UI中為CRM連線建立資料流](../../tutorials/ui/dataflow/crm.md)
