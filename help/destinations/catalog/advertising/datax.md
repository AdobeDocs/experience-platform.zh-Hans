---
title: Verizon MediaYahoo DataX连接
description: DataX是一个聚合的Verizon Media/Yahoo基础架构，它托管着各种组件，使Verizon Media/Yahoo能够以安全、自动化和可扩展的方式与外部合作伙伴交换数据。
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 3%

---

# [!DNL Verizon Media/Yahoo DataX] 连接

## 概述 {#overview}

[!DNL DataX] 是聚合 [!DNL Verizon Media/Yahoo] 托管各种组件的基础架构，这些组件可以 [!DNL Verizon Media/Yahoo] 以安全、自动化和可扩展的方式与外部合作伙伴交换数据。

>[!IMPORTANT]
>
>此目标连接器和文档页面由创建和维护 [!DNL Verizon Media/Yahoo]的 [!DNL DataX] 团队。 如有任何查询或更新请求，请直接通过以下电子邮件联系他们： [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## 先决条件 {#prerequisites}

**MDM ID**

这是中的唯一标识符 [!DNL Yahoo DataX] 并且它是设置数据导出到此目标的必填字段。 如果您不知道此ID，请联系贵机构的 [!DNL Yahoo DataX] 客户经理。

**分类元数据**

分类资源定义Base上的扩展 [!DNL DataX] 元数据结构

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

详细了解 [分类元数据](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) 在 [!DNL DataX] 开发人员文档。

## 费率限制和护栏 {#rate-limits-guardrails}

>[!IMPORTANT]
>
>在激活100多个受众时 [!DNL Verizon Media/Yahoo DataX]，您可能会收到来自目标的速率限制错误。 将受众激活到此目标时，请尝试在一个激活数据流中激活少于100个受众。 如果需要激活更多区段，请在同一帐户上创建一个新目标。

[!DNL DataX] 是根据 [DataX文档](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| 错误代码 | 错误消息 | 描述 |
|---------|----------|---------|
| 429请求过多 | 每小时超出速率限制 **（限制：100）** | 每个提供商一小时内允许的请求数。 |

{style="table-layout:auto"}

## 支持的身份 {#supported-identities}

[!DNL Verizon Media] 支持激活下表中描述的标识。 了解有关 [身份](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 在激活时自动散列数据。 |
| GAID | Google广告ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在导出具有Verizon Media目标中所用标识符(Email、GAID、IDFA)的受众的所有成员。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 用例 {#use-cases}

[!DNL DataX] API可用于广告商，这些广告商希望定位以中的电子邮件地址作为关键字的特定受众组 [!DNL Verizon Media] (VMG)可以使用VMG的近乎实时的API快速创建新受众并推送所需的受众组。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

![Platform UI中的Yahoo DataX目标卡](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

同时 [设置](../../ui/connect-destination.md) 此目标必须提供以下信息：

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL MDM ID]**：这是中的唯一标识符 [!DNL Yahoo DataX] 并且它是设置数据导出到此目标的必填字段。 如果您不知道此ID，请联系贵机构的 [!DNL Yahoo DataX] 客户经理。  使用MDM ID时，可以限制数据仅用于特定一组独占用户（例如广告商的第一方数据）。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将用户档案和受众激活到目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众激活到目标的说明。

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans).

## 其他资源 {#additional-resources}

欲知更多信息，请参阅 [!DNL Yahoo/Verizon Media] [文档 [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
