---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 設定資料集以擷取同意和偏好設定資料
description: 瞭解如何設定Experience Data Model (XDM)結構描述和資料集，以擷取Adobe Experience Platform中的同意和偏好設定資料。
exl-id: 61ceaa2a-c5ac-43f5-b118-502bdc432234
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---

# 設定資料集以擷取同意和偏好設定資料

為了讓Adobe Experience Platform處理您的客戶同意/偏好設定資料，該資料必須傳送至其結構描述包含與同意和其他許可權相關欄位的資料集。 具體而言，此資料集必須以 [!DNL XDM Individual Profile] 類別，並啟用以用於中 [!DNL Real-Time Customer Profile].

本檔案提供設定資料集的步驟，以便在Experience Platform中處理同意資料。 如需Platform中處理同意/偏好設定資料的完整工作流程總覽，請參閱 [同意處理概觀](./overview.md).

>[!IMPORTANT]
>
>本指南中的範例使用標準化的欄位集來代表客戶同意值，如以下所定義 [[!UICONTROL 同意和偏好設定詳細資料] 結構描述欄位群組](../../../../xdm/field-groups/profile/consents.md). 這些欄位的結構，是為了提供有效的資料模型，以涵蓋許多常見的同意收集使用案例。
>
>不過，您也可以根據自己的資料模型定義自己的欄位群組來表示同意。 請洽詢您的法律團隊，以根據下列選項取得符合您業務需求的同意資料模型核准：
>
>* 標準化的同意欄位群組
>* 由您的組織建立的自訂同意欄位群組
>* 標準化同意欄位群組和自訂同意欄位群組提供之其他欄位的組合


## 先决条件

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [體驗資料模型(XDM)](../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊。
* [即時客戶個人檔案](../../../../profile/home.md)：將不同來源的客戶資料整合至完整、統一的檢視中，並針對每個客戶互動提供可採取行動且附有時間戳記的說明。

>[!IMPORTANT]
>
>本教學課程假設您知道 [!DNL Profile] Platform中要用來擷取客戶屬性資訊的結構描述。 無論您使用何種方法來收集同意資料，此結構描述都必須 [啟用即時客戶個人檔案](../../../../xdm/ui/resources/schemas.md#profile). 此外，結構描述的主要身分不能是禁止用於興趣型廣告（例如電子郵件地址）的直接可識別欄位。 如果您不確定哪些欄位受到限制，請洽詢法律顧問。

## [!UICONTROL 同意和偏好設定詳細資料] 欄位群組結構 {#structure}

此 [!UICONTROL 同意和偏好設定詳細資料] 欄位群組提供標準化同意欄位給結構描述。 目前，此欄位群組僅與根據下列條件的結構描述相容： [!DNL XDM Individual Profile] 類別。

欄位群組提供單一物件型別欄位， `consents`，其子屬性會擷取一組標準化的同意欄位。 以下JSON為資料型別的範例 `consents` 資料擷取時預期：

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "idSpecific": {
      "email": {
        "jdoe@example.com": {
          "marketing": {
            "email": {
              "val": "n"
            }
          }
        }
      }
    }
  },
  "metadata": {
    "time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>如需中子屬性的結構和意義的詳細資訊 `consents`，請參閱 [[!UICONTROL 同意和偏好設定詳細資料] 欄位群組](../../../../xdm/field-groups/profile/consents.md).

## 將必要的欄位群組新增至 [!DNL Profile] 綱要 {#add-field-group}

為了使用Adobe標準收集同意資料，您必須具有包含下列兩個欄位群組的設定檔啟用結構描述：

* [!UICONTROL 同意和偏好設定詳細資料]
* [!UICONTROL 身分對應] （使用Platform Web或Mobile SDK傳送同意訊號時需要）

在Platform UI中選取 **[!UICONTROL 結構描述]** 在左側導覽中，然後選取 **[!UICONTROL 瀏覽]** 標籤來顯示現有結構描述的清單。 從這裡，選取 [!DNL Profile] — 您想要新增同意欄位的已啟用結構描述。 本節中的熒幕擷取畫面使用內建於 [結構描述建立教學課程](../../../../xdm/tutorials/create-schema-ui.md) 例如。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>您可以使用工作區的搜尋和篩選功能，輕鬆找到您的結構描述。 請參閱指南： [探索XDM資源](../../../../xdm/ui/explore.md) 以取得詳細資訊。

此 [!DNL Schema Editor] 會出現，並在畫布中顯示結構描述的結構。 在畫布左側，選取 **[!UICONTROL 新增]** 在 **[!UICONTROL 欄位群組]** 區段。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-field-group.png)

此 **[!UICONTROL 新增欄位群組]** 對話方塊隨即顯示。 從此處選取 **[!UICONTROL 同意和偏好設定詳細資料]** 從清單中。 您可以選擇使用搜尋列來縮小結果範圍，以便更輕鬆地找到欄位群組。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-group-dialog.png)

接下來，尋找 **[!UICONTROL 身分對應]** 欄位群組，並加以選取。 將兩個欄位群組都列在右側邊欄中後，選取 **[!UICONTROL 新增欄位群組]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/identitymap.png)

畫布會重新出現，並顯示 `consents` 和 `identityMap` 欄位已新增至結構描述結構。 如果您需要標準欄位群組未擷取的其他同意和偏好設定欄位，請參閱附錄 [將自訂同意和偏好設定欄位新增到結構描述](#custom-consent). 否則，請選取 **[!UICONTROL 儲存]** 以完成架構的變更。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

>[!IMPORTANT]
>
>如果您要建立新結構描述，或編輯尚未為設定檔啟用的現有結構描述，您必須 [為設定檔啟用結構描述](../../../../xdm/ui/resources/schemas.md#profile) 儲存之前。

如果您編輯的結構描述是由 [!UICONTROL 設定檔資料集] 已在您的Platform Web SDK資料流中指定，該資料集現在會包含新的同意欄位。 您現在可以返回 [同意處理指南](./overview.md#merge-policies) 以繼續設定Experience Platform以處理同意資料的程式。 如果您尚未為此結構描述建立資料集，請依照下一節中的步驟操作。

## 根據您的同意結構描述建立資料集 {#dataset}

使用同意欄位建立結構描述後，您必須建立資料集，以便最終擷取客戶的同意資料。 此資料集必須啟用 [!DNL Real-Time Customer Profile].

若要開始，請選取 **[!UICONTROL 資料集]** 在左側導覽中，然後選取 **[!UICONTROL 建立資料集]** 右上角。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

在下一頁，選取 **[!UICONTROL 從結構描述建立資料集]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

此 **[!UICONTROL 從結構描述建立資料集]** 工作流程隨即出現，從 **[!UICONTROL 選取結構描述]** 步驟。 在提供的清單中，找到您先前建立的其中一個同意結構描述。 您可以選擇使用搜尋列來縮小結果範圍，並更容易找到您的結構描述。 選取所需綱要旁的單選按鈕，然後選取 **[!UICONTROL 下一個]** 以繼續。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

此 **[!UICONTROL 設定資料集]** 步驟隨即顯示。 在選取之前，為資料集提供唯一、易於識別的名稱和說明 **[!UICONTROL 完成]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

新建立資料集的詳細資訊頁面隨即顯示。 如果資料集是以您的時間序列結構描述為基礎，則程式已完成。 如果資料集是以您的記錄結構描述為基礎，則此程式的最後一步是啟用資料集以用於中 [!DNL Real-Time Customer Profile].

在右邊欄中，選取 **[!UICONTROL 設定檔]** 切換。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

最後，選取 **[!UICONTROL 啟用]** 在確認彈出視窗中啟用結構描述 [!DNL Profile].

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

資料集現在已儲存並啟用，以供使用 [!DNL Profile]. 如果您打算使用Platform Web SDK將同意資料傳送至設定檔，您必須選取此資料集作為 [!UICONTROL 設定檔資料集] 設定您的 [資料串流](../../../../edge/datastreams/overview.md).

## 后续步骤

依照本教學課程，您已新增同意欄位至 [!DNL Profile] — 啟用的結構描述，其資料集將用於使用Platform Web SDK或直接XDM擷取來擷取同意資料。

您現在可以返回 [同意處理概觀](./overview.md#merge-policies) 以繼續設定Experience Platform以處理同意資料。

## 附录

下節包含建立資料集以擷取客戶同意和偏好設定資料的其他資訊。

### 將自訂同意和偏好設定欄位新增到結構描述 {#custom-consent}

如果您需要擷取標準所代表同意訊號以外的其他同意訊號 [!UICONTROL 同意和偏好設定詳細資料] 欄位群組，則可使用自訂XDM元件來增強同意綱要，以符合您的特定業務需求。 本節概述如何自訂您的同意綱要的基本原則，以便將這些訊號擷取到設定檔中。

>[!IMPORTANT]
>
>Platform Web和Mobile SDK的同意變更命令不支援自訂欄位。 目前將自訂同意欄位擷取至設定檔的唯一方式是透過 [批次擷取](../../../../ingestion/batch-ingestion/overview.md) 或 [來源連線](../../../../sources/home.md).

強烈建議您使用 [!UICONTROL 同意和偏好設定詳細資料] 欄位群組作為同意資料結構的基準，並根據需要新增其他欄位，而不是嘗試從頭開始建立整個結構。

若要將自訂欄位新增至標準欄位群組的結構，您必須先建立自訂欄位群組。 新增 [!UICONTROL 同意和偏好設定詳細資料] 欄位群組至結構描述，選取 **加(+)** 圖示於 **[!UICONTROL 欄位群組]** 區段，然後選取 **[!UICONTROL 建立新欄位群組]**. 提供欄位群組的名稱和選擇性說明，然後選取 **[!UICONTROL 新增欄位群組]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field-group.png)

此 [!DNL Schema Editor] 會在左側邊欄中選取新的自訂欄位群組時重新顯示。 在畫布中顯示可讓您新增自訂欄位到結構描述結構的控制項。 若要新增同意或偏好設定欄位，請選取 **加(+)** 圖示加以存取 `consents` 物件。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

新欄位會出現在 `consents` 物件。 由於您要將自訂欄位新增至標準XDM物件，新欄位會在以租使用者ID命名的物件下建立。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

在右邊欄中，於 **[!UICONTROL 欄位屬性]**，提供欄位的名稱和說明。 選取欄位的 **[!UICONTROL 型別]**，您必須對自訂同意或偏好設定欄位使用適當的標準資料型別：

* [[!UICONTROL 一般同意欄位]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL 通用行銷偏好設定欄位]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL 具有訂閱的一般行銷偏好設定欄位]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL 通用個人化偏好設定欄位]](../../../../xdm/data-types/personalization-field.md)

完成後，選取 **[!UICONTROL 套用]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

同意或偏好設定欄位會新增至結構描述結構。 請注意 [!UICONTROL 路徑] 顯示在右側邊欄中，包含 `_tenantId` 名稱空間。 每當您在資料作業中參照此欄位的路徑時，都必須包含此名稱空間。

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

請依照上述步驟繼續新增您需要的同意和偏好設定欄位。 完成後，選取 **[!UICONTROL 儲存]** 以確認您的變更。

如果您尚未為此結構描述建立資料集，請繼續前往一節： [建立資料集](#dataset).
