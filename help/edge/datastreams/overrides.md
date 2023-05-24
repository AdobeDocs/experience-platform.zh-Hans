---
title: 設定資料流覆寫
description: 瞭解如何在資料串流UI中設定資料串流覆寫，並透過Web SDK啟用它們。
exl-id: 7829f411-acdc-49a1-a8fe-69834bcdb014
source-git-commit: d76d596818db67c99aca0606b6b6fb1a9aa977aa
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# 設定資料流覆寫

資料串流覆寫可讓您為資料串流定義其他設定，這些設定會透過Web SDK傳遞到Edge Network。

這有助於您觸發與預設資料流行為不同的資料流行為，而不會建立新的資料流或修改現有的設定。

資料流設定覆寫是兩個步驟的程式：

1. 首先，您必須在以下位置定義資料流設定覆寫： [資料流設定頁面](configure.md).
2. 接著，您必須透過Web SDK命令或使用Web SDK將覆寫傳送至Edge Network [標籤延伸模組](../extension/web-sdk-extension-configuration.md).

本文說明每種支援覆寫型別的端對端資料流設定覆寫程式。

## 在資料流UI中設定資料流覆寫 {#configure-overrides}

資料流設定覆寫可讓您修改下列資料流設定：

* Experience Platform事件資料集
* Adobe Target屬性Token
* Audience ManagerID同步容器
* Adobe Analytics報表套裝

### Adobe Target的資料流覆寫 {#target-overrides}

若要設定Adobe Target資料流的資料流覆寫，您必須先建立Adobe Target資料流。 依照指示進行 [設定資料串流](configure.md) 使用 [Adobe Target](configure.md#target) 服務。

建立資料流後，請編輯 [Adobe Target](configure.md#target) 您所新增並使用的 **[!UICONTROL 屬性Token覆寫]** 區段來新增所需的資料流覆寫，如下圖所示。 每行新增一個屬性Token。

![資料串流UI熒幕擷圖顯示Adobe Target服務設定，並反白顯示屬性Token覆寫。](../assets/datastreams/overrides/override-target.png)

新增所需的覆寫後，請儲存資料流設定。

您現在應該已設定Adobe Target資料流覆寫。 現在您可以 [透過Web SDK將覆寫傳送至Edge Network](#send-overrides).

### Adobe Analytics的資料流覆寫 {#analytics-overrides}

若要設定Adobe Analytics資料串流的資料串流覆寫，您必須先設定 [Adobe Analytics](configure.md#analytics) 已建立資料流。 依照指示進行 [設定資料串流](configure.md) 使用 [Adobe Analytics](configure.md#analytics) 服務。

建立資料流後，請編輯 [Adobe Analytics](configure.md#target) 您所新增並使用的 **[!UICONTROL 報表套裝覆寫]** 區段來新增所需的資料流覆寫，如下圖所示。

選取 **[!UICONTROL 顯示批次模式]** 以啟用報表套裝覆寫的批次編輯。 您可以複製並貼上報表套裝覆寫清單，每行輸入一個報表套裝。

![資料串流UI熒幕擷圖顯示Adobe Analytics服務設定，並反白顯示報表套裝覆寫。](../assets/datastreams/overrides/override-analytics.png)

新增所需的覆寫後，請儲存資料流設定。

您現在應該已設定Adobe Analytics資料流覆寫。 現在您可以 [透過Web SDK將覆寫傳送至Edge Network](#send-overrides).

### Experience Platform事件資料集的資料流覆寫 {#event-dataset-overrides}

若要設定Experience Platform事件資料集的資料流覆寫，您必須先設定 [Adobe Experience Platform](configure.md#aep) 已建立資料流。 依照指示進行 [設定資料串流](configure.md) 使用 [Adobe Experience Platform](configure.md#aep) 服務。

建立資料流後，請編輯 [Adobe Experience Platform](configure.md#aep) 您新增的服務，並選取 **[!UICONTROL 新增事件資料集]** 新增一或多個覆寫事件資料集的選項，如下圖所示。

![資料串流UI熒幕擷圖顯示Adobe Experience Platform服務設定，並反白顯示事件資料集覆寫。](../assets/datastreams/overrides/override-aep.png)

新增所需的覆寫後，請儲存資料流設定。

您現在應該已設定Adobe Experience Platform資料流覆寫。 現在您可以 [透過Web SDK將覆寫傳送至Edge Network](#send-overrides).

### 第三方ID同步容器的資料流覆寫 {#container-overrides}

若要設定第三方ID同步容器的資料流覆寫，您必須先建立資料流。 依照指示進行 [設定資料串流](configure.md) 以建立一個。

建立資料流後，請前往 **[!UICONTROL 進階選項]** 並啟用 **[!UICONTROL 協力廠商ID同步]** 選項。

然後，使用 **[!UICONTROL 容器ID覆蓋]** 區段，新增您要覆寫預設設定的容器ID，如下圖所示。

>[!IMPORTANT]
>
>容器ID必須是數值，例如 `1234567`，而非字串，例如 `"1234567"`. 如果您透過Web SDK傳送字串值做為容器ID覆寫，則會收到錯誤。

![顯示資料流設定的Datastreams UI熒幕擷取畫面，反白顯示協力廠商ID同步容器覆寫。](../assets/datastreams/overrides/override-container.png)

新增所需的覆寫後，請儲存資料流設定。

您現在應該已設定ID同步容器覆寫。 現在您可以 [透過Web SDK將覆寫傳送至Edge Network](#send-overrides).

## 透過Web SDK將覆寫傳送至Edge Network {#send-overrides}

>[!NOTE]
>
>除了透過Web SDK命令傳送設定覆寫之外，您也可以將設定覆寫新增至Web SDK [標籤延伸模組](../extension/web-sdk-extension-configuration.md).

晚於 [設定資料流覆寫](#configure-overrides) 在資料收集UI中，您現在可以透過Web SDK將覆寫傳送至Edge Network。

透過Web SDK將覆寫傳送至Edge Network是啟動資料流設定覆寫的第二個也是最後一個步驟。

資料流設定覆寫會透過 `edgeConfigOverrides` Web SDK命令。 這個命令會建立傳遞至的資料流覆寫 [!DNL Edge Network] 下一個指令，或者，如果是 `configure` 命令，適用於每個要求。

此 `edgeConfigOverrides` 命令會建立傳遞至的資料流覆寫 [!DNL Edge Network] 下一個指令，或者，如果是 `configure`，以取得每個要求。

當設定覆寫隨以下專案傳送時： `configure` 命令，它包含在下列支援的命令中。

* [sendEvent](../fundamentals/tracking-events.md)
* [setConsent](../consent/iab-tcf/overview.md)
* [getIdentity](../identity/overview.md)
* [appendIdentityToUrl](../identity/id-sharing.md#cross-domain-sharing)
* [設定](../fundamentals/configuring-the-sdk.md)

個別命令上的組態選項可覆寫全域指定的選項。

### 透過傳送設定覆寫 `sendEvent` 命令 {#send-event}

以下範例顯示設定覆寫在 `sendEvent` 命令。

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      datasets: {
        event: {
          datasetId: "MyOverrideDataset"
        },
        profile: {
          datasetId: "www"
        }
      }
    },
    com_adobe_analytics: {
      reportSuites: [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
    },
    com_adobe_identity: {
      idSyncContainerId: "1234567"
    },
    com_adobe_target: {
      propertyToken: "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  }
});
```

### 透過傳送設定覆寫 `configure` 命令 {#send-configure}

以下範例顯示設定覆寫在 `configure` 命令。

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  edgeConfigId: "etc",
  orgId: "org",
  debugEnabled: true,
  edgeConfigOverrides: {
    "com_adobe_experience_platform": {
      "datasets": {
        "event": { 
          datasetId: "MyOverrideDataset"
        },
        "profile": { 
          datasetId: "www"
        }
      }
    },
    "com_adobe_analytics": {
      "reportSuites": [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
      ]
    },
    "com_adobe_identity": {
      "idSyncContainerId": "1234567"
    },
    "com_adobe_target": {
      "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  },
  onBeforeEventSend: function() { /* … */ });
};
```

### 裝載範例 {#payload-example}

上述範例會產生 [!DNL Edge Network] 裝載看起來像這樣：

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "MyOverrideDataset"
          },
          "profile": {
            "datasetId": "www"
          }
        }
      },
      "com_adobe_analytics": {
        "reportSuites": [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
      },
      "com_adobe_identity": {
        "idSyncContainerId": "1234567"
      },
      "com_adobe_target": {
        "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
      }
    },
    "state": {  }
  },
  "events": [  ],
  "query": {
    "identity": {
      "fetch": [
        "ECID"
      ]
    }
  }
}
```
