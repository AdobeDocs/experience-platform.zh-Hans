---
title: xdm
description: 了解如何通过XDM模式对齐对象向Adobe发送数据。
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# `xdm`

`xdm`对象包含发送到Adobe的数据有效负载。 在此对象中设置的字段直接映射到数据集架构中定义的元素。

Adobe Experience Platform使用架构，以一致且可重用的方式描述数据结构。 通过在各个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。

此对象的最大限制为32 KB。

## 使用Web SDK扩展配置XDM对象

在标记规则的操作中设置&#x200B;**[!UICONTROL XDM]**&#x200B;对象。 [XDM对象](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)提供了一个直观的界面以将其他数据元素映射到它们各自的XDM字段。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 规则]**，然后选择所需的规则。
1. 在[!UICONTROL 操作]下，选择现有操作或创建操作。
1. 将[!UICONTROL 扩展]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，并将[!UICONTROL 操作类型]设置为&#x200B;**[!UICONTROL 发送事件]**。
1. 在&#x200B;**[!UICONTROL XDM]**&#x200B;字段中提供包含所需对象的数据元素。
1. 单击&#x200B;**[!UICONTROL 保留更改]**，然后运行发布工作流程。

## 使用Web SDK JavaScript库配置XDM对象

运行`sendEvent`命令时设置`xdm`对象。 确保此对象中的层级与配置的数据集的架构匹配。 您可以在同一`sendEvent`命令中同时包含`xdm`对象和[`data`](data.md)对象。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

以下示例使用[Commerce详细信息架构字段组](/help/xdm/field-groups/event/commerce-details.md)：

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large field hat",
      },
      {
        "SKU":"HT104",
        "name":"Small field hat",
      }
    ]
  }
});
```
