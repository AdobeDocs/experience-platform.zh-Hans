---
keywords: Experience Platform；首頁；熱門主題；UI；UI；XDM；XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述編輯器；結構描述；結構描述；結構描述；結構描述
solution: Experience Platform
title: 使用結構編輯器建立結構描述
type: Tutorial
description: 本教程介绍了在 Experience Platform 中使用模式编辑器创建模式的步骤。
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '3959'
ht-degree: 0%

---

# 使用建立方案 [!DNL Schema Editor]

Adobe Experience Platform使用者介面可讓您建立和管理 [!DNL Experience Data Model] (XDM)在稱為 [!DNL Schema Editor]. 本教學課程說明如何使用 [!DNL Schema Editor].

為了示範，本教學課程中的步驟涉及建立範例結構描述，以說明客戶忠誠度計畫的會員。 雖然您可以使用這些步驟建立不同的結構描述以滿足您自己的目的，但建議您先建立範例結構描述以瞭解 [!DNL Schema Editor].

>[!NOTE]
>
>如果您正在將CSV資料擷取至Platform，您可以 [將該資料對應到AI產生的建議所建立的XDM結構描述](../../ingestion/tutorials/map-csv/recommendations.md) （目前為測試版），不需自行手動建立結構描述。
>
>如果您偏好使用來撰寫結構 [!DNL Schema Registry] API，從讀取 [[!DNL Schema Registry] 開發人員指南](../api/getting-started.md) 在嘗試進行教學課程之前： [使用API建立結構描述](create-schema-api.md).

## 快速入门

本教學課程需要深入瞭解Adobe Experience Platform建立結構描述的各個層面。 在開始本教學課程之前，請檢閱檔案以瞭解下列概念：

* [[!DNL Experience Data Model (XDM)]](../home.md)：作為依據的標準化架構 [!DNL Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../schema/composition.md)：XDM結構描述及其建置區塊的概觀，包括類別、結構描述欄位群組、資料型別和個別欄位。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

## 開啟 [!UICONTROL 結構描述] 工作區 {#browse}

此 [!UICONTROL 結構描述] 工作區在 [!DNL Platform] UI可提供 [!DNL Schema Library]，可讓您檢視管理可用於貴組織的結構描述。 工作區也包含 [!DNL Schema Editor]，即您可在本教學課程中撰寫結構描述的畫布。

登入之後 [!DNL Experience Platform]，選取 **[!UICONTROL 結構描述]** 在左側導覽以開啟 **[!UICONTROL 結構描述]** 工作區。 此 **[!UICONTROL 瀏覽]** 索引標籤會顯示結構描述清單(此清單代表了 [!DNL Schema Library])可供檢視與自訂。 此清單包括結構描述所依據的名稱、型別、類別和行為（記錄或時間序列），以及上次修改結構描述的日期和時間。

請參閱指南： [在UI中探索現有XDM資源](../ui/explore.md) 以取得詳細資訊。

## 建立結構描述並為其命名 {#create}

若要開始構成結構描述，請選取 **[!UICONTROL 建立結構描述]** 右上角 **[!UICONTROL 結構描述]** 工作區。 下拉式功能表隨即顯示，讓您可選擇在核心類別之間進行選擇 [!UICONTROL XDM個別設定檔] 和 [!UICONTROL XDM ExperienceEvent]. 如果這些類別不符合您的目的，您也可以選取 **[!UICONTROL 瀏覽]** 以從其他可用的類別中選擇 [建立新類別](#create-new-class).

在本教學課程中，請選取 **[!UICONTROL XDM個別設定檔]**.

![](../images/tutorials/create-schema/create-schema-button.png)

此 [!DNL Schema Editor] 出現。 這是您將在其中撰寫結構描述的畫布。 系統會自動在中建立未命名的結構描述 **[!UICONTROL 結構]** 區段，以及根據該類別包含在所有結構描述中的標準欄位。 結構描述的指派類別也會列在 **[!UICONTROL 類別]** 在 **[!UICONTROL 組合]** 區段。

![](../images/tutorials/create-schema/schema-editor.png)

>[!NOTE]
>
>您可以 [變更結構描述的類別](#change-class) 在儲存結構描述之前的初始構成程式期間的任何時刻，但應極其謹慎地進行。 欄位群組僅與某些類別相容，因此變更類別將會重設畫布和您已新增的任何欄位。

下 **[!UICONTROL 結構描述屬性]**，提供結構描述的顯示名稱和說明（選用）。 輸入名稱后，畫布會更新以反映結構描述的新名稱。

![](../images/tutorials/create-schema/name-schema.png)

決定結構描述名稱時，有幾個重要考量要考量：

* 結構描述名稱應簡短且具有描述性，以便稍後可以輕鬆找到結構描述。
* 結構描述名稱必須是唯一的，這表示它也應足夠具體，以便將來不會重複使用。 例如，如果貴組織針對不同品牌有不同的忠誠度方案，將方案命名為「品牌A忠誠度會員」將是明智的做法，可讓您輕鬆區別於您可能稍後定義的其他忠誠度相關方案。
* 您也可以使用結構描述來提供有關結構描述的任何其他內容相關資訊。

本教學課程撰寫結構描述以擷取與忠誠度計畫成員相關的資料，因此該結構描述命名為「[!DNL Loyalty Members]「。

## 新增欄位群組 {#field-group}

您現在可以透過新增欄位群組來開始將欄位新增到結構描述。 欄位群組是一或多個欄位的群組，通常搭配使用來描述特定概念。 本教學課程使用欄位群組來說明熟客方案的成員，並擷取關鍵資訊，例如姓名、生日、電話號碼、地址等。

若要新增欄位群組，請選取 **[!UICONTROL 新增]** 在 **[!UICONTROL 欄位群組]** 子區段。

![](../images/tutorials/create-schema/add-field-group-button.png)

新對話方塊隨即出現，顯示可用欄位群組清單。 每個欄位群組僅供特定類別使用，因此對話方塊僅列出與您所選類別相容的欄位群組(在此案例中， [!DNL XDM Individual Profile] 類別)。 如果您使用標準XDM類別，欄位群組的清單將會根據使用率聰明地排序。

![](../images/tutorials/create-schema/field-group-popularity.png)

您可以選取左側邊欄中的其中一個篩選器，將標準欄位群組清單縮小至特定 [產業](../schema/industries/overview.md) 如零售、金融服務及醫療保健。

![](../images/tutorials/create-schema/industry-field-groups.png)

從清單中選取欄位群組後，該群組就會顯示在右側邊欄中。 您可以視需要選取多個欄位群組，在確認前先將每個欄位群組新增至右側欄位中的清單。 此外，圖示會顯示在目前所選欄位群組的右側，可讓您預覽其所提供的欄位結構。

![](../images/tutorials/create-schema/preview-field-group-button.png)

預覽欄位群組時，右側欄中提供欄位群組結構的詳細說明。 您還可以瀏覽提供的畫布中的欄位群組欄位。 當您選取不同欄位時，右側欄會更新，顯示有關問題欄位的詳細資訊。 選取 **[!UICONTROL 返回]** 當您完成預覽以返回欄位群組選擇對話方塊時。

![](../images/tutorials/create-schema/preview-field-group.png)

在本教學課程中，選取 **[!UICONTROL 人口統計細節]** 欄位群組，然後選取 **[!UICONTROL 新增欄位群組]**.

![](../images/tutorials/create-schema/demographic-details.png)

結構畫布會重新出現。 此 **[!UICONTROL 欄位群組]** 區段現在列出&quot;[!UICONTROL 人口統計細節]」和 **[!UICONTROL 結構]** 區段包含欄位群組貢獻的欄位。 您可以選取欄位群組名稱在 **[!UICONTROL 欄位群組]** 區段來反白顯示在畫布中提供的特定欄位。

![](../images/tutorials/create-schema/demographic-details-structure.png)

此欄位群組提供頂層名稱下的數個欄位 `person` 資料型別為「[!UICONTROL 個人]「。 這組欄位說明個人的相關資訊，包括姓名、出生日期和性別。

>[!NOTE]
>
>請記住，欄位可能使用純量型別（例如字串、整數、陣列或日期），以及在中定義的任何資料型別（代表通用概念的一組欄位） [!DNL Schema Registry].

請注意 `name` 欄位的資料型別為&quot;[!UICONTROL 全名]「」，表示它也描述一個通用概念並包含與名稱相關的子欄位，例如名字、姓氏、尊稱和字尾。

選取畫布中的不同欄位，以顯示它們為結構描述結構貢獻的任何其他欄位。

## 新增更多欄位群組 {#field-group-2}

您現在可以重複相同的步驟來新增另一個欄位群組。 當您檢視 **[!UICONTROL 新增欄位群組]** 這次對話方塊中，請留意「[!UICONTROL 人口統計細節]「欄位群組已灰顯，且無法選取其旁邊的核取方塊。 這可防止您不小心複製已包含在目前結構描述中的欄位群組。

在本教學課程中，請選取標準欄位群組 **[!UICONTROL 個人聯絡詳細資訊]** 和 **[!UICONTROL 熟客方案細節]** 從清單中，然後選取 **[!UICONTROL 新增欄位群組]** 以將其新增至結構描述。

![](../images/tutorials/create-schema/more-field-groups.png)

畫布會重新出現，並在下方列出新增的欄位群組 **[!UICONTROL 欄位群組]** 在 **[!UICONTROL 組合]** 區段，以及其新增至結構描述結構的複合欄位。

![](../images/tutorials/create-schema/updated-structure.png)

## 定義自訂欄位群組 {#define-field-group}

此 [!UICONTROL 熟客會員] 結構描述用於擷取和忠誠度計畫會員相關的資料，以及標準 [!UICONTROL 熟客方案細節] 您新增到結構描述的欄位群組會提供大部分這類資訊，包括方案型別、點、加入日期等。

但是，在某些情況下，您可能會想要包含標準欄位群組未涵蓋的其他自訂欄位，以便達成您的使用案例。 新增自訂忠誠度欄位時，您有兩個選項：

1. 建立新的自訂欄位群組以擷取這些欄位。 此方法將於本教學課程中說明。
1. 擴充標準 [!UICONTROL 熟客方案細節] 具有自訂欄位的欄位群組。 這會導致 [!UICONTROL 熟客方案細節] 轉換為自訂欄位群組，而原始標準欄位群組將不再可用。 請參閱 [!UICONTROL 結構描述] UI指南，瞭解更多關於 [將自訂欄位新增至標準欄位群組的結構](../ui/resources/schemas.md#custom-fields-for-standard-groups).

若要建立新的欄位群組，請選取 **[!UICONTROL 新增]** 在 **[!UICONTROL 欄位群組]** 子區段，就像之前一樣，但這次選取 **[!UICONTROL 建立新欄位群組]** 靠近出現的對話方塊頂端。 接著，系統會要求您提供新欄位群組的顯示名稱和說明。 在本教學課程中，將新欄位群組命名為&quot;[!DNL Custom Loyalty Details]&quot;，然後選取 **[!UICONTROL 新增欄位群組]**.

![](../images/tutorials/create-schema/create-new-field-group.png)

>[!NOTE]
>
>與類別名稱一樣，欄位群組名稱應簡短而簡單，說明欄位群組對結構描述有哪些貢獻。 這些也是唯一的，因此您將無法重複使用名稱，因此必須確保它足夠具體。

&quot;[!DNL Custom Loyalty Details]「 」現在應顯示在下 **[!UICONTROL 欄位群組]** 位於畫布左側，但尚未有相關聯的欄位，因此下方不會顯示任何新欄位 **[!UICONTROL 結構]**.

## 新增欄位至欄位群組 {#field-group-fields}

現在您已建立「 」[!DNL Custom Loyalty Details]」欄位群組，現在可以定義欄位群組將貢獻給結構描述的欄位。

若要開始，請選取 **加(+)** 圖示加以識別（位於畫布中的結構描述名稱旁）。

![](../images/tutorials/create-schema/add-field.png)

一個&quot;[!UICONTROL 未命名的欄位]「預留位置會顯示在畫布中，而右邊欄會更新以顯示欄位的設定選項。

![](../images/tutorials/create-schema/untitled-field.png)

在此案例中，結構描述需要物件型別欄位，以詳細描述人員目前的忠誠度等級。 使用右側邊欄中的控制項，開始建立 `loyaltyTier` 型別為「」的欄位[!UICONTROL 物件]」來儲存您的相關欄位。

下 **[!UICONTROL 指派給]**，您必須選取要指派欄位的欄位群組。 請記住，所有結構描述欄位都屬於類別或欄位群組，由於此結構描述使用標準類別，因此您的唯一選項是選取欄位群組。 開始輸入名稱»[!DNL Custom Loyalty Details]「」，然後從清單中選取欄位群組。

完成後，選取 **[!UICONTROL 套用]**.

![](../images/tutorials/create-schema/loyalty-tier-object.png)

變更會套用且新建立的 `loyaltyTier` 物件出現。 由於這是自訂欄位，因此會自動巢狀內嵌於貴組織租使用者ID名稱空間中的物件，前面加底線(`_tenantId` 在此範例中)。

![](../images/tutorials/create-schema/tenant-id.png)

>[!NOTE]
>
>租使用者ID物件的存在表示您新增的欄位包含在您組織的名稱空間中。
>
>換言之，您新增的欄位對您的組織是唯一的，且將儲存於 [!DNL Schema Registry] 僅供貴組織存取的特定區域中。 您必須一律將您定義的欄位新增至租使用者名稱空間，以防止與其他標準類別、欄位群組、資料型別和欄位的名稱衝突。

選取 **加(+)** 圖示加以存取 `loyaltyTier` 物件，以開始新增子欄位。 新的欄位預留位置隨即出現， **[!UICONTROL 欄位屬性]** 區段會顯示在畫布的右側。

![](../images/tutorials/create-schema/new-field-in-loyalty-tier-object.png)

每個欄位都需要下列資訊：

* **[!UICONTROL 欄位名稱]：** 欄位名稱，最好以camelCase撰寫。 不允許使用空格字元。 這是用來在程式碼和其他下游應用程式中參照欄位的名稱。
   * 範例：loyaltyLevel
* **[!UICONTROL 顯示名稱]：** 欄位名稱，以字首大寫表示。 這是檢視或編輯結構描述時，畫布中顯示的名稱。
   * 範例：忠誠度等級
* **[!UICONTROL 型別]：** 欄位的資料型別。 這包括基本純量型別和 [!DNL Schema Registry]. 範例： [!UICONTROL 字串]， [!UICONTROL 整數]， [!UICONTROL 布林值]， [!UICONTROL 個人]， [!UICONTROL 地址]， [!UICONTROL 電話號碼]等。
* **[!UICONTROL 說明]：** 欄位的可選說明應包含最多200個字元。

的第一個欄位 `loyaltyTier` 物件將是一個字串，稱為 `id`，代表忠誠會員目前層級的ID。 每個忠誠度會員的層級ID將是唯一的，因為該公司會根據不同的因素為每個客戶設定不同的忠誠度層級臨界值。 將新欄位的型別設為&quot;[!UICONTROL 字串]「，以及 **[!UICONTROL 欄位屬性]** 截面會填入多個套用限制的選項，包括預設值、格式和最大長度。

![](../images/tutorials/create-schema/string-constraints.png)

從 `id` 會是隨機產生的自由字串，不需要進一步的限制。 選取 **[!UICONTROL 套用]** 以套用您的變更。

![](../images/tutorials/create-schema/id-field-added.png)

## 新增更多欄位至欄位群組 {#field-group-fields-2}

現在您已新增 `id` 欄位，您可以新增其他欄位以擷取忠誠度層級資訊，例如：

* 目前點數臨界值（整數）：成員必須維持在目前層級中的忠誠度點數下限。
* 下一個層級點臨界值（整數）：成員要畢業到下一個層級所必須累積的忠誠度點數。
* 生效日期（日期 — 時間）：忠誠會員加入此階層的日期。

若要將每個欄位新增至結構描述，請選取 **加(+)** 圖示加以存取 `loyalty` 物件並填入必要資訊。

完成後， `loyaltyTier` 物件將包含 `id`， `currentThreshold`， `nextThreshold`、和 `effectiveDate`.

![](../images/tutorials/create-schema/loyalty-tier-object-fields.png)

## 將列舉欄位新增至欄位群組 {#enum}

在中定義欄位時 [!DNL Schema Editor]，您可套用至基本欄位型別，對欄位可包含的資料提供進一步限制。 下表說明這些限制的使用案例：

| 限制 | 描述 |
| --- | --- |
| [!UICONTROL 必需] | 表示資料擷取需要欄位。 任何根據此結構描述上傳至資料集，但不包含此欄位的資料在擷取時將會失敗。 |
| [!UICONTROL 陣列] | 表示欄位包含值陣列，每個都具有指定的資料型別。 例如，在資料型別為&quot;的欄位上使用此限制[!UICONTROL 字串]」指定欄位將包含字串陣列。 |
| [!UICONTROL 列舉與建議值] | 列舉表示此欄位必須包含可能值的列舉清單中的其中一個值。 或者，您也可以使用此選項來只提供字串欄位的建議值清單，而不用限制欄位為這些值。 |
| [!UICONTROL 标识] | 表示此欄位是身分欄位。 提供了有關身分欄位的更多資訊 [在本教學課程的稍後章節](#identity-field). |
| [!UICONTROL 关系] | 雖然結構描述關係可透過使用聯合結構描述和來推斷 [!DNL Real-Time Customer Profile]，這僅適用於共用相同類別的結構描述。 此 [!UICONTROL 關係] constraint表示此欄位根據不同類別參考結構描述的主要身分，這表示兩個結構描述之間的關係。 請參閱教學課程，位置如下： [定義關係](./relationship-ui.md) 以取得詳細資訊。 |

{style="table-layout:auto"}

>[!NOTE]
>
>任何必要、身分或關係欄位會列在左側邊欄中各自的區段中，讓您無論結構描述的複雜性如何，都能輕鬆找到這些欄位。

在本教學課程中， `loyaltyTier` 結構描述中的物件需要新的列舉欄位來說明層級類別，其中值只能是四個可能選項之一。 若要將此欄位新增至結構描述，請選取 **加(+)** 圖示旁邊 `loyaltyTier` 物件，並填寫下列專案的必填欄位： **[!UICONTROL 欄位名稱]** 和 **[!UICONTROL 顯示名稱]**. 對象 **[!UICONTROL 型別]**，選取「[!UICONTROL 字串]「。

![](../images/tutorials/create-schema/tier-class-type.png)

選取欄位型別後，該欄位會出現其他核取方塊，包括的核取方塊 **[!UICONTROL 陣列]**， **[!UICONTROL 列舉與建議值]**， **[!UICONTROL 身分]**、和 **[!UICONTROL 關係]**.

選取 **[!UICONTROL 列舉與建議值]** 核取方塊，然後選取 **[!UICONTROL 列舉]**. 您可以在此處輸入 **[!UICONTROL 值]** （在駝峰式大小寫中）和 **[!UICONTROL 顯示名稱]** （標題大寫中的選填、讀者易記名稱），適用於每個可接受的忠誠度等級類別。

完成所有欄位屬性後，選取 **[!UICONTROL 套用]** 新增 `tierClass` 欄位至 `loyaltyTier` 物件。

![](../images/tutorials/create-schema/tier-class-enum.png)

## 將多欄位物件轉換為資料型別 {#datatype}

此 `loyaltyTier` 物件現在包含數個欄位，並代表可在其他結構描述中使用的通用資料結構。 此 [!DNL Schema Editor] 可讓您透過將物件的結構轉換為資料型別，輕鬆套用可重複使用的多欄位物件。

資料型別允許一致地使用多欄位結構，並且比欄位群組提供更大的彈性，因為它們可以在結構描述內的任何位置使用。 這是透過設定欄位的 **[!UICONTROL 型別]** 值與中定義之任何資料型別之值 [!DNL Schema Registry].

若要轉換 `loyaltyTier` 物件變更為資料型別，請選取 `loyaltyTier` 欄位，然後選取 **[!UICONTROL 轉換為新資料型別]** 在編輯器右側下方的 **[!UICONTROL 欄位屬性]**.

![](../images/tutorials/create-schema/convert-data-type.png)

此時會出現通知，確認已成功轉換物件。 在畫布中，您現在可以看到 `loyaltyTier` 欄位現在有連結圖示，而右邊欄指出其資料型別為&quot;[!DNL Loyalty Tier]「。

![](../images/tutorials/create-schema/loyalty-tier-data-type.png)

在未來的結構描述中，您現在可以將欄位指派為&quot;[!DNL Loyalty Tier]&quot; type且會自動包含ID、層類別、點臨界值和生效日期的欄位。

>[!NOTE]
>
>您也可以建立及編輯自訂資料型別，與編輯結構描述無關。 請參閱指南： [建立和編輯資料型別](../ui/resources/data-types.md) 以取得詳細資訊。

## 搜尋和篩選結構描述欄位

除了基底類別提供的欄位外，您的結構描述現在包含數個欄位群組。 使用較大的結構描述時，您可以選取左側邊欄中欄位群組名稱旁的核取方塊，將顯示的欄位篩選為僅為您感興趣的欄位群組提供的欄位。

![](../images/tutorials/create-schema/filter-by-field-group.png)

如果您要在結構描述中尋找特定欄位，也可以使用搜尋列依名稱篩選顯示的欄位，無論這些欄位是在哪個欄位群組下提供。

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>顯示相符欄位時，搜尋功能會考量任何選取的欄位群組篩選器。 如果搜尋查詢未顯示您預期的結果，您可能需要仔細檢查您是否未篩選出任何相關的欄位群組。

## 將結構描述欄位設定為身分欄位 {#identity-field}

結構提供的標準資料結構可用於識別跨多個來源屬於同一個人的資料，並允許各種下游使用案例，例如分段、報告、資料科學分析等。 若要根據個別身分拼接資料，索引鍵欄位必須標示為 [!UICONTROL 身分] 個欄位。

[!DNL Experience Platform] 透過使用，可讓您輕鬆表示身分欄位 **[!UICONTROL 身分]** 核取方塊(位於 [!DNL Schema Editor]. 不過，您必須根據資料的性質，判斷哪個欄位最適合作為身分使用。

例如，可能有數千名忠誠計畫會員屬於相同的忠誠度等級，而數個會員可能共用相同的實體地址。 不過，在此案例中，註冊時，忠誠度計畫的每位成員都會提供其個人電子郵件地址。 由於個人電子郵件地址通常由一人管理，因此欄位 `personalEmail.address` (由 [!UICONTROL 個人聯絡詳細資訊] 欄位群組)是身分欄位的良好候選項。

>[!IMPORTANT]
>
>以下概述的步驟包括如何將身分描述項新增到現有結構描述欄位。 除了在結構本身的結構中定義身分欄位外，您也可以使用 `identityMap` 欄位以包含身分資訊。
>
>如果您打算使用 `identityMap`，請記住，這會覆寫您直接新增到結構描述的任何主要身分。 請參閱以下小節： `identityMap` 在 [結構描述組合指南基本概念](../schema/composition.md#identityMap) 以取得詳細資訊。

選取 `personalEmail.address` 欄位，以及 **[!UICONTROL 身分]** 核取方塊會顯示在 **[!UICONTROL 欄位屬性]**. 核取方塊和選項，將此項設為 **[!UICONTROL 主要身分]** 出現。 也請選取此方塊。

>[!NOTE]
>
>每個結構描述只能包含一個主要身分欄位。 一旦結構描述欄位被設定為主要身分識別，如果您稍後嘗試在結構描述中設定另一個身分識別欄位為主要身分識別，將會收到錯誤訊息。

接下來，您必須提供 **[!UICONTROL 身分名稱空間]** 從下拉式清單中的預先定義名稱空間清單。 由於此欄位是客戶的電子郵件地址，請選取&quot;[!UICONTROL 電子郵件]」從下拉式清單中選取。 選取 **[!UICONTROL 套用]** 若要確認更新 `personalEmail.address` 欄位。

![](../images/tutorials/create-schema/primary-identity.png)

>[!NOTE]
>
>如需標準名稱空間及其定義的清單，請參閱 [[!DNL Identity Service] 檔案](../../identity-service/troubleshooting-guide.md#standard-namespaces).

套用變更後，的圖示 `personalEmail.address` 顯示指紋符號，表示它現在是身分欄位。 此欄位也會列於下方的左側邊欄中 **[!UICONTROL 身分]**.

![](../images/tutorials/create-schema/identity-applied.png)

現在，所有資料已擷取至 `personalEmail.address` 欄位將用來協助識別該個人，並將該客戶的單一檢視拼接在一起。 若要進一步瞭解在中使用身分識別 [!DNL Experience Platform]，請檢閱 [[!DNL Identity Service]](../../identity-service/home.md) 說明檔案。

## 啟用結構描述以用於 [!DNL Real-Time Customer Profile] {#profile}

[[!DNL Real-Time Customer Profile]](../../profile/home.md) 在中運用身分資料 [!DNL Experience Platform] 以提供每個個別客戶的整體檢視。 此服務可為客戶建立穩固的360度客戶屬性設定檔，以及客戶在任何整合系統的每次互動建立時間戳記帳戶 [!DNL Experience Platform].

為了啟用結構描述以用於 [!DNL Real-Time Customer Profile]，必須定義主要身分。 如果您嘗試在未先定義主要身分的情況下啟用結構描述，將會收到錯誤訊息。

![](../images/tutorials/create-schema/missing-primary-identity.png)

若要啟用「熟客會員」綱要以用於以下專案： [!DNL Profile]，從選取畫布中的結構描述標題開始。

在編輯器的右側，會顯示有關結構的資訊，包括其顯示名稱、說明和型別。 除了此資訊外， **[!UICONTROL 設定檔]** 切換按鈕。

![](../images/tutorials/create-schema/profile-toggle.png)

選取 **[!UICONTROL 設定檔]** 畫面隨即顯示彈出視窗，要求您確認要為其啟用結構描述 [!DNL Profile].

![](../images/tutorials/create-schema/enable-profile.png)

>[!WARNING]
>
>一旦為以下專案啟用結構描述 [!DNL Real-Time Customer Profile] 並儲存，則無法停用。

選取 **[!UICONTROL 啟用]** 以確認您的選擇。 您可以選取 **[!UICONTROL 設定檔]** 如果您願意，可再次切換以停用結構描述，但一旦結構描述儲存了 [!DNL Profile] 已啟用，則無法再停用。

## 後續步驟和其他資源

現在您已經完成撰寫結構描述，您可以在畫布中看到完整的結構描述。 選取 **[!UICONTROL 儲存]** 且結構描述將儲存至 [!DNL Schema Library]，可供 [!DNL Schema Registry].

您的新結構描述現在可用於將資料擷取到 [!DNL Platform]. 請記住，一旦使用結構描述來擷取資料，只能進行累加性變更。 請參閱 [結構描述組合基本概念](../schema/composition.md) 以取得架構版本設定的詳細資訊。

您現在可以依照教學課程進行： [在UI中定義結構描述關係](./relationship-ui.md) 將新的關係欄位新增至「忠誠會員」結構描述。

「忠誠會員」方案也可供檢視和管理 [!DNL Schema Registry] API。 若要開始使用API，請先閱讀 [[!DNL Schema Registry API] 開發人員指南](../api/getting-started.md).

### 視訊資源

>[!WARNING]
>
>此 [!DNL Platform] 以下影片中顯示的UI已過期。 請參閱上述檔案，瞭解最新的UI熒幕擷取畫面及功能。

以下影片說明如何在中建立簡單的結構描述 [!DNL Platform] UI。

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

以下影片旨在加深您對使用欄位群組和類別的瞭解。

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## 附录

以下小節提供有關使用的額外資訊 [!DNL Schema Editor].

### 建立新類別 {#create-new-class}

[!DNL Experience Platform] 提供根據貴組織獨有的類別來定義結構描述的彈性。 若要瞭解如何建立新類別，請參閱以下指南中的 [在UI中建立和編輯類別](../ui/resources/classes.md#create).

### 變更結構描述的類別 {#change-class}

您可以在儲存結構描述之前，在初始構成程式期間隨時變更結構描述的類別。

>[!WARNING]
>
>為結構描述重新指派類別時應格外謹慎。 欄位群組僅與某些類別相容，因此變更類別將會重設畫布和您已新增的任何欄位。

若要瞭解如何變更結構描述的類別，請參閱以下指南中的 [在UI中管理結構描述](../ui/resources/schemas.md#change-class).
