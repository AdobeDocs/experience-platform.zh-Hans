---
title: 配置数据流覆盖
description: 了解如何在数据流UI中配置数据流覆盖并通过Web SDK或Mobile SDK激活它们。
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 53%

---

# 配置数据流覆盖

数据流覆盖允许您为数据流定义其他配置，这些配置通过Web SDK或Mobile SDK传递到Edge Network。

这有助于触发与默认数据流行为不同的数据流行为，而无需创建数据流或修改现有设置。

数据流配置覆盖分为两步：

1. 首先，必须在[数据流配置页面](configure.md)中定义数据流配置覆盖。
2. 然后，您必须通过以下方式之一将覆盖发送到Edge Network：
   * 通过`sendEvent`或`configure` [Web SDK](#send-overrides)命令。
   * 通过Web SDK [标记扩展](../tags/extensions/client/web-sdk/configure/configuration-overrides.md)。
   * 通过Mobile SDK [sendEvent](#send-overrides) API或使用[Rules](#send-overrides)。

本文介绍每种受支持的覆盖的端到端数据流配置覆盖过程。

>[!IMPORTANT]
>
>[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/)集成当前不支持数据流覆盖。
><br>
>在需要将不同的数据发送到不同的数据流时应使用数据流覆盖。请勿对个性化用例或同意数据使用数据流覆盖。

## 用例 {#use-cases}

为了帮助您更好地了解如何以及何时使用数据流覆盖，以下是 Adobe Experience Platform 客户可使用此功能解决的一些用例。

**多区域数据收集**

一家公司对于其开展经营的不同国家/地区拥有不同的网站或子域。其中[配置了](configure.md)单独的数据流，这些数据流具有相应的 Analytics 特有的报表包、国家/地区特有的 Adobe Target 属性令牌、国家/地区特有的架构、数据集、Journey Optimizer 配置等等。该公司还有一套全球配置，其中汇集所有国家/地区特有的数据。

通过使用数据流覆盖，该公司可动态地将数据的流动切换到不同的数据流，取代将数据发送到一个数据流的默认行为。

一个常见的使用案例可能是将数据发送到特定于国家/地区的数据流，也发送到客户在其中执行重要操作（如下订单或更新其用户配置文件）的全球数据流。

**为不同的业务部门区分轮廓和身份标识**

具有多个业务部门的公司希望使用多个Experience Platforms沙盒存储特定于每个业务部门的数据。

该公司可使用数据流覆盖确保每个业务部门都有自己的数据流以通过它接收数据，而非将数据发送到默认数据流。

## 在数据流 UI 中配置数据流覆盖 {#configure-overrides}

数据流配置覆盖允许您修改以下数据流配置：

* Experience Platform 事件数据集
* Adobe Target 属性令牌
* Audience Manager ID 同步容器
* Adobe Analytics 报告包

### Adobe Target 的数据流覆盖 {#target-overrides}

要为 Adobe Target 数据流配置数据流覆盖，您必须首先创建 Adobe Target 数据流。按照说明进行操作，使用 [Adobe Target](configure.md#target) 服务[配置数据流](configure.md)。

创建数据流后，编辑已添加的[Adobe Target](configure.md#target)服务，并使用&#x200B;**[!UICONTROL Property Token Overrides]**&#x200B;部分添加所需的数据流覆盖，如下图所示。 每行添加一个属性令牌。

![数据流 UI 屏幕快照，显示了 Adobe Target 服务设置，并突出显示了属性令牌覆盖。](assets/overrides/override-target.png)

添加所需覆盖后，保存数据流设置。

您现在应已配置 Adobe Target 数据流覆盖。现在，您可以[通过Web SDK或Mobile SDK](#send-overrides)将覆盖发送到Edge Network。

### Adobe Analytics 的数据流覆盖 {#analytics-overrides}

要为 Adobe Analytics 数据流配置数据流覆盖，您必须首先创建 [Adobe Analytics](configure.md#analytics) 数据流。按照说明进行操作，使用 [Adobe Analytics](configure.md#analytics) 服务[配置数据流](configure.md)。

创建数据流后，编辑已添加的[Adobe Analytics](configure.md#target)服务，并使用&#x200B;**[!UICONTROL Report Suite Overrides]**&#x200B;部分添加所需的数据流覆盖，如下图所示。

选择&#x200B;**[!UICONTROL Show Batch Mode]**&#x200B;以启用对报表包覆盖的批量编辑。 您可以复制并粘贴报告包覆盖列表，每行输入一个报告包。

![数据流 UI 屏幕快照，显示了 Adobe Analytics 服务设置，并突出显示了报告包覆盖。](assets/overrides/override-analytics.png)

添加所需覆盖后，保存数据流设置。

您现在应已配置 Adobe Analytics 数据流覆盖。现在，您可以[通过Web SDK或Mobile SDK](#send-overrides)将覆盖发送到Edge Network。

### Experience Platform 事件数据集的数据流覆盖 {#event-dataset-overrides}

要为 Experience Platform 事件数据集配置数据流覆盖，您必须首先创建 [Adobe Experience Platform](configure.md#aep) 数据流。按照说明进行操作，使用 [Adobe Experience Platform](configure.md#aep) 服务[配置数据流](configure.md)。

创建数据流后，编辑已添加的[Adobe Experience Platform](configure.md#aep)服务，并选择&#x200B;**[!UICONTROL Add Event Dataset]**&#x200B;选项以添加一个或多个覆盖事件数据集，如下图所示。

![数据流 UI 屏幕快照，显示了 Adobe Experience Platform 服务设置，并突出显示了事件数据集覆盖。](assets/overrides/override-aep.png)

添加所需覆盖后，保存数据流设置。

您现在应已配置 Adobe Experience Platform 数据流覆盖。现在，您可以[通过Web SDK或Mobile SDK](#send-overrides)将覆盖发送到Edge Network。

### 第三方 ID 同步容器的数据流覆盖 {#container-overrides}

要为第三方 ID 同步容器配置数据流覆盖，您必须首先创建数据流。按照说明进行操作，[配置数据流](configure.md)以创建一个数据流。

创建数据流后，转到&#x200B;**[!UICONTROL Advanced Options]**&#x200B;并启用&#x200B;**[!UICONTROL Third Party ID Sync]**&#x200B;选项。

然后，使用&#x200B;**[!UICONTROL Container ID Overrides]**&#x200B;部分添加要覆盖默认设置的容器ID，如下图所示。

>[!IMPORTANT]
>
>容器 ID 必须是数值，例如 `1234567`，而不是字符串，例如 `"1234567"`。如果您通过 Web SDK 发送字符串值作为容器 ID 覆盖，您将收到错误。

![数据流 UI 屏幕快照，显示了数据流设置，并突出显示了第三方 ID 同步容器覆盖。](assets/overrides/override-container.png)

添加所需覆盖后，保存数据流设置。

您现在应已配置 ID 同步容器覆盖。现在，您可以[通过Web SDK或Mobile SDK](#send-overrides)将覆盖发送到Edge Network。

## 将覆盖发送到Edge Network {#send-overrides}

在数据收集UI中配置数据流覆盖后，您可以通过Web SDK或Mobile SDK将覆盖发送到Edge Network。

* **Web SDK**：有关JavaScript库代码示例，请参阅[数据流配置覆盖](/help/collection/js/commands/configure/edgeconfigoverrides.md)。
* **移动SDK**：您可以使用[sendEvent API](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-sendevent/)或使用[Rules](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-rules/)发送数据流ID覆盖。

## 负载示例 {#payload-example}

以上示例生成与以下示例类似的[!DNL Edge Network]有效负载。

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
