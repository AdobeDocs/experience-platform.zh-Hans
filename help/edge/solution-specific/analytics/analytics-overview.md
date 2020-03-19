---
title: 向Adobe Analytics发送数据
seo-title: 使用Adobe Experience Platform Web SDK将数据发送到Adobe Analytics
description: 了解如何使用Experience Platform Web SDK将数据发送到Adobe Analytics
seo-description: 了解如何使用Experience Platform Web SDK将数据发送到Adobe Analytics
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# （测试版）将数据发送到Adobe Analytics

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生更改。

Adobe Experience Platform Web SDK可以将数据发送到Adobe Analytics。 这可以通过将 `xdm` 其转换为Adobe Analytics可使用的格式来实现。

## 设置

如果您在客户配置UI中映射了报表包，Adobe Analytics会自动获取您发送的数据。 您可以在此将一个或多个报告映射到给定配置。 映射报表包后，数据将自动开始流动。

## 自动映射的数据

Adobe Experience Platform Edge Network可自动映射许多XDM变量。 此处列出了自动映射变量的完整 [列表](../analytics/automatically-mapped-vars.md)。

## 手动映射的数据

边缘网络采集的所有数据都可以通过处理规则访问。 数据使用点记号进行拼合，并作为contextData可用。

如果您有一个类似的架构。

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

![处理规则界面](../../../assets/edge_analytics_processing_rules.png)
