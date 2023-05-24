---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
solution: Experience Platform
title: 自助來源（批次SDK）概觀
description: Adobe Experience Platform自助來源（批次SDK）是一組設定API，可讓您使用流程服務API整合REST API型來源，以將您的資料帶入Experience Platform。
exl-id: 5d5449ad-a1ba-402b-a281-0b2d8b704f32
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# 自助來源（批次SDK）概觀

Adobe Experience PlatformExperience Platform自助來源（批次SDK）是一個架構，可讓您使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). 自助來源（批次SDK）提供一組設定API，用於建立您自己的來源並將批次資料帶入Experience Platform。

使用自助式來源（批次SDK），您可以：

* 使用設定新來源並將其整合到Experience Platform目錄 [!DNL Flow Service] API。
* 定義來源的規格，包括與支援的驗證型別相關的資訊，以及如何擷取資源資料。
* 為您的新來源建立使用者導向的檔案。

自助來原始檔提供設定、測試和發行REST API型來源與Experience Platform整合的說明，並讓您的來源成為不斷成長的來源目錄的一部分。

![目錄](./assets/catalog.png)

## 瞭解來源

Experience Platform可從外部來源擷取資料，同時允許您使用Experience Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

如需來源的詳細資訊，以及檢視Experience Platform目前支援的不同來源清單，請參閱 [來源概觀](../home.md).

## 建立來源

透過自助來源，您可以整合自己的REST API型來源，並使用將您的資料Experience Platform [!DNL Flow Service]. 您可以透過建立、設定和提交新的連線規格，將來源整合到Experience Platform來源目錄 [!DNL Flow Service] API。

請參閱指南： [建立新的連線規格](./api/api-overview.md) 有關如何將新來源整合到Experience Platform的資訊。

## 記錄您的來源

建立來源後，請參閱 [檔案指南](./documentation/doc-overview.md) 有關如何透過以下檔案記錄來源的指示： [!DNL GitHub] 網頁介面或透過您自己的文字編輯器。

## 高階流程

以Experience Platform設定來源的逐步流程概述如下：

* 閱讀 [自助來源（批次SDK） API指南](./api/api-overview.md).
   * 閱讀 [快速入門手冊](./api/getting-started.md).
   * 請依照上的教學課程進行 [建立新的連線規格](./api/create.md).
   * 請依照上的教學課程進行 [更新您的連線規格](./api/update-connection-specs.md).
   * 請依照上的教學課程進行 [將新的連線規格ID新增至流量規格](./api/update-flow-specs.md)
   * [提交您的新來源](./api/submit.md).
* 若要更瞭解連線規格的結構和屬性，請閱讀以下指南： [自助來源設定選項（批次SDK）](./config/config.md).
   * 閱讀指南： [設定您的驗證規格](./config/authspec.md) 以更清楚瞭解您可以用於來源的不同驗證型別。
   * 閱讀指南： [設定您的來源規格](./config/sourcespec.md) 如需不同分頁型別、排程格式以及可針對來源設定的自訂結構描述的詳細資訊。
   * 閱讀指南： [設定您的瀏覽規格](./config/explorespec.md) 有關如何定義瀏覽和檢查來源中所含物件所需引數的資訊。
* 若要開始記錄您的來源，請閱讀 [建立自助式來原始檔概覽](./documentation/doc-overview.md)
   * 您可以使用此 [來源API檔案範本](./documentation/template.md) 以建構您的API檔案。
   * 您可以使用此 [來源UI檔案範本](./documentation/ui-template.md) 以建構您的UI檔案。
   * 請參閱指南： [使用GitHub網頁介面](./documentation/github.md) 有關如何使用GitHub建立檔案的步驟。
   * 請參閱指南： [使用文字編輯器](./documentation/text-editor.md) 有關如何使用本機電腦建立檔案的步驟。
