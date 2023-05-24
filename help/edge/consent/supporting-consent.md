---
title: 使用Adobe Experience Platform Web SDK支援客戶同意偏好設定
description: 瞭解如何使用Adobe Experience Platform Web SDK支援同意偏好設定。
keywords: 同意；defaultConsent；預設同意；setConsent；設定檔隱私權欄位群組；體驗事件隱私權欄位群組；隱私權欄位群組；
exl-id: 647e4a84-4a66-45d6-8b05-d78786bca63a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# 支援客戶同意偏好設定

為了尊重使用者的隱私權，在允許SDK針對特定目的使用使用者特定資料之前，您可能需要要求使用者同意。 目前SDK僅允許使用者選擇加入或退出所有用途，但未來Adobe希望針對特定用途提供更精細的控制。

如果使用者選擇加入所有用途，SDK可以執行下列工作：

* 傳送資料至Adobe的伺服器或從中傳送。
* 讀取和寫入Cookie或Web儲存專案。

如果使用者選擇退出所有用途，SDK不會執行任何這些工作。

## 設定同意

根據預設，使用者會選擇加入所有用途。 若要在使用者選擇加入之前阻止SDK執行上述工作，請通過 `"defaultConsent": "pending"` 在SDK設定期間，如下所示：

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

當一般用途的預設同意設定為pending時，嘗試執行任何取決於使用者選擇加入偏好設定的命令(例如 `sendEvent` command)會導致命令在SDK中排入佇列。 直到您將使用者的選擇加入偏好設定傳達給SDK後，才會處理這些命令。

>[!NOTE]
>
>命令僅在記憶體中排入佇列。 它們不會跨頁面載入儲存。

如果您不想收集在設定使用者的選擇加入偏好設定之前發生的事件，您可以傳遞 `"defaultConsent": "out"` 在SDK設定期間。 在您將使用者的選擇加入偏好設定傳達給SDK之前，嘗試執行任何取決於使用者選擇加入偏好設定的命令將不會生效。

>[!NOTE]
>
>目前SDK僅支援單一all或nothing用途。 雖然我們計畫建立更強大的用途或類別集，以對應不同的Adobe功能和產品方案，但目前的實作是全有或全無選擇加入的方法。  這僅適用於Adobe Experience Platform [!DNL Web SDK] 而不是其他AdobeJavaScript程式庫。

此時，您可能會偏好要求使用者在您的使用者介面中選擇加入。 收集使用者的偏好設定後，請將這些偏好設定傳達SDK。

## 透過Adobe Experience Platform Standard通訊同意偏好設定

SDK支援Adobe Experience Platform同意標準1.0版和2.0版。 目前，1.0和2.0標準僅支援自動執行全部或全部不同意的偏好設定。 1.0標準正在逐步淘汰，取而代之的是2.0標準。 2.0標準允許您新增其他同意偏好設定，這些偏好設定可用於手動強制執行同意偏好設定。

### 使用Adobe standard 2.0版

如果您使用Adobe Experience Platform，則需要在您的設定檔結構描述中加入隱私權結構描述欄位群組。 另請參閱 [Adobe Experience Platform中的治理、隱私和安全性](../../landing/governance-privacy-security/overview.md) 以取得有關Adobe standard 2.0版的詳細資訊。您可以將資料新增至與結構描述相對應的下方值物件中 `consents` 的欄位 [!UICONTROL 同意和偏好設定] 設定檔欄位群組。

如果使用者選擇加入，請執行 `setConsent` 收集偏好設定設定為的命令 `y` 如下所示：

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        },
        metadata: {
          time: "2021-03-17T15:48:42-07:00"
        }
      }
    }]
});
```

時間欄位應指定使用者上次更新其同意偏好設定的時間。 如果使用者選擇退出，請執行 `setConsent` 收集偏好設定設定為的命令 `n` 如下所示：

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "n"
        },
        metadata: {
          time: "2021-03-17T15:51:30-07:00"
        }
      }
    }]
});
```

### 使用Adobe standard 1.0版

如果使用者選擇加入，請執行 `setConsent` 命令與 `general` 選項設定為 `in` 如下所示：

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    }]
});
```

如果使用者選擇退出，請執行 `setConsent` 命令與 `general` 選項設定為 `out` 如下所示：

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "out"
      }
    }]
});
```

## 透過IAB TCF標準通訊同意偏好設定

SDK支援記錄透過Interactive Advertising Bureau Europe (IAB) Transparency and Consent Framework (TCF)標準提供的使用者同意偏好設定。 同意字串可透過相同的設定 `setConsent` 命令如下所示：

```javascript
alloy("setConsent", {
    consent: [{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

以這種方式設定同意時，即時客戶設定檔會更新同意資訊。 為了讓此功能發揮作用，設定檔XDM結構描述需要包含 [設定檔隱私權結構描述欄位群組](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). 傳送事件時，需要手動將IAB同意資訊新增至事件XDM物件。 SDK不會自動在事件中包含同意資訊。 若要在事件中傳送同意資訊，請 [體驗事件隱私權欄位群組](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) 需要新增至體驗事件結構描述。

## 在一個請求中傳送多個標準

SDK也支援在要求中傳送多個同意物件。

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        },
        metadata: {
          time: "2021-03-17T15:48:42-07:00"
        }
      }
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## 同意偏好設定的持續性

在您使用向SDK傳達使用者偏好設定後 `setConsent` 命令中，SDK會儲存使用者對Cookie的偏好設定。 下次使用者在瀏覽器中載入您的網站時，SDK將會擷取並使用這些儲存的偏好設定來判斷是否可將事件傳送至Adobe。

您需要單獨儲存使用者偏好設定，才能顯示同意對話方塊與目前的偏好設定。 無法從SDK擷取使用者偏好設定。 為確保使用者偏好設定與SDK保持同步，您可以呼叫 `setConsent` 命令來載入每個頁面。 只有當偏好設定已變更時，SDK才會進行伺服器呼叫。

## 在設定同意時同步身分

當預設同意擱置或取消時， `setConsent` 可能是第一個發出並建立身分的要求。 因此，在第一個要求上同步身分識別可能很重要。 身分對應可以新增至 `setConsent` 命令，就像在 `sendEvent` 命令。 另請參閱 [正在擷取Experience CloudID](../identity/overview.md)
