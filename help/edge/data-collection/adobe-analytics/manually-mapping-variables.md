---
title: 在Adobe Experience Platform Web SDK中手动映射Adobe Analytics变量
description: 了解如何使用Experience PlatformWeb SDK中的处理规则手动将变量映射到Adobe Analytics。
seo-description: Manually map variables into Adobe Analytics using processing rules with Web SDK
keywords: adobe analytics；analytics；变量；映射变量；映射变量；contextData；上下文数据；处理规则；规则；xdm；架构；
exl-id: 395050c1-8d39-4da8-acea-6e618ed662dd
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 12%

---

# Adobe Analytics中的手动映射变量

Adobe Experience Platform [!DNL Web SDK] 可以自动映射某些变量，但自定义变量必须手动映射。

对于未自动映射到的XDM数据 [!DNL Analytics]，您可以使用 [上下文数据](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=zh-Hans) 以匹配您的 [架构](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hans). 然后可以将其映射到 [!DNL Analytics] 使用 [处理规则](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=zh-Hans) 以填充 [!DNL Analytics] 变量。

此外，您可以使用默认操作集和产品列表，通过Adobe Experience Platform Web SDK发送或检索数据。 要执行此操作，请参阅 [收集商业和产品信息](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html).

## 上下文数据

使用方 [!DNL Analytics]， XDM数据使用点表示法扁平化，并可用作 `contextData`. 以下值对列表显示了 `context data` 当它变平时：

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

可以通过[处理规则](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html?lang=zh-Hans)访问边缘网络收集的所有数据。在 [!DNL Analytics]，则可以使用处理规则将上下文数据合并到 [!DNL Analytics] 变量。

例如，在以下规则中，Adobe Analytics设置为填充 **内部搜索词(eVar2)** 与关联的数据 **a.x._atag.search.term（上下文数据）**.

![Analytics UI图像显示了规则示例。](assets/examplerule.png)

## XDM架构

Adobe Experience Platform使用架构，以一致且可重用的方式描述数据结构。 通过在各个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。 [!DNL Analytics] 上下文数据可与架构定义的结构配合使用。

以下示例显示了 [`event` 命令](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=zh-Hans) 可以与 `xdm` 用于使用Adobe Experience Platform Web SDK发送和检索数据的选项。 在此示例中，`event` 命令与 [ExperienceEvent 商务详细信息架构](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md)匹配，因此可以跟踪 productListItems `name` 和 `SKU` 值：


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

有关使用Adobe Experience Platform跟踪事件的更多信息 [!DNL Web SDK]，请参见 [跟踪事件](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=zh-Hans).
