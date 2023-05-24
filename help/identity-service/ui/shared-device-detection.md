---
keywords: Experience Platform；首頁；熱門主題；身分服務；身分服務；共用裝置；共用裝置
title: 共用裝置概述(Beta)
description: 共用裝置偵測可識別相同裝置的不同已驗證使用者，以便在身分圖表中更準確地呈現客戶資料
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# 共用裝置偵測概觀(Beta)

>[!IMPORTANT]
>
>此 [!DNL Shared Device Detection] 功能為測試版。 其功能和檔案可能會有所變更。

Adobe Experience Platform [!DNL Identity Service] 透過跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，協助您更好地瞭解客戶及其行為。

[!DNL Shared Device] 是指由超過一個人使用的裝置。 共用裝置的範例包括平板電腦、圖書館電腦和資訊站。 透過 [!DNL Shared Device Detection] 功能，可防止同一裝置的不同使用者合併為單一身分，以便更準確地表示個人。

替換為 [!DNL Shared Device Detection] 您可以：

* 為相同裝置的不同使用者建立個別身分圖表；
* 防止混合使用相同裝置的不同個人的資料；
* 為您的客戶產生更簡潔且更準確的檢視。

>[!TIP]
>
>的設定 [!DNL Shared Device Detection] 必須為資料集啟用設定檔之前完成，因為一旦在中產生圖形，您就無法再修訂設定 [!DNL Identity Service].

## 開始使用 [!DNL Shared Device Detection]

使用 [!DNL Shared Device Detection] 需要瞭解所涉及的各種平台服務。 開始使用之前 [!DNL Shared Device Detection]，請檢閱以下服務的檔案：

* [[!DNL Identity Service]](../home.md)：透過跨裝置和系統橋接身分，更能瞭解個別客戶及其行為。
   * [身分圖表檢視器](./identity-graph-viewer.md)：將身分圖表檢視器視覺化並與其互動，以更加瞭解客戶身分如何拼接在一起，以及拼接方式為何。
   * [身分名稱空間](../namespaces.md)：檢視完整身分的元件，以及身分名稱空間如何讓您區分身分的內容和型別。

## 了解 [!DNL Shared Device Detection]

使用時，請務必瞭解下列術語
[!DNL Shared Device Detection]. 請參閱下表，瞭解瞭解必不可少的術語清單 [!DNL Shared Device Detection].

### 术语

| 术语 | 定义 |
| --- | --- |
| 共用裝置 | 共用裝置是指一個以上個人使用的任何裝置。 共用裝置的範例包括平板電腦、圖書館電腦和資訊站。 |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] 是指允許來自相同裝置不同使用者的資料互相分離的組態設定。 |
| 共用的身分名稱空間 | 共用身分名稱空間代表可由多個使用者使用的裝置。 共用身分名稱空間通常是ECID，但可以設定為其他裝置ID。 |
| 使用者身分名稱空間 | 使用者身分名稱空間代表共用裝置的已驗證（已登入）使用者。 |
| 上次驗證的使用者 | 如果裝置正由多個帳戶登入，則上次驗證的使用者代表上次登入裝置的使用者。 |

{style="table-layout:auto"}

[!DNL Shared Device Detection] 可透過建立兩個名稱空間來運作： **共用的身分名稱空間** 和 **使用者身分名稱空間**.

* 共用身分名稱空間代表可由多個使用者使用的裝置。 Adobe建議客戶使用ECID作為共用裝置識別碼。
* 使用者身分名稱空間會對應至對應至使用者登入ID的身分名稱空間，這可以是使用者的CRM ID、電子郵件地址、雜湊電子郵件或電話號碼。

共用裝置（如平板電腦）只有一個 **共用的身分名稱空間**. 另一方面，共用裝置的每位使用者都有其專屬的 **使用者身分名稱空間** 與其個別登入ID相對應的資訊。 例如，Kevin和Nora分享用於電子商務的平板電腦擁有自己的ECID `1234`，而Kevin擁有自己的使用者身分名稱空間，並已對應至其 `kevin@email.com` 帳戶和Nora擁有自己的使用者身分名稱空間對應到她 `nora@email.com` 帳戶。

[!DNL Shared Device Detection] 可連結共用的身分名稱空間(例如， ECID)與上次驗證使用者的使用者身分名稱空間（登入ID）。

### 身分資料如何傳送至身分圖表

請參考下列範例，協助您瞭解如何 [!DNL Shared Device Detection] 作用：

>[!NOTE]
>
>在此圖表中，共用身分名稱空間已設定為ECID，而使用者身分名稱空間已設定為CRM ID。

![圖表](../images/shared-device/diagram.png)

* Kevin和Nora分享平板電腦來造訪電子商務網站。 不過，他們都有自己的獨立帳戶，各自用來瀏覽和線上購物；
   * 做為共用裝置，平板電腦擁有對應的ECID，代表平板電腦的網頁瀏覽器Cookie ID；
* 假設Kevin使用平板電腦 **登入** 前往其電子商務帳戶以瀏覽耳機，則表示Kevin的CRM ID (**使用者身分名稱空間**)現在與平板電腦的ECID (**共用的身分名稱空間**)。 平板電腦的瀏覽資料現在與Kevin的身分圖表整合。
   * 如果Kevin **登出** 和Nora使用平板電腦 **登入** 前往她自己的帳戶並購買相機，然後她的CRM ID現在會連結至平板電腦的ECID。 因此，平板電腦的瀏覽資料現在與Nora的身分圖表合併。
   * 若為Nora **未登出** Kevin使用平板電腦，但 **未登入**，則平板電腦的瀏覽資料仍會與Nora合併，因為她仍為已驗證的使用者，且她的CRM ID仍連結至平板電腦的ECID。
   * 若為Nora **登出** Kevin使用平板電腦，但 **未登入**，則平板電腦的瀏覽資料仍會與Nora的身分圖表合併，因為作為 **上次驗證的使用者**，她的CRM ID仍與平板電腦的ECID連結。
   * 如果Kevin **登入** 同樣地，他的CRM ID現在會連結至平板電腦的ECID，因為他現在是最後一個已驗證的使用者，而且平板電腦的瀏覽資料現在已合併至他的身分圖表。

### 如何 [!DNL Profile Service] 合併設定檔片段 [!DNL Shared Device Detection] 已啟用

[!DNL Profile Service] 記下設定檔片段和合併的設定檔。 每個個別客戶設定檔都由多個設定檔片段組成，這些片段已合併以形成該客戶的單一檢視。 例如，如果客戶跨多個管道與您的品牌互動，您的組織將有多個與該單一客戶相關的設定檔片段出現在多個資料集中。 將這些片段內嵌至Platform時，會合併在一起，以便為該客戶建立單一設定檔。

時間 [!DNL Shared Device Detection] 已啟用， [!DNL Profile] 根據體驗事件已驗證或未驗證，定義設定檔片段的主要身分

一個 **已驗證的體驗事件** 是使用者登入裝置時完成的動作。 對於已驗證的體驗事件，主要身分是 **使用者身分名稱空間** （登入ID）。 一個 **未驗證的體驗事件** 是由未登入裝置的使用者完成的動作。 對於未驗證的體驗事件，主要身分是 **共用的身分名稱空間** (ECID)。

如需詳細資訊，請參閱  [[!DNL Real-Time Customer Profile] 概觀](../../profile/home.md).

## 共用裝置UI

在Platform UI中選取 **[!UICONTROL 身分]** 從左側導覽列中，然後選取 **[!UICONTROL 身分設定]**.

![identity-dashboard](../images/shared-device/identity-dashboard.png)

此 [!UICONTROL 共用裝置設定] 頁面隨即顯示，提供您設定資料共用裝置設定的介面。 共用裝置設定預設為停用。

啟用後，共用裝置設定可將來自相同裝置不同使用者的資料互相區隔。 此組態設定可讓身分圖表呈現得更清楚、更準確，其中不會將相同裝置的使用者身分合併在一起。

選取 **[!UICONTROL 啟用]** 以開始修改您的共用裝置設定。

![啟用 — 共用裝置](../images/shared-device/enable-shared-device.png)

此 [!UICONTROL 共用的身分名稱空間] 和 [!UICONTROL 使用者身分名稱空間] 設定選項隨即顯示，可讓您修改要使用的身分名稱空間。

![set-namespaces](../images/shared-device/set-namespaces.png)

[!UICONTROL 共用的身分名稱空間] 代表多個不同使用者使用的單一裝置。 此名稱空間一律設為 **[!UICONTROL ECID]** 因為所有平台使用者都使用 **[!UICONTROL ECID]** 作為網頁瀏覽器識別碼。

![shared-identity-name](../images/shared-device/shared-identity-namespace.png)

此 [!UICONTROL 使用者身分名稱空間] 可讓您識別相同裝置的不同使用者，並防止資料合併至相同的身分圖表。

![user-identity-namespace](../images/shared-device/user-identity-namespace.png)

選取 **[!UICONTROL 使用者身分名稱空間]** 搜尋列，然後輸入身分名稱空間或從下拉式選單中選取身分名稱空間。

>[!TIP]
>
>此 [!UICONTROL 使用者身分名稱空間] 應該對應至對應至一般使用者登入ID的身分名稱空間。 選項包括客戶ID、電子郵件和雜湊電子郵件。

![電子郵件](../images/shared-device/emails.png)

一旦您設定了 [!UICONTROL 共用裝置設定]，選取 **[!UICONTROL 儲存]**.

![保存](../images/shared-device/save.png)

會出現一個快顯視窗，提示您確認您的選擇。 選取 **[!UICONTROL 是]** 以完成組態設定。

![confirm](../images/shared-device/confirm.png)
