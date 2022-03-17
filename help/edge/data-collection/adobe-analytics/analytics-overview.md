---
title: 将Adobe Analytics与Platform Web SDK结合使用
description: 了解如何使用Adobe Experience Platform Web SDK将数据发送到Adobe Analytics。
keywords: adobe analytics;analytics；映射的数据；映射的变量；
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 921a3a32ee5f2daa04512a3f2c68935667ab3875
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 6%

---

# 将Adobe Analytics与Platform Web SDK结合使用

Adobe Experience Platform [!DNL Web SDK] 可以将数据发送到Adobe Analytics。 这是通过翻译 `xdm` 格式，以便Adobe Analytics使用。

## 设置

如果您在客户配置UI中映射了报表包，Adobe Analytics会自动选取您发送的数据。 在此，您可以将一个或多个报表映射到给定配置。 报表包映射后，数据将自动开始流动。

## XDM字段组

为了更便于捕获最常见的Adobe Analytics量度，我们提供了一个Analytics字段组，供您使用。 有关此架构的更多详细信息，请参阅 [Adobe Analytics ExperienceEvent完整扩展架构字段组](../../../xdm/field-groups/event/analytics-full-extension.md)

## 自动映射的数据

Adobe Experience Platform [!DNL Edge Network] 自动映射多个XDM变量。 下面列出了这些变量的完整列表 [此处](automatically-mapped-vars.md).

## 手动映射的数据

可以通过处理规则访问边缘网络收集的所有数据。数据使用点表示法进行扁平化，可用作contextData。

如果你有这样的模式。

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

以下是使用此数据的处理规则示例。

![处理规则界面](./assets/edge_analytics_processing_rules.png)
