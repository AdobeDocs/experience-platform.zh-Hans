---
title: 配置数据流覆盖
description: 了解如何在数据流 UI 中配置数据流覆盖并通过 Web SDK 激活它们。
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '1450'
ht-degree: 60%

---

# 配置数据流覆盖

数据流覆盖允许您为数据流定义其他配置，这些配置通过 Web SDK 传递到 Edge Network。

这有助于触发与默认数据流行为不同的数据流行为，而无需创建数据流或修改现有设置。

数据流配置覆盖分为两步：

1. 首先，您必须在以下位置定义数据流配置覆盖 [数据流配置页面](configure.md).
2. 然后，您必须通过以下方式之一将覆盖发送到Edge Network：
   * 通过 `sendEvent` 或 `configure` [Web SDK](#send-overrides-web-sdk) 命令。
   * 通过Web SDK [标记扩展](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).
   * 通过Mobile SDK [sendEvent](#send-overrides-mobile-sdk) 命令。

本文介绍每种受支持的覆盖的端到端数据流配置覆盖过程。

>[!IMPORTANT]
>
>数据流覆盖仅支持 [Web SDK](../edge/home.md) 和 [移动SDK](https://developer.adobe.com/client-sdks/home/) 集成。 [服务器API](../server-api/overview.md) 集成当前不支持数据流覆盖。
><br>
>在需要将不同的数据发送到不同的数据流时应使用数据流覆盖。请勿对个性化用例或同意数据使用数据流覆盖。

## 用例 {#use-cases}

为了帮助您更好地了解如何以及何时使用数据流覆盖，以下是 Adobe Experience Platform 客户可使用此功能解决的一些用例。

**多区域数据收集**

一家公司对于其开展经营的不同国家/地区拥有不同的网站或子域。其中[配置了](configure.md)单独的数据流，这些数据流具有相应的 Analytics 特有的报表包、国家/地区特有的 Adobe Target 属性令牌、国家/地区特有的架构、数据集、Journey Optimizer 配置等等。该公司还有一套全球配置，其中汇集所有国家/地区特有的数据。

通过使用数据流覆盖，该公司可动态地将数据的流动切换到不同的数据流，取代将数据发送到一个数据流的默认行为。

一个常见的使用案例可能是将数据发送到特定于国家/地区的数据流，也发送到客户在其中执行重要操作（如下订单或更新其用户配置文件）的全球数据流。

**为不同的业务部门区分配置文件和标识**

具有多个业务部门的公司希望使用多个Experience Platform沙盒来存储特定于每个业务部门的数据。

该公司可使用数据流覆盖确保每个业务部门都有自己的数据流以通过它接收数据，而非将数据发送到默认数据流。

## 在数据流 UI 中配置数据流覆盖 {#configure-overrides}

数据流配置覆盖允许您修改以下数据流配置：

* Experience Platform 事件数据集
* Adobe Target 属性令牌
* Audience Manager ID 同步容器
* Adobe Analytics 报告包

### Adobe Target 的数据流覆盖 {#target-overrides}

要为 Adobe Target 数据流配置数据流覆盖，您必须首先创建 Adobe Target 数据流。按照说明进行操作，使用 [Adobe Target](configure.md#target) 服务[配置数据流](configure.md)。

创建数据流后，编辑 [Adobe Target](configure.md#target) 您已添加并使用 **[!UICONTROL 资产令牌覆盖]** 部分来添加所需的数据流覆盖，如下图所示。 每行添加一个属性令牌。

![数据流 UI 屏幕快照，显示了 Adobe Target 服务设置，并突出显示了属性令牌覆盖。](assets/overrides/override-target.png)

添加所需覆盖后，保存数据流设置。

您现在应已配置 Adobe Target 数据流覆盖。现在，您可以[通过 Web SDK 将覆盖发送到 Edge Network](#send-overrides)。

### Adobe Analytics 的数据流覆盖 {#analytics-overrides}

要为 Adobe Analytics 数据流配置数据流覆盖，您必须首先创建 [Adobe Analytics](configure.md#analytics) 数据流。按照说明进行操作，使用 [Adobe Analytics](configure.md#analytics) 服务[配置数据流](configure.md)。

创建数据流后，编辑 [Adobe Analytics](configure.md#target) 您已添加并使用 **[!UICONTROL 报表包覆盖]** 部分来添加所需的数据流覆盖，如下图所示。

选择&#x200B;**[!UICONTROL 显示批处理模式]**&#x200B;可启用报告包覆盖的批量编辑。您可以复制并粘贴报告包覆盖列表，每行输入一个报告包。

![数据流 UI 屏幕快照，显示了 Adobe Analytics 服务设置，并突出显示了报告包覆盖。](assets/overrides/override-analytics.png)

添加所需覆盖后，保存数据流设置。

您现在应已配置 Adobe Analytics 数据流覆盖。现在，您可以[通过 Web SDK 将覆盖发送到 Edge Network](#send-overrides)。

### Experience Platform 事件数据集的数据流覆盖 {#event-dataset-overrides}

要为 Experience Platform 事件数据集配置数据流覆盖，您必须首先创建 [Adobe Experience Platform](configure.md#aep) 数据流。按照说明进行操作，使用 [Adobe Experience Platform](configure.md#aep) 服务[配置数据流](configure.md)。

创建数据流后，编辑 [Adobe Experience Platform](configure.md#aep) 已添加的服务并选择 **[!UICONTROL 添加事件数据集]** 用于添加一个或多个覆盖事件数据集的选项，如下图所示。

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

## 通过 Web SDK 将覆盖发送到 Edge Network {#send-overrides-web-sdk}

>[!NOTE]
>
>作为通过 Web SDK 命令发送配置覆盖的替代方法，您可以将配置覆盖添加到 Web SDK [标记扩展](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)。

在数据收集 UI 中[配置数据流覆盖](#configure-overrides)后，您现在可以通过 Web SDK 将覆盖发送到 Edge Network。

如果您使用的是Web SDK，请通过 `edgeConfigOverrides` 命令是激活数据流配置覆盖的第二步，也是最后一步。

数据流配置覆盖通过 `edgeConfigOverrides` Web SDK 命令发送到 Edge Network。此命令创建数据流覆盖，并将其传递给 [!DNL Edge Network] 在下一个命令中。 如果您使用 `configure` 命令，则会为每个请求传递覆盖。

此 `edgeConfigOverrides` 命令创建数据流覆盖，这些覆盖将传递给 [!DNL Edge Network] 在下一个命令中。

当使用 `configure` 命令发送配置覆盖时，它包含在以下 Web SDK 命令中。

* [sendEvent](../edge/fundamentals/tracking-events.md)
* [setConsent](../edge/consent/iab-tcf/overview.md)
* [getIdentity](../edge/identity/overview.md)
* [appendIdentityToUrl](../edge/identity/id-sharing.md#cross-domain-sharing)
* [configure](../edge/fundamentals/configuring-the-sdk.md)

全局指定的选项可由各个命令上的配置选项覆盖。

### 通过Web SDK发送配置覆盖 `sendEvent` 命令 {#send-event}

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
          datasetId: "SampleEventDatasetIdOverride"
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

### 通过Web SDK发送配置覆盖 `configure` 命令 {#send-configure}

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
          datasetId: "SampleProfileDatasetIdOverride"
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

## 通过Mobile SDK将覆盖发送到Edge Network {#send-overrides-mobile-sdk}

之后 [配置数据流覆盖](#configure-overrides) 在数据收集UI中，您现在可以通过Mobile SDK将覆盖发送到Edge Network。

如果您使用的是Mobile SDK，请通过 `sendEvent` API是激活数据流配置覆盖的第二步，也是最后一步。

有关Experience PlatformMobile SDK的更多信息，请参阅 [移动SDK文档](https://developer.adobe.com/client-sdks/edge/edge-network/).

### 通过移动SDK覆盖数据流ID {#id-override-mobile}

以下示例显示了数据流ID覆盖在Mobile SDK集成中可能显示的内容。 选择下面的选项卡以查看 [!DNL iOS] 和 [!DNL Android] 示例。

>[!BEGINTABS]

>[!TAB iOS (Swift)]

此示例显示数据流ID覆盖在Mobile SDK中会是什么样子 [!DNL iOS] 集成。

```swift
// Create Experience event from dictionary
var xdmData: [String: Any] = [
  "eventType": "SampleXDMEvent",
  "sample": "data",
]
let experienceEvent = ExperienceEvent(xdm: xdmData, datastreamIdOverride: "SampleDatastreamId")

Edge.sendEvent(experienceEvent: experienceEvent) { (handles: [EdgeEventHandle]) in
  // Handle the Edge Network response
}
```

>[!TAB Android™ (Kotlin)]

此示例显示数据流ID覆盖在Mobile SDK中会是什么样子 [!DNL Android] 集成。

```kotlin
// Create experience event from Map
val xdmData = mutableMapOf < String, Any > ()
xdmData["eventType"] = "SampleXDMEvent"
xdmData["sample"] = "data"

val experienceEvent = ExperienceEvent.Builder()
    .setXdmSchema(xdmData)
    .setDatastreamIdOverride("SampleDatastreamId")
    .build()

Edge.sendEvent(experienceEvent) {
    // Handle the Edge Network response
}
```

>[!ENDTABS]

### 通过Mobile SDK覆盖数据流配置 {#config-override-mobile}

以下示例显示了数据流配置覆盖在Mobile SDK集成上可能显示的内容。 选择下面的选项卡以查看 [!DNL iOS] 和 [!DNL Android] 示例。

>[!BEGINTABS]

>[!TAB iOS (Swift)]

此示例显示数据流配置覆盖在Mobile SDK中看起来是什么样子 [!DNL iOS] 集成。

```swift
// Create Experience event from dictionary
var xdmData: [String: Any] = [
  "eventType": "SampleXDMEvent",
  "sample": "data",
]

let configOverrides: [String: Any] = [
  "com_adobe_experience_platform": [
    "datasets": [
      "event": [
        "datasetId": "SampleEventDatasetIdOverride"
      ]
    ]
  ],
  "com_adobe_analytics": [
  "reportSuites": [
        "MyFirstOverrideReportSuite",
          "MySecondOverrideReportSuite",
          "MyThirdOverrideReportSuite"
      ]
  ],
  "com_adobe_identity": [
    "idSyncContainerId": "1234567"
  ],
  "com_adobe_target": [
    "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
 ],
]

let experienceEvent = ExperienceEvent(xdm: xdmData, datastreamConfigOverride: configOverrides)

Edge.sendEvent(experienceEvent: experienceEvent) { (handles: [EdgeEventHandle]) in
  // Handle the Edge Network response
}
```

>[!TAB Android (Kotlin)]

此示例显示数据流配置覆盖在Mobile SDK中看起来是什么样子 [!DNL Android] 集成。

```kotlin
// Create experience event from Map
val xdmData = mutableMapOf < String, Any > ()
xdmData["eventType"] = "SampleXDMEvent"
xdmData["sample"] = "data"

val configOverrides = mapOf(
    "com_adobe_experience_platform"
    to mapOf(
        "datasets"
        to mapOf(
            "event"
            to mapOf("datasetId"
                to "SampleEventDatasetIdOverride")
        )
    ),
    "com_adobe_analytics"
    to mapOf(
        "reportSuites"
        to listOf(
            "MyFirstOverrideReportSuite",
            "MySecondOverrideReportSuite",
            "MyThirdOverrideReportSuite"
        )
    ),
    "com_adobe_identity"
    to mapOf(
        "idSyncContainerId"
        to "1234567"
    ),
    "com_adobe_target"
    to mapOf(
        "propertyToken"
        to "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    )
)

val experienceEvent = ExperienceEvent.Builder()
    .setXdmSchema(xdmData)
    .setDatastreamConfigOverride(configOverrides)
    .build()

Edge.sendEvent(experienceEvent) {
    // Handle the Edge Network response
}
```

>[!ENDTABS]

## 负载示例 {#payload-example}

上述示例会生成 [!DNL Edge Network] 有效负载类似于以下有效负载。

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "SampleProfileDatasetIdOverride"
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
  "events": [  ]
}
```
