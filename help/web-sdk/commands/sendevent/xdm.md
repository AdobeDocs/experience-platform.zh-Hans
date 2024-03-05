---
title: xdm
description: 发送到Adobe的架构对齐对象。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# `xdm`

此 `xdm` 对象包含发送到Adobe的数据有效负载。 在此对象中设置的字段直接映射到数据集架构中定义的元素。

Adobe Experience Platform使用架构，以一致且可重用的方式描述数据结构。 通过在各个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。

此字段的最大限制为32 KB。

## 使用Web SDK扩展配置XDM对象

设置 **[!UICONTROL XDM]** 标记规则操作中的字段。 此 [XDM对象](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) 提供了一个直观的界面以将其他数据元素映射到它们各自的XDM字段。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 规则]**，然后选择所需的规则。
1. 下 [!UICONTROL 操作]，选择现有操作或创建操作。
1. 设置 [!UICONTROL 扩展名] 下拉字段至 **[!UICONTROL Adobe Experience Platform Web SDK]**，并设置 [!UICONTROL 操作类型] 到 **[!UICONTROL 发送事件]**.
1. 提供包含中所需对象的数据元素 **[!UICONTROL XDM]** 字段。
1. 单击 **[!UICONTROL 保留更改]**，然后运行发布工作流程。

## 使用Web SDK JavaScript库配置XDM对象

设置 `xdm` 对象 `sendEvent` 命令。 确保此对象中的层级与配置的数据集的架构匹配。 您可以同时包含 `xdm` 对象和 [`data`](data.md) 同一对象中的 `sendEvent` 命令。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

以下示例使用 [商务详细信息架构字段组](/help/xdm/field-groups/event/commerce-details.md)：

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
