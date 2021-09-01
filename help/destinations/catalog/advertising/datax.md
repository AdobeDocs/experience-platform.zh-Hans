---
title: Verizon MediaYahoo DataX集成
description: DataX是Verizon Media/Yahoo的聚合基础架构，它托管各种组件，使Verizon Media/Yahoo能够以安全、自动和可扩展的方式与其外部合作伙伴交换数据。
source-git-commit: 07c8a7afaf6cd2af249ad52eabfbc5f8cd6689ae
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 2%

---


# Verizon Media/Yahoo DataX

## 概述 {#overview}

DataX是Verizon Media/Yahoo的聚合基础架构，它托管各种组件，使Verizon Media/Yahoo能够以安全、自动和可扩展的方式与其外部合作伙伴交换数据。

>[!IMPORTANT]
>
>此文档页面由Verizon Media/Yahoo的DataX团队创建。 如有任何查询或更新请求，请直接通过[dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)联系他们

## 先决条件 {#prerequisites}

**MDM ID**

这是Yahoo DataX中的唯一标识符，它是设置导出到此目标的数据的必填字段。 如果您不知道此ID，请联系您的Yahoo Data X客户经理。

**速率限制**

根据[DataX文档](https://developer.verizonmedia.com/datax/guide/rate-limits/)中概述的分类和受众帖子的配额限制，DataX具有限制的速率。


| 错误代码 | 错误消息 | 描述 |
|---------|----------|---------|
| 429请求过多 | 每小时超出速率限制&#x200B;**(限制：100)** | 每个提供商一小时内允许的请求数。 |

{style=&quot;table-layout:auto&quot;}

**分类元数据**

分类资源通过基本DataX元数据结构定义扩展

```
{

  >>(Base DataX Metadata)<<

        "extensions" : { "action" :
        {string}, "incrementalData" :
        {
                "taxonomyId": {string}
                },
                "links" : [{
                "rel"   : "https://datax.yahooapis.com/rels/fullTaxonomy", "title" : "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

有关[分类元数据](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/)的更多信息，请参阅DataX开发人员文档。

## 支持的身份 {#supported-identities}

Verizon Media支持激活下表所述的身份。 了解有关[identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)的更多信息。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]在激活时自动对数据进行哈希处理。 |
| GAID | Google广告ID | 如果源标识是GAID命名空间，请选择GAID目标标识。 |
| IDFA | 适用于广告商的Apple ID | 如果源标识是IDFA命名空间，请选择IDFA目标标识。 |

{style=&quot;table-layout:auto&quot;}

## 导出类型 {#export-type}

**区段导出**  — 您正在导出区段（受众）的所有成员，以及Verizon Media目标中使用的标识符（电子邮件）。

## 用例 {#use-cases}

DataX API适用于那些想要定位特定受众组的广告商，这些受众组在Verizon Media(VMG)中以电子邮件地址作为关键字，这样，他们就可以快速创建新区段，并使用VMG的近实时API推送所需的受众组。

## 连接到目标 {#connect}

![Platform UI中的Yahoo DataX目标卡](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL MDM ID]**:这是Yahoo DataX中的唯一标识符，它是设置导出到此目标的数据的必填字段。如果您不知道此ID，请联系您的Yahoo Data X客户经理。  使用MDM ID，可以限制数据仅用于特定专用用户集（例如广告商的第一方数据）。

## 将区段激活到此目标 {#activate}

请阅读[将配置文件和区段激活到目标](../../ui/activate-segment-streaming-destinations.md) ，以了解有关将受众区段激活到目标的说明。

## 数据使用和管理 {#data-usage-governance}

处理数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据管理的详细信息，请参阅[数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)。

## 其他资源 {#additional-resources}

有关更多信息，请阅读DataX](https://developer.verizonmedia.com/datax/guide/)上的Yahoo/Verizon Media [文档。