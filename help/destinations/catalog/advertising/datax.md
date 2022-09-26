---
title: Verizon MediaYahoo DataX连接
description: DataX是Verizon Media/Yahoo的聚合基础架构，它托管各种组件，使Verizon Media/Yahoo能够以安全、自动和可扩展的方式与其外部合作伙伴交换数据。
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 0580816c471400ba17eddcb6b1a9dfbf01797938
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 3%

---

# [!DNL Verizon Media/Yahoo DataX] 连接

## 概述 {#overview}

[!DNL DataX] 是聚合 [!DNL Verizon Media/Yahoo] 可托管各种组件的基础架构，这些组件支持 [!DNL Verizon Media/Yahoo] 以安全、自动和可扩展的方式与外部合作伙伴交换数据。

>[!IMPORTANT]
>
>此文档页面由 [!DNL Verizon Media/Yahoo]&#39;s [!DNL DataX] 团队。 如有任何查询或更新请求，请直接联系 [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## 先决条件 {#prerequisites}

**MDM ID**

这是 [!DNL Yahoo DataX] 它是设置向此目标导出数据的必填字段。 如果您不知道此ID，请联系您的 [!DNL Yahoo DataX] 客户经理。

**分类元数据**

分类资源定义基础上的扩展 [!DNL DataX] 元数据结构

```
{

  >>(Base DataX Metadata)<<

        "extensions": { "action":
        {string}, "incrementalData":
        {
                "taxonomyId": {string}
                },
                "links": [{
                "rel": "https://datax.yahooapis.com/rels/fullTaxonomy", "title": "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

有关更多信息 [分类元数据](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) 在 [!DNL DataX] 开发人员文档。

## 速率限制和防护 {#rate-limits-guardrails}

>[!IMPORTANT]
>
>在将100个以上的区段激活到 [!DNL Verizon Media/Yahoo DataX]，则可能会从目标收到速率限制错误。 在将区段激活到此目标时，请尝试在一个激活数据流中激活少于100个区段。 如果您需要激活更多区段，请在同一帐户上创建新目标。

[!DNL DataX] 是针对分类和受众帖子的配额限制(如 [DataX文档](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| 错误代码 | 错误消息 | 描述 |
|---------|----------|---------|
| 429请求过多 | 超出速率限制每小时 **(限制：100)** | 每个提供商一小时内允许的请求数。 |

{style=&quot;table-layout:auto&quot;}

## 支持的身份 {#supported-identities}

[!DNL Verizon Media] 支持激活下表所述的身份。 详细了解 [标识](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。 |
| GAID | Google Advertising ID | 如果源标识是GAID命名空间，请选择GAID目标标识。 |
| IDFA | Apple ID for Advertisers | 如果源标识是IDFA命名空间，请选择IDFA目标标识。 |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您正在导出区段（受众）的所有成员，以及Verizon Media目标中使用的标识符（电子邮件、GAID、IDFA）。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 用例 {#use-cases}

[!DNL DataX] API适用于要定位未通过 [!DNL Verizon Media] (VMG)可以使用VMG的近实时API快速创建新区段并推送所需的受众组。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

![Platform UI中的Yahoo DataX目标卡](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL MDM ID]**:这是 [!DNL Yahoo DataX] 它是设置向此目标导出数据的必填字段。 如果您不知道此ID，请联系您的 [!DNL Yahoo DataX] 客户经理。  使用MDM ID，可以限制数据仅用于特定专用用户集（例如广告商的第一方数据）。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [将用户档案和区段激活到目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到目标的说明。

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans).

## 其他资源 {#additional-resources}

有关更多信息，请阅读 [!DNL Yahoo/Verizon Media] [文档 [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
