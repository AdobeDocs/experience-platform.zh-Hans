---
title: Adobe Experience Platform發行說明2022年11月
description: Adobe Experience Platform的2022年11月發行說明。
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: ccfc46714069e8c29f1777dea5ba73e318c0a4a6
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 5%

---

# Adobe Experience Platform 发行说明

**发行日期：2022 年 11 月 23 日**

Adobe Experience Platform 现有功能的更新包括：

- [資料彙集](#data-collection)
- [體驗資料模型(XDM)](#xdm)
- [源](#sources)

## 資料彙集 {#data-collection}

Adobe Experience Platform提供了一套技術，可讓您收集使用者端客戶體驗資料，並將其傳送至Adobe Experience Platform Edge Network，在那裡可以擴充和轉換資料，並將其分發到Adobe或非Adobe目的地。

**新功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| [!DNL AWS] 事件轉送的擴充功能 | 您現在可以將資料傳送至 [!DNL Amazon Web Services] ([!DNL AWS])使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 副檔名。 請參閱 [[!DNL AWS] 擴充功能概觀](../../tags/extensions/server/aws/overview.md) 以取得詳細資訊。 |
| [!DNL Google Ads Enhanced Conversions] 事件轉送的擴充功能 | 您現在可以將轉換資料傳送至 [!DNL Google Ads] 使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 副檔名。 請參閱 [[!DNL Google Ads Enhanced Conversions] 擴充功能概觀](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 以取得詳細資訊。 |
| [!DNL Microsoft Azure] 事件轉送的擴充功能 | 您現在可以將資料傳送至 [!DNL Microsoft Azure] 使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 副檔名。 請參閱 [[!DNL Microsoft Azure] 擴充功能概觀](../../tags/extensions/server/azure/overview.md) 以取得詳細資訊。 |

如需Platform資料收集功能的詳細資訊，請參閱 [資料彙集概觀](../../collection/home.md).

## 體驗資料模型(XDM) {#xdm}

XDM是開放原始碼規格，針對帶入Adobe Experience Platform的資料提供通用結構和定義（結構描述）。 藉由遵守XDM標準，所有客戶體驗資料都可以整合到通用表示中，以更快、更整合的方式提供深入分析。 您可以從客戶動作獲得有價值的深入分析、透過區段定義客戶對象，以及使用客戶屬性進行個人化。

**新功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| 直接新增到結構描述時，將欄位指派給自訂類別 | 時間 [將個別欄位直接新增到結構描述](../../xdm/ui/resources/schemas.md#add-individual-fields)，先前您只能將欄位指派給欄位群組作為其父資源。 現在，除了欄位群組之外，您可以 [將欄位指派給自訂類別](../../xdm/ui/resources/schemas.md#add-to-class) 作為其父級資源。 |

{style="table-layout:auto"}

如需有關Platform中XDM的詳細資訊，請參閱 [XDM系統總覽](../../xdm/home.md).

## 源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**更新的功能**

| 功能 | 描述 |
| --- | --- | 
| oracle服務雲端來源的測試版可用性 | 使用Oracle服務雲端來源，將資料從您的Oracle服務雲端帳戶擷取到Experience Platform。 如需詳細資訊，請參閱以下連結的相關檔案： [oracle服務雲端來源](../../sources/connectors/customer-success/oracle-service-cloud.md). |

若要進一步瞭解來源，請閱讀 [來源概觀](../../sources/home.md).
