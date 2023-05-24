---
keywords: Experience Platform；首頁；熱門主題；啟用傳入資料；填入設定檔；填入rtcp；填入的統一設定檔
solution: Experience Platform
title: 啟用傳入來源資料以在UI中填入客戶設定檔
type: Tutorial
description: 來自您來源聯結器的傳入資料可用於擴充和填入您的即時客戶設定檔資料。
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# 啟用傳入來源資料以填入客戶設定檔

來自您來源聯結器的傳入資料可用於擴充和填入 [!DNL Real-Time Customer Profile] 資料。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   - [結構描述組合基本概念](../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   - [結構描述編輯器教學課程](../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

此外，本教學課程需要您已建立並設定來源聯結器。  在UI中建立不同聯結器的教學課程清單可在以下網址找到： [來源聯結器概觀](../../home.md).

## 填入您的 [!DNL Real-Time Customer Profile] 資料

為了豐富客戶設定檔，目標資料集的來源結構描述必須相容以用於 [!DNL Real-Time Customer Profile]. 相容的結構描述符合下列要求：

- 結構描述至少指定一個屬性做為身分屬性。
- 結構描述具有定義為主要身分的身分屬性。
- 資料流中存在對應，其中主要身分是目標屬性。

在來源工作區中，按一下 **[!UICONTROL 瀏覽]** 索引標籤以列出基礎連線。 在顯示的清單中，尋找包含您要填入設定檔之資料流的連線。 按一下連線的名稱以存取其詳細資訊。

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

連線的 **[!UICONTROL 來源活動]** 畫面隨即顯示，顯示連線正在將來源資料擷取的資料集。 按一下您要啟用的資料集名稱 [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

此 **[!UICONTROL 資料集活動]** 畫面隨即顯示。 此 **[!UICONTROL 屬性]** 畫面右側的欄會顯示資料集的詳細資訊，並包含 **[!UICONTROL 設定檔]** 切換並連結至資料集所遵守的結構描述。 按一下結構描述的名稱，即可檢視其組成。

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

此 **[!UICONTROL 結構描述編輯器]** 會出現，並在中央畫布中顯示結構描述的結構。 在畫布中，選取要設定為主要身分的欄位。 在 **[!UICONTROL 欄位屬性]** 標籤中，選取 **[!UICONTROL 身分]** 核取方塊，然後 **[!UICONTROL 主要身分]**. 最後，選取適當的 **[!UICONTROL 身分名稱空間]**，然後按一下 **[!UICONTROL 套用]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

按一下結構描述結構的頂層物件，然後 **[!UICONTROL 結構描述屬性]** 欄會出現。 為以下專案啟用結構描述： [!DNL Profile] 切換 **[!UICONTROL 設定檔]** 切換。 按一下 **[!UICONTROL 儲存]** 以完成變更。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

現在結構描述已啟用 [!DNL Profile]，返回 **[!UICONTROL 資料集活動]** 畫面並啟用資料集 [!DNL Profile] 按一下 **[!UICONTROL 設定檔]** 切換於 **[!UICONTROL 屬性]** 欄。

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

同時啟用結構描述和資料集 [!DNL Profile]，擷取至該資料集的資料現在也會填入客戶設定檔。

>[!NOTE]
>
>最近啟用的資料集中的現有資料不會被 [!DNL Profile].

## 后续步骤

依照本教學課程，您已成功啟用的傳入資料 [!DNL Profile] 母體。 如需詳細資訊，請參閱 [[!DNL Real-Time Customer Profile] 概觀](../../../profile/home.md).
