---
title: 在Adobe Analytics手动映射变量
seo-title: 使用Web SDK在Adobe Analytics手动映射变量
description: 如何用处理规则将变量手动映射到Adobe Analytics
seo-description: 使用带有Web SDK的处理规则将变量手动映射到Adobe Analytics
keywords: adobe analytics;analytics;variables;mapping variables;map variables;contextData;context Data;Processing rules;rules;xdm;schema;
translation-type: tm+mt
source-git-commit: 1b5ee9b1f9bdc7835fa8de59020b3eebb4f59505
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 35%

---


# 在Adobe Analytics手动映射变量

Adobe Experience Platform [!DNL Web SDK] 可以自动映射某些变量，但必须手动映射自定义变量。

For XDM data that is not automatically mapped to [!DNL Analytics], you can use [context data](https://docs.adobe.com/content/help/zh-Hans/analytics/implementation/vars/page-vars/contextdata.html) to match your [schema](https://docs.adobe.com/content/help/zh-Hans/experience-platform/xdm/schema/composition.html). 然后，可以使用处理规 [!DNL Analytics] 则将 [其映射到](https://docs.adobe.com/content/help/zh-Hans/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) ，以填充 [!DNL Analytics] 变量。

此外，您可以使用默认的操作集和产品列表来使用Adobe Experience PlatformWeb SDK发送或检索数据。 为此，请参阅[产品](https://docs.adobe.com/content/help/zh-Hans/experience-platform/edge/implement/commerce.html)。

## 上下文数据

To be used by [!DNL Analytics], XDM data is flattened using dot notation and made available as `contextData`. 以下值对列表显示了 `context data` 示例：

```json
{
  "bh": "900",
  "bw": "1680",
  "c": "24",
  "c.a.d.key.[0]": "value1",
  "c.a.d.key.[1]": "value2",
  "c.a.d.object.key1": "value1",
  "c.a.d.object.key2.[0]": "value2",
  "c.a.x.environment.browserdetails.javascriptenabled": "true",
  "c.a.x.environment.type": "browser",
  "cust_hit_time_gmt": "1579781427",
  "g": "http://example.com/home",
  "gn": "home",
  "j": "1.8.5",
  "k": "Y",
  "s": "1680x1050",
  "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:0|1,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
  "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
  "v": "Y"
}
```

## 处理规则

可以通过[处理规则](https://docs.adobe.com/content/help/zh-Hans/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html)访问边缘网络收集的所有数据。In [!DNL Analytics], you can use processing rules to incorporate context data into [!DNL Analytics] variables.

For example, in the following rule, Adobe Analytics is set to populate **Internal Search terms (eVar2)** with the data associated with **a.x_atag.search.term(Context Data)**.

![](assets/examplerule.png)


## XDM模式

Adobe Experience Platform使用模式以一致、可重用的方式描述数据结构。 通过跨系统一致地定义数据，更容易保留含义，从而从数据中获得价值。 [!DNL Analytics] 上下文数据与模式定义的结构配合使用。

The following example shows how the [`event` command](https://docs.adobe.com/content/help/zh-Hans/experience-platform/edge/fundamentals/tracking-events.html) can be used with the `xdm` option to send and retrieve data with Adobe Experience Platform Web SDK. 在此示例中，`event` 命令与 [ExperienceEvent 商务详细信息架构](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md)匹配，因此可以跟踪 productListItems `name` 和 `SKU` 值：


```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large Field Hat",
      },
      {
        "SKU":"HT104",
        "name":"Small Field Hat",
      }
    ]
  }
});
```

有关使用Adobe Experience Platform跟踪事件的更多信 [!DNL Web SDK]息，请参 [阅跟踪事件](https://docs.adobe.com/content/help/zh-Hans/experience-platform/edge/fundamentals/tracking-events.html)。
