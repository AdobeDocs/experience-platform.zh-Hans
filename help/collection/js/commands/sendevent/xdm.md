---
title: xdm
description: 了解如何通过XDM架构对齐的对象将数据发送到Adobe。
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# `xdm`

`xdm`对象包含发送到Adobe的数据有效负载。 在此对象中设置的字段直接映射到数据集架构中定义的元素。

Adobe Experience Platform使用架构，以一致且可重用的方式描述数据结构。 通过在各个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。

运行`xdm`命令时设置`sendEvent`对象。 确保此对象中的层级与配置的数据集的架构匹配。 您可以在同一`xdm`命令中同时包含[`data`](data.md)对象和`sendEvent`对象。

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

## 通过Web SDK标记扩展使用`xdm`对象

使用Web SDK标记扩展时，`xdm`对象可用作[变量数据元素](/help/tags/extensions/client/web-sdk/data-element-types.md#variable)或[XDM对象数据元素](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)。 Adobe建议在大多数情况下使用变量数据元素。
