---
title: 在Platform Web SDK中使用Adobe Analytics
description: 了解如何使用Adobe Experience Platform Web SDK将数据发送到Adobe Analytics。
keywords: adobe analytics；analytics；映射的数据；映射的变量；
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 836fa7814a6966903639e871bfaea0563847f363
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 在Platform Web SDK中使用Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] 可以向Adobe Analytics发送数据。 这可以通过翻译实现 `xdm` 转换为Adobe Analytics可以使用的格式。

## 设置

如果您在客户配置UI中映射了报表包，则Adobe Analytics会自动选取您发送的数据。 在这里，您可以将一个或多个报表映射到给定的配置。 在映射报表包后，数据将自动开始流动。

## XDM字段组

为了更便于捕获最常见的Adobe Analytics量度，我们提供了一个您可以使用的Analytics字段组。 有关此架构的更多详细信息，请参阅 [Adobe Analytics ExperienceEvent完整扩展架构字段组](../../../xdm/field-groups/event/analytics-full-extension.md)

## 自动映射的数据

Adobe Experience Platform [!DNL Edge Network] 自动映射许多XDM变量。 将列出这些变量的完整列表 [此处](automatically-mapped-vars.md).

## 手动映射的数据

任何未由自动映射的数据 [!DNL Edge Network] 可以通过处理规则访问。 数据使用点表示法扁平化，并可用作contextData。

如果你有一个类似这样的结构描述。

```javascript
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

然后，这些将是可供您使用的上下文数据键。

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

以下是将使用此数据的处理规则的示例。

![处理规则界面](./assets/edge_analytics_processing_rules.png)

>[!NOTE]
>
>通过Experience Edge收集，所有事件都会发送到Analytics，以及您为数据流配置的任何其他服务。 例如，如果您将Analytics和Target配置为服务，并且分别发起个性化调用和Analytics调用，则这两个事件都将发送到Analytics和Target。 这些事件将记录在Analytics报表中，并且可能会影响跳出率等量度。
