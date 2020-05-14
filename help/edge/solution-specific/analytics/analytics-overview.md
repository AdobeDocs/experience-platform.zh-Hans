---
title: 将数据发送到Adobe Analytics
seo-title: 使用Adobe Experience Platform Web SDK将数据发送到Adobe Analytics
description: 了解如何使用Experience Platform Web SDK将数据发送到Adobe Analytics
seo-description: 了解如何使用Experience Platform Web SDK将数据发送到Adobe Analytics
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 将数据发送到Adobe Analytics

Adobe Experience Platform Web SDK可以将数据发送到Adobe Analytics。 这可以通过将 `xdm` Adobe Analytics可以使用的格式进行转换。

## 设置

如果您在客户配置UI中映射了报表包，Adobe Analytics会自动选取您要发送的数据。 您可以在此将一个或多个报告映射到给定配置。 映射报表包后，数据将自动开始流动。

## 自动映射的数据

Adobe Experience Platform Edge Network自动映射许多XDM变量。 此处列出自动映射变量的完整 [列表](../analytics/automatically-mapped-vars.md)。

## 手动映射的数据

边缘网络收集的所有数据都可以通过处理规则进行访问。 数据使用点记号进行拼合，并可作为contextData使用。

如果你的模式长成这样。

```javascript
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    v1,
    v2,
    v3
  ],
  arrayofobjects:[
    {
      obj1key:objval1
    },
    {
      obj2key:objval2
    }
  ]
}
```

然后这些将是可供您使用的上下文数据键。

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array[0] //v1
a.x.array[1] //v2
a.x.array[3] //v3
a.x.arrayofobjects[1].obj1key //objval1
a.x.arrayofobjects[2].obj2key //objval2
```

以下是将使用此数据的处理规则的示例。

![处理规则接口](../../../assets/edge_analytics_processing_rules.png)
