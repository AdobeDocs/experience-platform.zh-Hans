---
title: 使用Web SDK将数据发送到Adobe Analytics
description: 了解如何使用Adobe Experience Platform Web SDK将数据发送到Adobe Analytics。
keywords: adobe analytics；analytics；映射的数据；映射的变量；
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 3%

---

# 使用Web SDK将数据发送到Adobe Analytics

Adobe Experience Platform Web SDK可以通过Adobe Experience Platform Edge Network向Adobe Analytics发送数据。 当数据到达Edge Network时，它会将XDM对象转换为Adobe Analytics可以理解的格式。

## XDM字段组

为了更便于捕获最常见的Adobe Analytics量度，Adobe提供了一个针对Adobe Analytics的字段组，您可以使用该字段组。 有关此架构的更多详细信息，请参阅 [Adobe Analytics ExperienceEvent完整扩展架构字段组](/help/xdm/field-groups/event/analytics-full-extension.md).

## 变量映射

Edge Network会自动映射许多XDM变量。 请参阅 [Edge Network中的Analytics变量映射](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=zh-Hans) Adobe Analytics ，以获取自动映射变量的完整变量列表。

任何未自动映射的变量均可用作 [上下文数据变量](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=zh-Hans). 然后，您可以使用 [处理规则](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about.html) 将上下文数据变量映射到Analytics变量。 例如，如果您有一个类似于以下内容的自定义XDM架构：

```js
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    "v0",
    "v1",
    "v2"
  ],
  arrayofobjects:[
    {
      obj1key:objval0
    },
    {
      obj2key:objval1
    }
  ]
}
```

下面是“处理规则”界面中可用的上下文数据键：

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.arrayofobjects.0.obj1key //objval0
a.x.arrayofobjects.1.obj2key //objval1
```

>[!NOTE]
>
>通过Edge Network收集，所有事件都会发送到Analytics以及您为数据流配置的任何其他服务。 例如，如果将Analytics和Target配置为服务，并且分别发起个性化调用和Analytics调用，则这两个事件都会发送到Analytics和Target。 这些事件记录在Analytics报表中，可能会影响跳出率等量度。

## 页面查看次数和链接跟踪调用

Adobe Analytics中的AppMeasurement使用单独的页面查看方法调用([`t()` 方法](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/t-method.html))和链接跟踪调用([`tl()` 方法](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/tl-method.html))。 而Web SDK仅提供 [`sendEvent`](../commands/sendevent/overview.md) 用于发送页面查看和链接跟踪的命令。 您在事件中包含的数据确定它是否为 [页面查看](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-views.html) 或 [页面事件](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-events.html) 在Adobe Analytics中。

默认情况下，所有事件都将被视为Adobe Analytics中的页面查看次数。 如果要将Web SDK事件设置为Adobe Analytics链接跟踪调用，请设置以下XDM字段：

* **`web.webInteraction.URL`**：链接URL。
* **`web.webInteraction.name`**：自定义链接、下载链接或退出链接维度名称，具体取决于中的值 `web.webInteraction.type`
* **`web.webInteraction.type`**：确定点击的链接类型。 有效值包括 `other`（自定义链接）、`download`（下载链接）和 `exit`（退出链接）。

如果您启用 [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) 在 `configure` 命令，将为您填充这些XDM字段。
