---
title: 使用Web SDK将数据发送到Adobe Analytics
description: 了解如何使用Adobe Experience Platform Web SDK将数据发送到Adobe Analytics。
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# 使用Web SDK将数据发送到Adobe Analytics

Experience PlatformWeb SDK可以通过Experience PlatformEdge Network向Adobe Analytics发送数据。 Adobe提供了多个选项，可用于使用Web SDK将数据发送到Adobe Analytics：

* 将[**[!UICONTROL Adobe Analytics ExperienceEvent字段组]**](../../xdm/field-groups/event/analytics-full-extension.md)添加到您的架构中，然后使用[`XDM`对象](../commands/sendevent/xdm.md)。
* 使用[`data`对象](../commands/sendevent/data.md)将数据发送到不带XDM架构的Adobe Analytics。
* 使用自动生成的[上下文数据变量](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/contextdata)和[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about)。

## 使用`XDM`对象 {#use-xdm-object}

如果要使用特定于Adobe Analytics的预定义架构，可将[Adobe Analytics ExperienceEvent架构字段组](../../xdm/field-groups/event/analytics-full-extension.md)添加到您的架构中。 添加后，您可以使用Web SDK中的`xdm`对象填充此架构，以将数据发送到报表包。 数据到达Edge Network时，会将XDM对象转换为Adobe Analytics可以理解的格式。

可以通过Web SDK以两种方式将数据发送到Adobe Analytics：

* [使用Web SDK标记扩展将数据发送到Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-tag-extension)
* [使用Web SDK JavaScript库将数据发送到Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-javascript-library)

请参阅Adobe Analytics实施指南中的[XDM对象变量映射到Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/xdm-var-mapping)，以获取有关XDM字段及其如何映射到Analytics变量的完整参考。

## 使用`data`对象 {#use-data-object}

作为使用XDM对象的替代方法，您可以改用数据对象。 数据对象适用于当前使用AppMeasurement的实施，从而更加轻松地升级到Web SDK。

根据您使用的是AppMeasurement还是Analytics标记扩展，请参阅以下指南以了解有关如何迁移到Web SDK的详细信息：

* [从Adobe Analytics标记扩展迁移到Web SDK标记扩展](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/analytics-extension-to-web-sdk)
* [从AppMeasurement迁移到Web SDK](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk)

有关数据对象字段及其映射到Analytics变量的完整参考，请参阅Adobe Analytics实施指南中有关将数据对象变量映射到Adobe Analytics[&#128279;](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping)的文档。

## 使用上下文数据变量 {#use-context-data-variables}

任何未自动映射的变量均可用作[上下文数据变量](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/contextdata)。 然后，您可以使用[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about)将上下文数据变量映射到Analytics变量。 例如，如果您有一个类似于以下内容的自定义XDM架构：

```json
{
  "xdm": {
    "key":"value",
    "animal": {
      "species": "Raven",
      "size": "13 inches"
    },
    "array": [
      "v0",
      "v1",
      "v2"
    ],
    "objectArray":[{
      "ad1": "300x200",
      "ad2": "60x240",
      "ad3": "600x50"
    }]
  }
}
```

然后，这些字段将成为您在处理规则界面中可用的上下文数据键：

```javascript
a.x.key //value
a.x.animal.species //Raven
a.x.animal.size //13 inches
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.objectarray.0.ad1 //300x200
a.x.objectarray.1.ad2 //60x240
a.x.objectarray.2.ad3 //600x50
```

## 常见问题解答

+++如何在Web SDK中区分页面查看调用和链接跟踪调用？

Adobe Analytics中的AppMeasurement使用单独的页面查看方法调用（[`t()`方法](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/t-method)）和链接跟踪调用（[`tl()`方法](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/tl-method)）。 Web SDK而是仅提供用于发送页面查看和链接跟踪的[`sendEvent`](../commands/sendevent/overview.md)命令。 包含在事件中的数据将确定它是Adobe Analytics中的[页面查看](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/page-views)还是[页面事件](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/page-events)。

默认情况下，所有事件都将被视为Adobe Analytics中的页面查看次数。 如果要将Web SDK事件设置为Adobe Analytics链接跟踪调用，请设置以下字段：

* **XDM对象**： `xdm.web.webInteraction.name`、`web.webInteraction.type`和`web.webInteraction.URL`
* **数据对象**： `data.__adobe.analytics.linkName`、`data.__adobe.analytics.linkType`和`data.__adobe.analytics.linkURL`
* **上下文数据**：不支持

有关详细信息，请参阅Adobe Analytics实施指南中的[`tl()`方法](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/tl-method)。

如果在`configure`命令中启用[`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md)，则会为您填充这些字段。

+++

+++数据流如何将数据与其他服务区分开来，以及面向Adobe Analytics的数据？

发送到数据流的所有事件都会传递到所有配置的服务。 例如，如果您分别调用个性化和Analytics，则这两个事件都会发送到Analytics和Target。 这些事件记录在Analytics报表中，可能会影响跳出率等量度。

如果您使用Web SDK，则这些调用通常合并到[`sendEvent`](../commands/sendevent/overview.md)命令中。

+++
