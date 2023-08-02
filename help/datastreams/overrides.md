---
title: 配置数据流覆盖
description: 了解如何在数据流 UI 中配置数据流覆盖并通过 Web SDK 激活它们。
exl-id: 7829f411-acdc-49a1-a8fe-69834bcdb014
source-git-commit: 32f36d96e3aa6beb72121adcc74f2da0bd2c9473
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 97%

---

# 配置数据流覆盖

数据流覆盖允许您为数据流定义其他配置，这些配置通过 Web SDK 传递到 Edge Network。

这可以帮助您触发与默认数据流行为不同的数据流行为，而无需创建新的数据流或修改现有设置。

数据流配置覆盖是一个两步过程：

1. 首先，您必须在[数据流配置页面](configure.md)中定义数据流配置覆盖。
2. 然后，您必须通过 Web SDK 命令或使用 Web SDK [标记扩展](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)将这些覆盖发送到 Edge Network。

本文介绍每种受支持的覆盖的端到端数据流配置覆盖过程。

>[!IMPORTANT]
>
>数据流覆盖仅支持 [Web SDK](../edge/home.md) 集成。 [移动SDK](https://developer.adobe.com/client-sdks/documentation/) 和 [服务器API](../server-api/overview.md) 集成当前不支持数据流覆盖。

## 在数据流 UI 中配置数据流覆盖 {#configure-overrides}

数据流配置覆盖允许您修改以下数据流配置：

* Experience Platform 事件数据集
* Adobe Target 属性令牌
* Audience Manager ID 同步容器
* Adobe Analytics 报告包

### Adobe Target 的数据流覆盖 {#target-overrides}

要为 Adobe Target 数据流配置数据流覆盖，您必须首先创建 Adobe Target 数据流。按照说明进行操作，使用 [Adobe Target](configure.md#target) 服务[配置数据流](configure.md)。

创建数据流后，编辑您已添加的 [Adobe Target](configure.md#target) 服务，并使用&#x200B;**[!UICONTROL 属性令牌覆盖]**&#x200B;部分添加所需的数据流覆盖，如下图所示。每行添加一个属性令牌。

![数据流 UI 屏幕快照，显示了 Adobe Target 服务设置，并突出显示了属性令牌覆盖。](assets/overrides/override-target.png)

添加所需覆盖后，保存数据流设置。

您现在应已配置 Adobe Target 数据流覆盖。现在，您可以[通过 Web SDK 将覆盖发送到 Edge Network](#send-overrides)。

### Adobe Analytics 的数据流覆盖 {#analytics-overrides}

要为 Adobe Analytics 数据流配置数据流覆盖，您必须首先创建 [Adobe Analytics](configure.md#analytics) 数据流。按照说明进行操作，使用 [Adobe Analytics](configure.md#analytics) 服务[配置数据流](configure.md)。

创建数据流后，编辑您已添加的 [Adobe Analytics](configure.md#target) 服务，并使用&#x200B;**[!UICONTROL 报告包覆盖]**&#x200B;部分添加所需的数据流覆盖，如下图所示。

选择&#x200B;**[!UICONTROL 显示批处理模式]**&#x200B;可启用报告包覆盖的批量编辑。您可以复制并粘贴报告包覆盖列表，每行输入一个报告包。

![数据流 UI 屏幕快照，显示了 Adobe Analytics 服务设置，并突出显示了报告包覆盖。](assets/overrides/override-analytics.png)

添加所需覆盖后，保存数据流设置。

您现在应已配置 Adobe Analytics 数据流覆盖。现在，您可以[通过 Web SDK 将覆盖发送到 Edge Network](#send-overrides)。

### Experience Platform 事件数据集的数据流覆盖 {#event-dataset-overrides}

要为 Experience Platform 事件数据集配置数据流覆盖，您必须首先创建 [Adobe Experience Platform](configure.md#aep) 数据流。按照说明进行操作，使用 [Adobe Experience Platform](configure.md#aep) 服务[配置数据流](configure.md)。

创建数据流后，编辑已添加的 [Adobe Experience Platform](configure.md#aep) 服务并选择&#x200B;**[!UICONTROL 添加事件数据集]**&#x200B;选项以添加一个或多个覆盖事件数据集，如下图所示。

![数据流 UI 屏幕快照，显示了 Adobe Experience Platform 服务设置，并突出显示了事件数据集覆盖。](assets/overrides/override-aep.png)

添加所需覆盖后，保存数据流设置。

您现在应已配置 Adobe Experience Platform 数据流覆盖。现在，您可以[通过 Web SDK 将覆盖发送到 Edge Network](#send-overrides)。

### 第三方 ID 同步容器的数据流覆盖 {#container-overrides}

要为第三方 ID 同步容器配置数据流覆盖，您必须首先创建数据流。按照说明进行操作，[配置数据流](configure.md)以创建一个数据流。

创建数据流后，请转到&#x200B;**[!UICONTROL 高级选项]**&#x200B;并启用&#x200B;**[!UICONTROL 第三方 ID 同步]**&#x200B;选项。

然后，使用&#x200B;**[!UICONTROL 容器 ID 覆盖]**&#x200B;部分添加要覆盖默认设置的容器 ID，如下图所示。

>[!IMPORTANT]
>
>容器 ID 必须是数值，例如 `1234567`，而不是字符串，例如 `"1234567"`。如果您通过 Web SDK 发送字符串值作为容器 ID 覆盖，您将收到错误。

![数据流 UI 屏幕快照，显示了数据流设置，并突出显示了第三方 ID 同步容器覆盖。](assets/overrides/override-container.png)

添加所需覆盖后，保存数据流设置。

您现在应已配置 ID 同步容器覆盖。现在，您可以[通过 Web SDK 将覆盖发送到 Edge Network](#send-overrides)。

## 通过 Web SDK 将覆盖发送到 Edge Network {#send-overrides}

>[!NOTE]
>
>作为通过 Web SDK 命令发送配置覆盖的替代方法，您可以将配置覆盖添加到 Web SDK [标记扩展](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)。

在数据收集 UI 中[配置数据流覆盖](#configure-overrides)后，您现在可以通过 Web SDK 将覆盖发送到 Edge Network。

通过 Web SDK 将覆盖发送到 Edge Network 是激活数据流配置覆盖的第二步，这也是最后一步。

数据流配置覆盖通过 `edgeConfigOverrides` Web SDK 命令发送到 Edge Network。该命令创建数据流覆盖，对于每个请求，这些覆盖通过下一条命令或 `configure` 命令传递给 [!DNL Edge Network]。

`edgeConfigOverrides` 命令创建数据流覆盖，对于每个请求，这些覆盖通过下一条命令或 `configure` 命令传递给 [!DNL Edge Network]。

当使用 `configure` 命令发送配置覆盖时，它包含在以下 Web SDK 命令中。

* [sendEvent](../edge/fundamentals/tracking-events.md)
* [setConsent](../edge/consent/iab-tcf/overview.md)
* [getIdentity](../edge/identity/overview.md)
* [appendIdentityToUrl](../edge/identity/id-sharing.md#cross-domain-sharing)
* [configure](../edge/fundamentals/configuring-the-sdk.md)

全局指定的选项可由各个命令上的配置选项覆盖。

### 通过 `sendEvent` 命令发送配置覆盖 {#send-event}

以下示例显示 `sendEvent` 命令中的配置覆盖的情况。

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
    datastreamId: "{DATASTREAM_ID}"
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

| 参数 | 描述 |
|---|---|
| `edgeConfigOverrides.datastreamId` | 使用此参数可允许单个请求转到与 `configure`命令定义的数据流不同的数据流。 |

### 通过 `configure` 命令发送配置覆盖 {#send-configure}

以下示例显示 `configure` 命令中的配置覆盖的情况。

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  datastreamId: "{DATASTREAM_ID}",
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

### 负载示例 {#payload-example}

上述示例生成一个 [!DNL Edge Network] 负载，如下所示：

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
