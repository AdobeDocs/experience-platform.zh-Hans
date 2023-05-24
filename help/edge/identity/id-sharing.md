---
title: 行動裝置對網頁和跨網域ID共用
description: 瞭解如何將訪客ID從行動裝置保留至Web屬性，並跨網域保留
keywords: 身分；行動；ID；共用；網域；跨網域；sdk；平台；
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 3b65143e33804b251f888dbe2a69d238b3f4cda3
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 1%

---

# 行動裝置對網頁和跨網域ID共用

## 概述

Adobe Experience Platform Web SDK支援訪客ID共用功能，讓客戶在行動應用程式和行動網站內容之間，以及跨網域更準確地提供個人化體驗。

## 用例 {#use-cases}

### 在行動應用程式和行動網站之間提供一致的個人化

一家服裝公司想要根據客戶的興趣來個人化他們的客戶體驗，並在同時載入WebViews的行動應用程式中保持個人化的準確性。 透過使用行動裝置對網頁ID共用功能，使用者可透過傳遞以下代碼，使用應用程式和行動裝置網頁內容中的相同訪客識別碼，確保向客戶呈現最準確的優惠： [!DNL ECID] 移至行動網頁URL。

### 跨網域提供一致的個人化

擁有多個線上商店的零售商想要根據客戶興趣，在其網域間個人化購物者體驗。 零售商可以使用Web SDK跨網域ID共用功能，根據客戶興趣在所有網域中提供正確的優惠。

### 增強訪客活動報告功能

技術零售商想要改善訪客活動報表，提供訪客從行動應用程式移至其行動網站或其他網域的相關資訊。 使用Web SDK跨網域ID共用功能，行銷團隊可以準確地追蹤訪客的網頁屬性並產生活動報表。

## 先决条件 {#prerequisites}

若要使用行動裝置對網頁和跨網域ID共用，您必須使用 [!DNL Web SDK] 2.11.0版或更新版本。

若為Edge Network行動實作，此功能在 [邊緣網路的身分識別](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) 擴充功能從1.1.0版(iOS和Android)開始。

此功能也與 [!DNL VisitorAPI.js] 1.7.0版或更新版本。

## 行動裝置對網頁識別碼共用 {#mobile-to-web}

使用 `getUrlVariables` 來自的API [邊緣網路的身分識別](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables) 擴充功能，可將識別碼擷取為查詢引數，並在開啟時附加至URL [!DNL webViews].

Web SDK不需額外設定即可接受 `ECID` 查詢字串中的值。

查詢字串引數包括：

* `MCID`：Experience CloudID (`ECID`)
* `MCORGID`：Experience Cloud `orgID` 必須符合 `orgID` 設定於 [!DNL Web SDK].
* `TS`：時間戳記引數不能超過五分鐘。


行動裝置對網頁的ID共用會使用 `adobe_mc` 引數。 當 `adobe_mc` 引數存在且有效， `ECID` 來自查詢字串的資料會自動新增至對Edge Network提出之第一個要求中的身分對應。 所有後續的Edge Network互動都會使用 `ECID`.

如需如何將訪客ID從行動應用程式傳遞至WebView的詳細資訊，請參閱以下說明檔案： [處理網頁檢視](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## 跨網域識別碼共用 {#cross-domain-sharing}

針對跨網域ID共用，Web SDK 2.11.0版新增對 `appendIdentityToUrl` 命令。 使用時，這個指令會產生 `adobe_mc` 查詢字串引數。

該命令接受具有一個屬性的物件， `url`，並傳回具有屬性的物件 `url`.

此命令不會等待任何同意更新。 如果尚未提供同意，則會傳回URL而不變更。

如果 `ECID` 未提供， `/acquire` 將呼叫端點以產生 `ECID`.

以下範例說明客戶如何在其網站上實作跨網域ID共用。

此程式碼會針對頁面上的所有點按，以及點按是否位在相符網域的連結上（在此例中為），新增事件監聽器 `adobe.com` 或 `behance.com`)，將身分新增至URL並在那裡將使用者重新導向。

```js
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

## 使用標籤擴充功能 {#tags-extension}

類似於使用 [!DNL Web SDK]中，不需進行額外設定 [!DNL Tags] 擴充功能，使用透過URL傳遞的身分識別。

若要透過Tags擴充功能使用行動裝置對網頁和跨網域ID共用，您必須使用Tags擴充功能2.12.0版或更新版本。

若要將目前頁面的身分識別共用給其他網域，以下專案中有新動作可用： [!DNL Web SDK] [!DNL Tags] 副檔名。 此動作旨在搭配 **[!UICONTROL 核心 — 按一下]** 事件型別和值比較條件。

請依照所述的步驟操作 [此處](../../tags/ui/managing-resources/rules.md) 若要使用下列組態建立規則：

* [!UICONTROL 事件設定]：
   * **[!UICONTROL 扩展：核心]**
   * **[!UICONTROL 事件型別：按一下]**
   * 選取 **[!UICONTROL 當使用者點選>特定元素]**
   * 輸入 **[!UICONTROL 選擇器]**： `a[href]`. 只要在頁面上使用「 」按一下錨點標籤，此事件就會觸發。 `href` 屬性。

      ![顯示具有上述設定的事件設定的UI影像](assets/id-sharing-event-configuration.png)

* [!UICONTROL 條件設定]
   * **[!UICONTROL 邏輯型別]**： [!UICONTROL 一般]
   * **[!UICONTROL 副檔名]**： [!UICONTROL 核心]
   * **[!UICONTROL 條件型別]**： [!UICONTROL 值比較]
   * **[!UICONTROL 左運算元]**： [!UICONTROL `%this.hostname%`]. 此為特殊資料元素，適用於 [!UICONTROL 核心 — 按一下] 事件並解析為所點按連結的主機名稱。
   * **[!UICONTROL 運運算元]**： [!UICONTROL 符合Regex]
   * **[!UICONTROL 右運算元]**：輸入符合您要共用身分識別的網域的規則運算式。 例如，比對主機名稱結尾為的連結 `adobe.com` 或 `behance.com`，使用此規則運算式： `behance.com$|adobe.com$`. 連結的頁面必須具備 [!DNL Web SDK] 或 [!DNL Visitor ID] 安裝以接受身分。

      ![顯示具有上述設定的條件設定的UI影像](assets/id-sharing-condition-configuration.png)

* [!UICONTROL 操作配置]
   * **[!UICONTROL 副檔名]**： [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL 動作型別]**： [!UICONTROL 使用身分重新導向]
   * **[!UICONTROL 例項]**：選取您的執行個體。 在大多數情況下，您只會設定一個執行個體。 如果您有多個執行個體，請選取具有您要共用之身分的執行個體。

      ![顯示具有上述設定的動作設定的UI影像](assets/id-sharing-action-configuration.png)

此 **[!UICONTROL 使用身分重新導向]** 動作會停止瀏覽器瀏覽至連結。 然後，它會呼叫 `appendIdentityToUrl` 上的方法 [!DNL Web SDK] 執行個體。

最後，會將使用者重新導向至 [!DNL URL] 使用 `adobe_mc` 查詢字串引數已附加。
