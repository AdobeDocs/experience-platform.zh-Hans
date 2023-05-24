---
title: 在Real-time Customer Data Platform B2B版本中定義兩個結構描述之間的關係
description: 瞭解如何在Adobe Real-time Customer Data Platform B2B Edition中定義兩個結構描述之間的多對一關係。
exl-id: 14032754-c7f5-46b6-90e6-c6e99af1efba
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '1391'
ht-degree: 14%

---

# 在Real-time Customer Data Platform B2B版本中定義兩個結構描述之間的多對一關係 {#relationship-b2b}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_reference_schema"
>title="参考架构"
>abstract="选择要与之建立关系的架构。根据架构的类，它还可能与 B2B 上下文中的其他实体存在现有关系。请参阅文档以了解 B2B 架构类如何相互关联。"

Adobe Real-time Customer Data Platform B2B Edition提供數種Experience Data Model (XDM)類別，可擷取基本B2B資料實體，包括 [帳戶](../classes/b2b/business-account.md)， [機會](../classes/b2b/business-opportunity.md)， [行銷活動](../classes/b2b/business-campaign.md)、等等。 根據這些類別建立結構描述，並啟用它們以用於中 [即時客戶個人檔案](../../profile/home.md)，您可以將不同來源的資料合併成稱為聯合結構描述的統一表示法。

不過，聯合結構描述只能包含共用相同類別的結構描述所擷取的欄位。 這就是結構描述關係的用處。 透過在B2B結構描述中實作關係，您可以說明這些業務實體如何彼此關聯，並可在下游細分使用案例中包含來自多個類別的屬性。

下圖提供不同B2B類別在基本實作中如何相互關聯的範例：

![B2B類別關係](../images/tutorials/relationship-b2b/classes.png)

本教學課程涵蓋在Real-Time CDP B2B Edition中定義兩個結構描述之間多對一關係的步驟。

>[!NOTE]
>
>如果您沒有使用Real-time Customer Data Platform B2B Edition或想建立一對一的關係，請參閱以下指南中的內容： [建立一對一關係](./relationship-ui.md) 而非。
>
>本教學課程著重於如何在Platform UI中手動建立B2B結構描述之間的關係。 如果您從B2B來源連線引進資料，您可以使用自動產生公用程式來建立所需的結構描述、身分和關係。 如需有關的詳細資訊，請參閱B2B名稱空間和結構描述的來原始檔 [使用自動產生公用程式](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md).

## 快速入门

本教學課程需要您實際瞭解 [!DNL XDM System] 以及中的結構編輯器 [!DNL Experience Platform] UI。 在開始本教學課程之前，請檢閱下列檔案：

* [Experience Platform中的XDM系統](../home.md)：XDM及其在中的實作概觀 [!DNL Experience Platform].
* [結構描述組合基本概念](../schema/composition.md)：XDM結構描述建置區塊簡介。
* [使用建立方案 [!DNL Schema Editor]](create-schema-ui.md)：此教學課程涵蓋如何在UI中建立及編輯結構描述的基礎知識。

## 定義來源和參考結構描述

您應已建立將在關係中定義的兩個結構描述。 為了示範，本教學課程會在商業機會之間建立關係(定義於「[!DNL Opportunities]「結構描述)及其相關聯的商業帳戶(定義於「[!DNL Accounts]&quot;結構描述)。

結構描述關係由內的專用欄位表示。 **來源結構描述** 會參照的主要身分欄位 **參考結構描述**. 在接下來的步驟中， 」[!DNL Opportunities]&quot;作為來源結構描述，而&quot;[!DNL Accounts]「 」可作為參考結構描述。

### 瞭解B2B關係中的身分

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_identity_namespace"
>title="参考标识命名空间"
>abstract="参考架构的主要标识字段的命名空间（类型）。参考架构必须有一个建立的主要标识字段才能参与关系。请参阅文档以了解有关 B2B 关系中的标识的更多信息。"

為了建立關係，參考結構描述必須具有定義的主要身分。 為B2B實體設定主要身分時，請記住，如果您跨不同系統或位置收集字串型實體ID，則這些ID可能會重疊，這可能會導致Platform中的資料衝突。

為了解決這個問題，所有標準B2B類別都包含符合 [[!UICONTROL B2B來源] 資料型別](../data-types/b2b-source.md). 此資料型別提供B2B實體的字串識別碼欄位，以及有關識別碼來源的其他內容資訊。 其中一個欄位， `sourceKey`，串連資料型別中其他欄位的值，以產生實體的完全唯一識別碼。 此欄位一律用作B2B實體結構描述的主要身分。

![sourceKey欄位](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>時間 [將XDM欄位設定為身分](../ui/fields/identity.md)，您必須提供身分名稱空間，才能在下定義身分。 這可以是Adobe提供的標準名稱空間，也可以是貴組織定義的自訂名稱空間。 實際上，名稱空間只是內容字串，您可以設定為您喜歡的任何值，前提是這對於您的組織分類身分型別有意義。 請參閱以下文章的概觀： [身分名稱空間](../../identity-service/namespaces.md) 以取得詳細資訊。

為方便參考，以下幾節將說明在定義關係之前，本教學課程中使用的每個結構描述的結構。 記下在結構描述結構中定義主要身分的位置，以及這些身分使用的自訂名稱空間。

### [!DNL Opportunities] 綱要

來源結構描述&quot;[!DNL Opportunities]&quot;是根據 [!UICONTROL XDM商業機會] 類別。 類別提供的其中一個欄位， `opportunityKey`，當作結構描述的識別碼。 具體而言， `sourceKey` 欄位位於 `opportunityKey` 物件在名為的自訂名稱空間下設定為結構描述的主要身分 [!DNL B2B Opportunity].

如下方所示 **[!UICONTROL 結構描述屬性]**，此結構描述已啟用以用於中 [!DNL Real-Time Customer Profile].

![機會結構描述](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] 綱要

參考結構描述»[!DNL Accounts]&quot;是根據 [!UICONTROL XDM帳戶] 類別。 根層級 `accountKey` 欄位包含 `sourceKey` 會在名為的自訂名稱空間下當作其主要身分識別 [!DNL B2B Account]. 此結構描述也已啟用以供設定檔使用。

![帳戶結構描述](../images/tutorials/relationship-b2b/accounts.png)

## 定義來源結構描述的關係欄位 {#relationship-field}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_current"
>title="当前架构中的关系名称"
>abstract="描述当前架构与参考架构之间的关系的标签（例如，“相关帐户”）。此标签在配置文件和分段中用于为来自相关 B2B 实体的数据提供上下文。请参阅文档以了解有关构建 B2B 架构关系的更多信息。"

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_reference"
>title="参考架构中的关系名称"
>abstract="描述参考架构与当前架构之间的关系的标签（例如，“相关机会”）。此标签在配置文件和分段中用于为来自相关 B2B 实体的数据提供上下文。请参阅文档以了解有关构建 B2B 架构关系的更多信息。"

為了定義兩個結構描述之間的關係，來源結構描述必須具有專用欄位，以指示參考結構描述的主要身分。 標準B2B類別包含一般相關商業實體的專用來源索引鍵欄位。 例如， [!UICONTROL XDM商業機會] 類別包含相關帳戶(`accountKey`)和相關的行銷活動(`campaignKey`)。 不過，您也可以新增其他 [!UICONTROL B2B來源] 如果需要的元件超過預設元件，請使用自訂欄位群組將欄位新增至結構描述。

>[!NOTE]
>
>目前，從來源結構描述到參考結構描述只能定義多對一和一對一關係。 對於一對多關係，您必須在代表「許多」的結構描述中定義關係欄位。

若要設定關係欄位，請選取箭頭圖示(![箭頭圖示](../images/tutorials/relationship-b2b/arrow.png))位於畫布中相關欄位旁。 若為 [!DNL Opportunities] 結構描述，這是 `accountKey.sourceKey` 欄位，因為目標是與帳戶建立多對一關係。

![關係按鈕](../images/tutorials/relationship-b2b/relationship-button.png)

會出現一個對話方塊，可讓您指定有關關係的詳細資訊。 關係型別會自動設定為 **[!UICONTROL 多對一]**.

![關係對話方塊](../images/tutorials/relationship-b2b/relationship-dialog.png)

下 **[!UICONTROL 參考結構描述]**，使用搜尋列來尋找參考結構描述的名稱。 反白參考結構描述名稱時， **[!UICONTROL 參考身分名稱空間]** 欄位會自動更新為結構描述主要身分的名稱空間。

![參考結構描述](../images/tutorials/relationship-b2b/reference-schema.png)

下 **[!UICONTROL 來自目前結構描述的關係名稱]** 和 **[!UICONTROL 引用結構描述中的關係名稱]**，分別為來源和參考結構描述中的關係提供易記名稱。 完成後，選取 **[!UICONTROL 儲存]** 以套用變更並儲存結構。

![關係名稱](../images/tutorials/relationship-b2b/relationship-name.png)

畫布會重新出現，而關係欄位現在會以您先前提供的好記名稱標籤。 此關係名稱也會列在左側邊欄下方，以方便參考。

![已套用關係](../images/tutorials/relationship-b2b/relationship-applied.png)

如果您檢視參考結構描述的結構，關係標籤會出現在結構描述的主要身分欄位旁和左側邊欄中。

![目的地結構描述關係標籤](../images/tutorials/relationship-b2b/destination-relationship.png)

## 后续步骤

依照本教學課程所述，您已使用下列範例成功建立兩個結構描述之間的多對一關係： [!DNL Schema Editor]. 使用以這些結構為基礎的資料集擷取資料，且該資料已在設定檔資料存放區中啟動後，您就可以將這兩個結構中的屬性用於 [多類別細分使用案例](../../rtcdp/segmentation/b2b.md).
