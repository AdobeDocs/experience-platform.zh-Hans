---
keywords: Experience Platform；首頁；熱門主題；UI；UI；XDM；XDM系統；體驗資料模型；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述編輯器；結構描述編輯器；結構描述；結構描述；結構描述；建立；關係；參考；參考；
solution: Experience Platform
title: 使用結構編輯器定義兩個結構描述之間的關係
description: 本檔案提供在Experience Platform使用者介面中使用結構編輯器定義兩個結構描述之間關係的教學課程。
type: Tutorial
exl-id: feed776b-bc8d-459b-9700-e5c9520788c0
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 9%

---

# 使用定義兩個結構描述之間的一對一關係 [!DNL Schema Editor] {#relationship-ui}

>[!CONTEXTUALHELP]
>id="platform_schemas_relationships"
>title="架构关系"
>abstract="可以通过关系字段对属于不同类的架构进行上下文链接，从而构建更复杂的分段规则。有关架构关系的更多信息，请参阅文档。"

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_reference_schema"
>title="参考架构"
>abstract="选择要与之建立关系的架构。此架构可以是与当前架构不同的类。有关架构关系的更多信息，请参阅文档。"

>[!CONTEXTUALHELP]
>id="platform_xdm_1to1_identity_namespace"
>title="参考标识命名空间"
>abstract="参考架构的主要标识字段的命名空间（类型）。参考架构必须有一个建立的主要标识字段才能参与关系。有关架构关系的更多信息，请参阅文档。"

瞭解客戶之間的關係以及客戶在不同管道中與您品牌的互動是Adobe Experience Platform的重要部分。 在的結構中定義這些關係 [!DNL Experience Data Model] (XDM)結構描述可讓您對客戶資料獲得複雜的深入分析。

雖然結構描述關係可透過使用聯合結構描述和來推斷 [!DNL Real-Time Customer Profile]，這僅適用於共用相同類別的結構描述。 若要在屬於不同類別的兩個結構描述之間建立關係，必須將專用關係欄位新增到來源結構描述中，該欄位會參考其他相關結構描述的身分。

本檔案提供使用結構編輯器定義兩個結構描述之間關係的教學課程。 [!DNL Experience Platform] 使用者介面。 如需使用API定義結構描述關係的步驟，請參閱以下教學課程： [使用結構描述登入API定義關係](relationship-api.md).

>[!NOTE]
>
>如需在Adobe Real-time Customer Data Platform B2B版本中建立多對一關係的步驟，請參閱以下指南： [建立B2B關係](./relationship-b2b.md).

## 快速入门

本教學課程需要您實際瞭解 [!DNL XDM System] 以及中的結構編輯器 [!DNL Experience Platform] UI。 在開始本教學課程之前，請檢閱下列檔案：

* [Experience Platform中的XDM系統](../home.md)：XDM及其在中的實作概觀 [!DNL Experience Platform].
* [結構描述組合基本概念](../schema/composition.md)：XDM結構描述建置區塊簡介。
* [使用建立方案 [!DNL Schema Editor]](create-schema-ui.md)：此教學課程涵蓋使用的基本知識 [!DNL Schema Editor].

## 定義來源和參考結構描述

您應已建立將在關係中定義的兩個結構描述。 為了示範，本教學課程會在組織的熟客方案成員之間建立關係(定義於「[!DNL Loyalty Members]「結構描述)和他們最喜愛的飯店(定義於「[!DNL Hotels]&quot;結構描述)。

>[!IMPORTANT]
>
>為了建立關係，兩個結構描述都必須定義主要身分並啟用 [!DNL Real-Time Customer Profile]. 請參閱以下小節： [啟用結構描述以在設定檔中使用](./create-schema-ui.md#profile) 架構建立教學課程中，如果您需要有關如何據以設定架構的指引。

結構描述關係由內的專用欄位表示。 **來源結構描述** 該欄位指向 **參考結構描述**. 在接下來的步驟中， 」[!DNL Loyalty Members]&quot;將是來源結構描述，而&quot;[!DNL Hotels]」將做為參考結構描述。

以下幾節說明在定義關係之前，本教學課程中使用的每個結構描述的結構。

### [!DNL Loyalty Members] 綱要

來源結構描述&quot;[!DNL Loyalty Members]&quot;是根據 [!DNL XDM Individual Profile] 類別，包含描述忠誠度計畫成員的欄位。 其中一個欄位， `personalEmail.addess`，會作為下結構描述的主要身分 [!UICONTROL 電子郵件] 名稱空間。 如下方所示 **[!UICONTROL 結構描述屬性]**，此結構描述已啟用以用於中 [!DNL Real-Time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] 綱要

參考結構描述»[!DNL Hotels]「以自訂為基礎」[!DNL Hotels]「類別，並包含描述飯店的欄位。 為了參與關係，參考結構描述還必須定義主要身分並啟用 [!UICONTROL 設定檔]. 在這種情況下， `_tenantId.hotelId`使用自訂&quot;，當作結構描述的主要身分識別。[!DNL Hotel ID]&quot;身分名稱空間。

![為設定檔啟用](../images/tutorials/relationship/hotels.png)

>[!NOTE]
>
>若要瞭解如何建立自訂身分名稱空間，請參閱 [Identity Service檔案](../../identity-service/namespaces.md#manage-namespaces).

## 建立關係欄位群組

>[!NOTE]
>
>只有在您的來源結構描述沒有專用字串型別欄位來當作參考結構描述主要身分的指標時，才需要執行此步驟。 如果您已在來源結構描述中定義此欄位，請跳至的下一個步驟 [定義關係欄位](#relationship-field).

為了定義兩個結構描述之間的關係，來源結構描述必須有一個專用欄位來指示參考結構描述的主要身分。 您可以建立新的結構描述欄位群組或擴充現有的結構描述欄位群組，將此欄位新增至來源結構描述。

若為 [!DNL Loyalty Members] 結構描述，新 `preferredHotel` 將會新增欄位，以指出忠誠會員對於公司造訪偏好的飯店。 從選取加號圖示(**+**)。

![](../images/tutorials/relationship/loyalty-add-field.png)

畫布中會出現新的欄位預留位置。 下 **[!UICONTROL 欄位屬性]**，提供欄位名稱和欄位顯示名稱，並將其型別設為&quot;[!UICONTROL 字串]「。 下 **[!UICONTROL 指派給]**，選取要擴充的現有欄位群組，或輸入唯一名稱以建立新欄位群組。 在此範例中，新增&quot;[!DNL Preferred Hotel]「欄位群組已建立。

![](../images/tutorials/relationship/relationship-field-details.png)

完成後，選取 **[!UICONTROL 套用]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

已更新 `preferredHotel` 欄位會顯示在畫布中，位於 `_tenantId` 物件，因為它是自訂欄位。 選取 **[!UICONTROL 儲存]** 以完成您對結構描述的變更。

![](../images/tutorials/relationship/relationship-field-save.png)

## 定義來源結構描述的關係欄位 {#relationship-field}

一旦您的來源結構描述定義了專用參考欄位，您就可以將其指定為關係欄位。

>[!NOTE]
>
>以下步驟說明如何使用畫布中的滑鼠右欄控制項定義關係欄位。 如果您有Real-Time CDP B2B Edition的存取權，也可以使用 [相同對話方塊](./relationship-b2b.md#relationship-field) 建立多對一關係時也是如此。

選取 `preferredHotel` 欄位，然後向下捲動至 **[!UICONTROL 欄位屬性]** 直到 **[!UICONTROL 關係]** 核取方塊隨即顯示。 選取核取方塊以顯示設定關係欄位所需的引數。

![](../images/tutorials/relationship/relationship-checkbox.png)

選取以下專案的下拉式清單： **[!UICONTROL 參考結構描述]** 並選取關係的參考結構描述(&quot;[!DNL Hotels]&quot;（在此範例中）。 下 **[!UICONTROL 參考身分名稱空間]**，選取參考結構描述身分欄位的名稱空間(在此案例中為「 」[!DNL Hotel ID]「)。 選取 **[!UICONTROL 套用]** 完成後。

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

此 `preferredHotel` 欄位現在會在畫布中反白為關係，顯示參考結構描述的名稱。 選取 **[!UICONTROL 儲存]** 以儲存變更並完成工作流程。

![](../images/tutorials/relationship/relationship-save.png)

## 后续步骤

依照本教學課程所述，您已使用下列範例成功建立兩個結構描述之間的一對一關係： [!DNL Schema Editor]. 如需如何使用API定義關係的步驟，請參閱以下教學課程： [使用結構描述登入API定義關係](relationship-api.md).
