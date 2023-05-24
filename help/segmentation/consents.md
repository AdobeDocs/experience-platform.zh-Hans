---
keywords: Experience Platform；首頁；熱門主題；選擇退出；分段；分段服務；榮譽選擇退出；選擇退出；選擇退出；同意；共用；收集；
solution: Experience Platform
title: 在區段中接受同意
description: 瞭解如何在區段操作中遵循個人資料收集和分享的客戶同意偏好設定。
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# 在區段中接受同意

法律隱私權法規，例如 [!DNL California Consumer Privacy Act] (CCPA)給予消費者選擇退出收集其個人資料或與第三方分享的權利。 Adobe Experience Platform提供標準Experience Data Model (XDM)元件，旨在擷取即時客戶個人檔案資料中的這些客戶同意偏好設定。

如果客戶撤回或拒絕同意分享其個人資料，貴組織在產生行銷活動的受眾時，務必遵循該偏好設定。 本檔案說明如何使用Experience Platform使用者介面，將客戶同意值整合到您的區段定義中。

## 快速入门

遵循客戶同意值需要瞭解各種 [!DNL Adobe Experience Platform] 涉及的服務。 開始進行本教學課程之前，請務必熟悉下列服務：

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md)：Platform組織客戶體驗資料的標準化架構。
* [[!DNL Real-Time Customer Profile]](../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的客戶設定檔。
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md)：可讓您從以下專案建立受眾區段： [!DNL Real-Time Customer Profile] 資料。

## 同意結構描述欄位

為了遵循客戶同意和偏好設定，屬於您其中一部分的結構描述之一 [!UICONTROL XDM個別設定檔] 聯合結構描述必須包含標準欄位群組 **[!UICONTROL 同意和偏好設定]**.

有關欄位群組提供的每個屬性的結構和預期使用案例的詳細資訊，請參閱 [同意和偏好設定參考指南](../xdm/field-groups/profile/consents.md). 有關如何將欄位群組新增到結構描述的逐步指示，請參閱 [XDM UI指南](../xdm/ui/resources/schemas.md#add-field-groups).

將欄位群組新增至後 [啟用設定檔的結構描述](../xdm/ui/resources/schemas.md#profile) 及其欄位已用來從體驗應用程式擷取同意資料，您可以在區段規則中使用收集的同意屬性。

## 處理分段中的同意

為了確保選擇退出的設定檔不會包含在區段中，必須在建立任何新區段時向現有區段新增並包含特殊欄位。

以下步驟示範如何為兩種型別的選擇退出標幟新增適當的欄位：

1. [!UICONTROL 数据收集]
1. [!UICONTROL 共用資料]

>[!NOTE]
>
>雖然本指南著重於上述兩個選擇退出標幟，但您可以設定區段以一併納入其他同意訊號。 此 [同意和偏好設定參考指南](../xdm/field-groups/profile/consents.md) 提供上述每個選項及其預期使用案例的詳細資訊。

在UI中建立區段時，在 **[!UICONTROL 屬性]**，導覽至 **[!UICONTROL XDM個別設定檔]**，然後選取 **[!UICONTROL 同意和偏好設定]**. 從這裡，您可以看到以下專案的選項 **[!UICONTROL 資料彙集]** 和 **[!UICONTROL 共用資料]**.

![](./images/opt-outs/consents.png)

從選取 **[!UICONTROL 資料彙集]** 類別，然後拖曳 **[!UICONTROL 選擇值]** 放入區段產生器中。 將屬性新增至區段時，您可以指定 [同意值](../xdm/field-groups/profile/consents.md#choice-values) 必須包含或排除的專案。

![](./images/opt-outs/consent-values.png)

其中一種方式是排除選擇退出收集其資料的任何客戶。 若要這麼做，請將運運算元設為 **[!UICONTROL 不等於]**，然後選擇下列值：

* **[!UICONTROL 否（選擇退出）]**
* **[!UICONTROL 「否」（選擇退出）的預設值]**
* **[!UICONTROL 未知]** （若未提供其他資訊，則會假設未提供同意）

![](./images/opt-outs/collect.png)

下 **[!UICONTROL 屬性]** 在左側邊欄中，導覽回 **[!UICONTROL 同意和偏好設定]** 區段，然後選取 **[!UICONTROL 共用資料]**. 拖曳其對應的 **[!UICONTROL 選擇值]** 並選取與相同的值 [!UICONTROL 資料彙集] 選擇值。 確保 **[!UICONTROL 或]** 在兩個屬性之間建立關係。

![](./images/opt-outs/share.png)

同時使用 **[!UICONTROL 資料彙集]** 和 **[!UICONTROL 共用資料]** 新增至區段的同意值，則會從產生的對象中排除選擇退出使用其資料的任何客戶。 從這裡，您可以繼續自訂區段定義，然後再選取 **[!UICONTROL 儲存]** 以完成程式。

## 后续步骤

依照本教學課程所述，您現在應該更瞭解在Experience Platform中建立區段時，如何遵循客戶同意和偏好設定。

如需在Platform中管理同意的詳細資訊，請參閱下列檔案：

* [使用Adobe標準進行同意處理](../landing/governance-privacy-security/consent/adobe/overview.md)
* [使用IAB TCF 2.0標準進行同意處理](../landing/governance-privacy-security/consent/iab/overview.md)