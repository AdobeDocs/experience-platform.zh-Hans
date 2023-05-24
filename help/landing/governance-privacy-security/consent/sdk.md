---
title: 使用Adobe Experience Platform Web SDK處理客戶同意資料
description: 瞭解如何整合Adobe Experience Platform Web SDK，以便在Adobe Experience Platform中處理客戶同意資料。
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: dc269f952d0970cb5be1b28ab91c6006de975df3
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 1%

---

# 整合Platform Web SDK以處理客戶同意資料

Adobe Experience Platform Web SDK可讓您擷取同意管理平台(CMP)產生的客戶同意訊號，並在發生同意變更事件時將其傳送至Adobe Experience Platform。

**SDK不會與任何立即可用的CMP進行介面**. 您可以自行決定如何將SDK整合至您的網站、接聽CMP中的同意變更，以及呼叫適當的命令。 本檔案提供如何將CMP與Platform Web SDK整合的一般指引。

## 先决条件 {#prerequisites}

本教學課程假設您已決定如何在CMP中產生同意資料，並建立資料集，其中包含符合Adobe標準或IAB透明與同意架構(TCF) 2.0標準的同意欄位。 如果您尚未建立此資料集，請先參閱下列教學課程，然後再返回本指南：

* [使用Adobe標準建立資料集](./adobe/dataset.md)
* [使用TCF 2.0標準建立資料集](./iab/dataset.md)

本指南會遵循在UI中使用標籤擴充功能設定SDK的工作流程。 如果您不想使用擴充功能，且想要直接在網站上內嵌獨立SDK版本，請參閱下列檔案，而非本指南：

* [配置数据流](../../../edge/datastreams/overview.md)
* [安裝SDK](../../../edge/fundamentals/installing-the-sdk.md)
* [設定SDK以使用同意命令](../../../edge/consent/supporting-consent.md)

本指南中的安裝步驟需要您實際瞭解標籤擴充功能以及它們在Web應用程式中的安裝方式。 如需詳細資訊，請參閱下列檔案：

* [标记概述](../../../tags/home.md)
* [快速入門手冊](../../../tags/quick-start/quick-start.md)
* [发布概述](../../../tags/ui/publishing/overview.md)

## 设置数据流

為了讓SDK將資料傳送至Experience Platform，您必須先設定資料流。 在資料收集UI或Experience Platform UI中，選取 **[!UICONTROL 資料串流]** 左側導覽列中。

建立新資料流或選取要編輯的現有資料流後，選取旁的切換按鈕 **[!UICONTROL Adobe Experience Platform]**. 接下來，使用下列值完成表單。

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| 資料流欄位 | 值 |
| --- | --- |
| [!UICONTROL 沙盒] | 平台名稱 [沙箱](../../../sandboxes/home.md) 包含設定資料流所需的串流連線和資料集。 |
| [!UICONTROL 事件資料集] | 一個 [!DNL XDM ExperienceEvent] 您打算使用SDK將事件資料傳送至的資料集。 雖然您需要提供事件資料集才能建立Platform資料流，但請注意，下游執行工作流程不會遵循透過事件傳送的同意資料。 |
| [!UICONTROL 設定檔資料集] | 此 [!DNL Profile] — 已啟用資料集，其中包含您建立的客戶同意欄位 [較早](#prerequisites). |

完成後，選取 **[!UICONTROL 儲存]** 在熒幕底部，並依照任何其他提示繼續完成設定。

## 安裝及設定Platform Web SDK

依照上節所述建立資料流後，您必須設定Platform Web SDK擴充功能，才能最終在網站上部署。 如果您的標籤屬性上未安裝SDK擴充功能，請選取「 」 **[!UICONTROL 擴充功能]** 在左側導覽列中，後面接著 **[!UICONTROL 目錄]** 標籤。 然後，選取 **[!UICONTROL 安裝]** 可用擴充功能清單中Platform SDK擴充功能底下。

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

設定SDK時，於 **[!UICONTROL Edge Configurations]**，選取您在上一步建立的資料流。

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

選取 **[!UICONTROL 儲存]** 以安裝擴充功能。

### 建立資料元素以設定預設同意

安裝SDK擴充功能後，您可選擇建立資料元素，以代表預設的資料收集同意值(`collect.val`)。 如果您想要根據使用者而有不同的預設值，例如 `pending` 適用於歐盟使用者和 `in` 適用於北美使用者。

在此使用案例中，您可以實作下列專案，以根據使用者的地區設定預設同意：

1. 判斷使用者在網頁伺服器上的地區。
1. 早於 `script` 標籤（內嵌程式碼）時，呈現個別的 `script` 標籤設定 `adobeDefaultConsent` 變數。
1. 設定資料元素，此元素使用 `adobeDefaultConsent` JavaScript變數，並使用此資料元素作為使用者的預設同意值。

如果使用者的區域由CMP決定，您可以改用以下步驟：

1. 處理頁面上的「CMP已載入」事件。
1. 在事件處理常式中，設定 `adobeDefaultConsent` 變數，然後使用JavaScript載入標籤程式庫指令碼。
1. 設定資料元素，此元素使用 `adobeDefaultConsent` JavaScript變數，並使用此資料元素作為使用者的預設同意值。

若要在UI中建立資料元素，請選取 **[!UICONTROL 資料元素]** 在左側導覽中，然後選取 **[!UICONTROL 新增資料元素]** 導覽至資料元素建立對話方塊。

從這裡，您必須建立 [!UICONTROL JavaScript變數] 資料元素依據 `adobeDefaultConsent`. 選取 **[!UICONTROL 儲存]** 完成後。

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

建立資料元素後，請導覽回Web SDK擴充功能設定頁面。 在 [!UICONTROL 隱私權] 區段，選取 **[!UICONTROL 資料元素提供]**，並使用提供的對話方塊來選取您先前建立的預設同意資料元素。

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### 在您的網站上部署擴充功能

完成擴充功能設定後，即可將其整合至您的網站。 請參閱 [發佈指南](../../../tags/ui/publishing/overview.md) 標籤檔案中，以取得有關如何部署已更新程式庫組建的詳細資訊。

## 發出同意變更命令 {#commands}

將SDK擴充功能整合至網站後，您就可以開始使用Platform Web SDK `setConsent` 將同意資料傳送至Platform的命令。

此 `setConsent` 命令會執行兩個動作：

1. 直接在設定檔存放區中更新使用者的設定檔屬性。 這不會將任何資料傳送至Data Lake。
1. 建立 [體驗事件](../../../xdm/classes/experienceevent.md) 會記錄同意變更事件的時間戳記帳戶。 此資料會直接傳送至Data Lake，並可用於追蹤同意偏好設定在一段時間內的變更。

### 何時呼叫 `setConsent`

有兩種情況 `setConsent` 應呼叫您的網站：

1. 同意載入頁面時（換言之，載入每個頁面時）
1. 做為CMP掛接或事件接聽程式的一部分，可偵測同意設定中的變更

### `setConsent` 語法

>[!NOTE]
>
>如需Platform SDK命令常用語法的簡介，請參閱以下檔案： [正在執行命令](../../../edge/fundamentals/executing-commands.md).

此 `setConsent` 命令需要兩個引數：

1. 指出命令型別的字串(在此案例中， `"setConsent"`)
1. 包含單一陣列型別屬性的裝載物件： `consent`. 此 `consent` 陣列必須至少包含一個物件，提供Adobe標準所需的同意欄位。

以下範例顯示Adobe標準的必要同意欄位 `setConsent` 呼叫：

```js
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: {
        val: "y"
      },
      share: {
        val: "y"
      },
      personalize: {
        content: {
          val: "y"
        }
      },
      metadata: {
        time: "2020-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| 裝載屬性 | 描述 |
| --- | --- |
| `standard` | 使用的同意標準。 對於Adobe標準，此值必須設定為 `Adobe`. |
| `version` | 下方所示的同意標準版本號碼 `standard`. 此值必須設定為 `2.0` 以進行Adobe標準的同意處理。 |
| `value` | 客戶更新的同意資訊，提供為XDM物件，符合已啟用設定檔資料集同意欄位的結構。 |

>[!NOTE]
>
>如果您結合使用其他同意標準 `Adobe` (例如 `IAB TCF`)，您可以將其他物件新增至 `consent` 每個標準的陣列。 每個物件都必須包含適當的值 `standard`， `version`、和 `value` 代表同意標準。

以下JavaScript提供處理網站上同意偏好設定變更的函式範例，該函式可用作事件監聽器或CMP掛接中的回呼：

```js
var setConsent = function () {

  // Retrieve the current consent data.
  var categories = getConsentData();

  // If the script is running on a consent change, generate a new timestamp.
  // If the script is running on page load, set the timestamp to when the consent values last changed.
  var now = new Date();
  var collectedAt = consentChanged ? now.toISOString() : categories.collectedAt;

  //  Map the consent values and timestamp to XDM
  var consentXDM = {
    collect: {
      val: categories.collect !== -1 ? "y" : "n"
    },
    personalize: {
      content: {
        val: categories.personalizeContent !== -1 ? "y" : "n"
      }
    },
    share: {
      val: categories.share !== -1 ? "y" : "n"
    },
    metadata: {
      time: collectedAt
    }
  };

  // Pass the XDM object to the Platform Web SDK
  alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: consentXDM
    }]
  });
});
```

## 處理SDK回應

全部 [!DNL Platform SDK] 命令會傳回promise ，指出呼叫成功或失敗。 然後，您可以將這些回應用於其他邏輯，例如向客戶顯示確認訊息。 請參閱以下小節： [處理成功或失敗](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) 請參閱執行SDK命令指南中的特定範例。

一旦您成功建立 `setConsent` 透過SDK進行呼叫時，您可以使用平台UI中的設定檔檢視器，驗證資料是否登陸設定檔存放區。 請參閱以下小節： [依身分瀏覽設定檔](../../../profile/ui/user-guide.md#browse-identity) 以取得詳細資訊。

## 后续步骤

依照本指南，您已將Platform Web SDK擴充功能設定為傳送同意資料給Experience Platform。 如需測試實作的指引，請參閱您正在實作的同意標準檔案：

* [Adobe標準](./adobe/overview.md#test)
* [TCF 2.0標準](./iab/overview.md#test)
