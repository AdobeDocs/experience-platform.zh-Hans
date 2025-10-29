---
title: Verizon MediaYahoo DataX连接
description: DataX是一个聚合的Verizon Media/Yahoo基础架构，它托管着各种组件，使Verizon Media/Yahoo能够以安全、自动化和可扩展的方式与外部合作伙伴交换数据。
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 3%

---

# [!DNL Verizon Media/Yahoo DataX]连接

## 概述 {#overview}

[!DNL DataX]是一个聚合[!DNL Verizon Media/Yahoo]基础结构，它托管各种组件，这些组件使[!DNL Verizon Media/Yahoo]能够以安全、自动和可伸缩的方式与其外部合作伙伴交换数据。

>[!IMPORTANT]
>
>此目标连接器和文档页面由[!DNL Verizon Media/Yahoo]的[!DNL DataX]团队创建并维护。 如有任何查询或更新请求，请直接通过[dataoperations@yahooinc.com](mailto:dataoperations@yahooinc.com)联系他们

## 先决条件 {#prerequisites}

**MDM ID**

这是[!DNL Yahoo DataX]中的唯一标识符，并且是用于设置数据导出到此目标的必填字段。 如果您不知道此ID，请与您的[!DNL Yahoo DataX]客户经理联系。

**分类元数据**

分类资源在基[!DNL DataX]元数据结构上定义扩展

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

有关[分类元数据](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/)的更多信息，请参阅[!DNL DataX]开发人员文档。

## 费率限制和护栏 {#rate-limits-guardrails}

>[!IMPORTANT]
>
>将超过100个受众激活到[!DNL Verizon Media/Yahoo DataX]时，您可能会收到来自目标的速率限制错误。 将受众激活到此目标时，请尝试在一个激活数据流中激活少于100个受众。 如果需要激活更多区段，请在同一帐户上创建一个新目标。

根据[!DNL DataX]DataX文档[中概述的分类和受众帖子的配额限制，](https://developer.verizonmedia.com/datax/guide/rate-limits/)是费率限制的。


| 错误代码 | 错误消息 | 描述 |
|---------|----------|---------|
| 429请求过多 | 超过每小时的速率限制&#x200B;**（限制： 100）** | 每个提供商一小时内允许的请求数。 |

{style="table-layout:auto"}

## 支持的身份 {#supported-identities}

[!DNL Verizon Media]支持激活下表中描述的标识。 了解有关[标识](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以便在激活时自动对[!DNL Experience Platform]数据进行哈希处理。 |
| GAID | GOOGLE ADVERTISING ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Audience export]** | 您正在导出具有Verizon Media目标中所用标识符(Email、GAID、IDFA)的受众的所有成员。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 用例 {#use-cases}

[!DNL DataX] API可用于广告商，这些广告商希望定位以[!DNL Verizon Media] (VMG)中的电子邮件地址作为关键字的特定受众组，它们可以使用VMG的近乎实时API快速创建新受众并推送所需的受众组。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

Experience Platform UI中的![Yahoo DataX目标卡](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL MDM ID]**：这是[!DNL Yahoo DataX]中的唯一标识符，是设置数据导出到此目标的必填字段。 如果您不知道此ID，请与您的[!DNL Yahoo DataX]客户经理联系。  使用MDM ID时，可以限制数据仅用于特定一组独占用户（例如广告商的第一方数据）。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到目标的说明，请阅读[将配置文件和受众激活到目标](../../ui/activate-segment-streaming-destinations.md)。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans)。

## 其他资源 {#additional-resources}

有关详细信息，请参阅[!DNL Yahoo/Verizon Media][上的 [!DNL DataX] &#x200B;](https://developer.verizonmedia.com/datax/guide/)文档。
