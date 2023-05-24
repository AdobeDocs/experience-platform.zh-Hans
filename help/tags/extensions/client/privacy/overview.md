---
title: Adobe隱私權擴充功能概觀
description: 瞭解Adobe Experience Platform中的Adobe隱私權標籤擴充功能。
exl-id: 8401861e-93ad-48eb-8796-b26ed8963c32
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 5%

---

# Adobe隱私權擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

Adobe隱私權標籤擴充功能可讓您收集及移除使用者端裝置上Adobe解決方案指派給使用者的使用者ID。 收集的ID可傳送至 [Adobe Experience Platform Privacy Service](../../../../privacy-service/home.md) 在支援的Adobe Experience Cloud應用程式中存取或刪除相關個人的個人資料。

本指南說明如何在AdobeUI或資料收集UI中安裝和設定Experience Platform隱私權擴充功能。

>[!NOTE]
>
>如果您偏好在不使用標籤的情況下安裝這些功能，請參閱 [隱私權JavaScript程式庫概觀](../../../../privacy-service/js-library.md) 以瞭解如何使用原始程式碼來實作的步驟。

## 安装和配置 扩展

選取 **[!UICONTROL 擴充功能]** 在左側導覽列中，後面接著 **[!UICONTROL 目錄]** 標籤。 使用搜尋列縮小可用擴充功能清單的範圍，直到找到「Adobe隱私權」為止。 選取 **[!UICONTROL 安裝]** 以繼續。

![安裝擴充功能](../../../images/extensions/client/privacy/install.png)

下一個畫面可讓您設定要擴充功能從中收集ID的來源和解決方案。 擴充功能支援下列解決方案：

* Adobe Analytics (AA)
* Adobe Audience Manager (AAM)
* Adobe Target
* Adobe Experience Cloud Identity服務（訪客或ECID）
* Adobe Advertising Cloud (AdCloud)

選取一或多個解決方案，然後選取 **[!UICONTROL 更新]**.

![选择解决方案](../../../images/extensions/client/privacy/select-solutions.png)

畫面會更新，根據您選取的解決方案，顯示所需設定引數的輸入。

![必要屬性](../../../images/extensions/client/privacy/required-properties.png)

使用下面的下拉式選單，您還可以將其他解決方案特定的引數新增到設定。

![選擇性屬性](../../../images/extensions/client/privacy/optional-properties.png)

>[!NOTE]
>
>請參閱以下小節： [設定引數](../../../../privacy-service/js-library.md#config-params) ，以取得每個支援解決方案的接受設定值的詳細資訊。

完成新增所選解決方案的引數後，請選取 **[!UICONTROL 儲存]** 以儲存設定。

![選擇性屬性](../../../images/extensions/client/privacy/save-config.png)

## 使用擴充功能 {#using}

Adobe隱私權擴充功能提供三種動作型別，可用於下列用途： [規則](../../../ui/managing-resources/rules.md) 當特定事件發生且符合條件時：

* **[!UICONTROL 擷取身分]**：會擷取使用者儲存的身分資訊。
* **[!UICONTROL 移除身分]**：移除使用者儲存的身分資訊。
* **[!UICONTROL 擷取然後移除身分]**：擷取使用者儲存的身分資訊，然後移除。

對於上述每個動作，您必須提供回呼JavaScript函式，該函式接受並處理擷取的身分識別資料作為物件引數。 從這裡，您可以儲存這些身分、顯示身分，或將其傳送至 [PRIVACY SERVICEAPI](../../../../privacy-service/api/overview.md) 視需要而定。

使用Adobe隱私權標籤擴充功能時，您必須以資料元素的形式提供所需的回呼函式。 請參閱下一節以瞭解如何設定此資料元素的步驟。

### 定義資料元素以處理身分

透過選取「 」，開始建立新資料元素的程式 **[!UICONTROL 資料元素]** 在左側導覽列中，後面接著 **[!UICONTROL 新增資料元素]**. 進入設定畫面後，選取「 」 **[!UICONTROL 核心]** 擴充功能和 **[!UICONTROL 自訂程式碼]** （資料元素型別）。 從此處選取 **[!UICONTROL 開啟編輯器]** 在右側面板中。

![選取資料元素型別](../../../images/extensions/client/privacy/data-element-type.png)

在出現的對話方塊中，定義將處理擷取之身分識別的JavaScript函式。 回呼必須接受單一物件型別引數(`ids` （在以下範例中）。 然後，函式可以處理您想要的ID，也可以叫用網站上全域可用的任何變數和函式以供進一步處理。

>[!NOTE]
>
>如需有關架構的詳細資訊， `ids` 回呼函式應處理的物件，請參閱 [程式碼範例](../../../../privacy-service/js-library.md#samples) 隱私權JavaScript程式庫概觀中提供。

完成後，選取 **[!UICONTROL 儲存]**.

![定義回呼函式](../../../images/extensions/client/privacy/define-custom-code.png)

如果您需要不同事件的不同回呼，可以繼續建立其他自訂程式碼資料元素。

### 使用隱私權動作建立規則

設定回呼資料元素以處理擷取的ID後，您可以建立規則，每當網站上發生特定事件，並符合您所需的任何其他條件時，就會叫用Adobe隱私權擴充功能。

為規則設定動作時，選取 **[!UICONTROL Adobe隱私權]** 用於擴充功能。 對於動作型別，請選取 [三個函式](#using) 由擴充功能提供。

![選取動作型別](../../../images/extensions/client/privacy/action-type.png)

右側面板會提示您選取將做為動作回撥的資料元素。 選取資料庫圖示(![資料庫圖示](../../../images/extensions/client/privacy/database.png))並從清單中選擇您先前建立的資料元素。 選取 **[!UICONTROL 保留變更]** 以繼續。

![選取資料元素](../../../images/extensions/client/privacy/add-data-element.png)

從這裡，您可以繼續設定規則，讓Adobe隱私權動作根據您需要的事件和條件引發。 滿意後，選取 **[!UICONTROL 儲存]**.

![保存规则](../../../images/extensions/client/privacy/save-rule.png)

您現在可以將規則新增至程式庫，以便在網站上部署為組建進行測試。 請參閱以下文章的概觀： [標籤發佈流程](../../../ui/publishing/overview.md) 以取得詳細資訊。

## 停用或解除安裝擴充功能

安装该扩展后，您可以禁用或删除它。選取 **[!UICONTROL 設定]** (位於已安裝擴充功能的「Adobe隱私權」卡上)，然後選取 **[!UICONTROL 停用]** 或 **[!UICONTROL 解除安裝]**.

## 后续步骤

本指南涵蓋UI中Adobe隱私權標籤擴充功能的使用。 如需擴充功能提供的詳細資訊，包括如何使用原始程式碼加以運用的範例，請參閱 [隱私權JavaScript程式庫概觀](../../../../privacy-service/js-library.md) 在Privacy Service檔案中。
