---
title: 在Analytics中手动映射变量
seo-title: 使用Web SDK在Analytics中手动映射变量
description: 如何使用处理规则将变量手动映射到Analytics
seo-description: 使用带有Web SDK的处理规则将变量手动映射到Analytics
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 11%

---


# 在Analytics中手动映射变量

Adobe Experience Platform(AEP)可以自 [!DNL Web SDK] 动映射某些变量，但必须手动映射自定义变量。

对于未自动映射到的XDM数 [!DNL Analytics]据，可以使 [用上下文](https://docs.adobe.com/content/help/zh-Hans/analytics/implementation/vars/page-vars/contextdata.html) 数据来匹 [配模式](https://docs.adobe.com/content/help/zh-Hans/experience-platform/xdm/schema/composition.html)。 然后，可以使用处理规 [!DNL Analytics] 则将 [其映射到](https://docs.adobe.com/content/help/zh-Hans/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) ，以填充 [!DNL Analytics] 变量。

此外，您还可以使用一组默认的操作和产品列表通过AEP发送或检索数据 [!DNL Web SDK]。 为此，请参阅产 [品](https://docs.adobe.com/content/help/en/experience-platform/edge/implement/commerce.html)。

## 上下文数据

要使用， [!DNL Analytics]XDM数据使用点记号进行拼合并提供 `contextData`。 以下值对的列表显示了以下示例 `context data`:

```javascript
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

边缘网络收集的所有数据都可以通过处理 [规则访问](https://docs.adobe.com/content/help/zh-Hans/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html)。 在中 [!DNL Analytics]，您可以使用处理规则将上下文数据合并到变 [!DNL Analytics] 量中。

例如，在以下规则中，Analytics设置为用与 **a.x_atag.search.term(Context Data** )关联的数 **据填充内部搜索词(eVar2)**。

![](assets/examplerule.png)


## XDM模式

[!DNL Experience Platform] 使用模式以一致、可重用的方式描述数据结构。 通过跨系统一致地定义数据，更容易保留含义，从而从数据中获得价值。 [!DNL Analytics] 上下文数据与模式定义的结构配合使用。

以下示例说明如何 [`event` 与](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html) AEP中 `xdm` 的选项一起使用命令来发送和检索数据 [!DNL Web SDK]。 在此示例中，该命 `event` 令与ExperienceEvent Commerce [Details模式匹配](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) ，以便跟踪productListItems `name` 和 `SKU` 值：


```
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

有关使用AEP跟踪事件的更多信 [!DNL Web SDK]息，请参 [阅跟踪事件](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html)。
