---
title: 配置数据流覆盖
description: 了解如何在数据流UI中配置数据流覆盖，并通过Web SDK激活它们。
source-git-commit: ce2e80a7ea7385be98bbcda6a0704cd0814c62b2
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---


# 配置数据流覆盖

数据流覆盖允许您为数据流定义其他配置，这些配置通过Web SDK传递到边缘网络。

这有助于您触发与默认数据流行为不同的数据流行为，而无需创建新数据流或修改现有设置。

数据流配置覆盖是一个两步流程：

1. 首先，您必须在 [“数据流配置”页](configure.md).
2. 然后，您必须通过Web SDK命令或使用Web SDK将覆盖发送到边缘网络 [标记扩展](../extension/web-sdk-extension-configuration.md).

本文介绍了每种支持覆盖类型的端到端数据流配置覆盖过程。

## 在数据流UI中配置数据流覆盖 {#configure-overrides}

数据流配置覆盖允许您修改以下数据流配置：

* Experience Platform事件数据集
* Adobe Target资产令牌
* Audience ManagerID同步容器
* Adobe Analytics报表包

### Adobe Target的数据流覆盖 {#target-overrides}

要为Adobe Target数据流配置数据流覆盖，您必须首先创建Adobe Target数据流。 按照 [配置数据流](configure.md) 和 [Adobe Target](configure.md#target) 服务。

创建数据流后，编辑 [Adobe Target](configure.md#target) 您添加和使用的服务 **[!UICONTROL 资产令牌覆盖]** ，如下图所示。 每行添加一个资产令牌。

![数据流UI屏幕截图，其中显示了Adobe Target服务设置，并突出显示了资产令牌覆盖。](../assets/datastreams/overrides/override-target.png)

添加所需的覆盖后，保存数据流设置。

您现在应该配置了Adobe Target数据流覆盖。 现在，您可以 [通过Web SDK将覆盖内容发送到边缘网络](#send-overrides).

### Adobe Analytics的数据流覆盖 {#analytics-overrides}

要为Adobe Analytics数据流配置数据流覆盖，您必须首先具有 [Adobe Analytics](configure.md#analytics) 数据流已创建。 按照 [配置数据流](configure.md) 和 [Adobe Analytics](configure.md#analytics) 服务。

创建数据流后，编辑 [Adobe Analytics](configure.md#target) 您添加和使用的服务 **[!UICONTROL 报表包覆盖]** ，如下图所示。

选择 **[!UICONTROL 显示批处理模式]** 以启用对报表包覆盖的批量编辑。 您可以复制并粘贴报表包覆盖的列表，每行输入一个报表包。

![数据流UI屏幕截图，其中显示了Adobe Analytics服务设置，并突出显示了报表包覆盖。](../assets/datastreams/overrides/override-analytics.png)

添加所需的覆盖后，保存数据流设置。

您现在应该配置了Adobe Analytics数据流覆盖。 现在，您可以 [通过Web SDK将覆盖内容发送到边缘网络](#send-overrides).

### Experience Platform事件数据集的数据流覆盖 {#event-dataset-overrides}

要为Experience Platform事件数据集配置数据流覆盖，您必须首先具有 [Adobe Experience Platform](configure.md#aep) 数据流已创建。 按照 [配置数据流](configure.md) 和 [Adobe Experience Platform](configure.md#aep) 服务。

创建数据流后，编辑 [Adobe Experience Platform](configure.md#aep) 已添加的服务，然后选择 **[!UICONTROL 添加事件数据集]** 选项来添加一个或多个覆盖事件数据集，如下图所示。

![数据流UI屏幕截图，其中显示了Adobe Experience Platform服务设置，并突出显示了事件数据集覆盖。](../assets/datastreams/overrides/override-aep.png)

添加所需的覆盖后，保存数据流设置。

您现在应该配置了Adobe Experience Platform数据流覆盖。 现在，您可以 [通过Web SDK将覆盖内容发送到边缘网络](#send-overrides).

### 第三方ID同步容器的数据流覆盖 {#container-overrides}

要为第三方ID同步容器配置数据流覆盖，您必须首先创建数据流。 按照 [配置数据流](configure.md) 创建一个。

创建数据流后，转到 **[!UICONTROL 高级选项]** 并启用 **[!UICONTROL 第三方ID同步]** 选项。

然后，使用 **[!UICONTROL 容器ID覆盖]** 部分添加要覆盖默认设置的容器ID，如下图所示。

>[!IMPORTANT]
>
>容器ID必须是数值，如 `1234567`，而不是字符串，例如 `"1234567"`. 如果您通过Web SDK作为容器ID覆盖发送字符串值，则会收到错误。

![数据流UI屏幕截图显示数据流设置，第三方ID同步容器覆盖高亮显示。](../assets/datastreams/overrides/override-container.png)

添加所需的覆盖后，保存数据流设置。

您现在应该配置了ID同步容器覆盖。 现在，您可以 [通过Web SDK将覆盖内容发送到边缘网络](#send-overrides).

## 通过Web SDK将覆盖发送到边缘网络 {#send-overrides}

>[!NOTE]
>
>作为通过Web SDK命令发送配置覆盖的替代方法，您可以将配置覆盖添加到Web SDK [标记扩展](../extension/web-sdk-extension-configuration.md).

之后 [配置数据流覆盖](#configure-overrides) 在数据收集UI中，您现在可以通过Web SDK将覆盖发送到边缘网络。

通过Web SDK将覆盖发送到边缘网络是激活数据流配置覆盖的第二个也是最后一个步骤。

数据流配置覆盖通过 `edgeConfigOverrides` Web SDK命令。 此命令创建传递到 [!DNL Edge Network] 下一个命令，或者 `configure` 命令。

的 `edgeConfigOverrides` 命令创建传递到的数据流覆盖 [!DNL Edge Network] 下一个命令，或者 `configure`，用于每个请求。

在发送配置覆盖时， `configure` 命令中，它包含在以下受支持的命令中。

* [sendEvent](../fundamentals/tracking-events.md)
* [setConsent](../consent/iab-tcf/overview.md)
* [getIdentity](../identity/overview.md)
* [appendIdentityToUrl](../identity/id-sharing.md#cross-domain-sharing)
* [配置](../fundamentals/configuring-the-sdk.md)

全局指定的选项可以被单个命令上的配置选项覆盖。

### 通过发送配置覆盖 `sendEvent` 命令 {#send-event}

以下示例显示了 `sendEvent` 命令。

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

### 通过发送配置覆盖 `configure` 命令 {#send-configure}

以下示例显示了 `configure` 命令。

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

### 负载示例 {#payload-example}

以上示例将生成 [!DNL Edge Network] 有效负载如下所示：

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

