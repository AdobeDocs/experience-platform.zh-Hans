---
title: (Beta)Experience Cloud受众
description: 了解如何将区段从Experience Platform共享到各种Experience Platform解决方案。
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1509'
ht-degree: 2%

---

# (Beta) [!UICONTROL Experience Cloud受众] 连接

利用此目标，可将区段从Experience Platform共享到各种Experience Cloud解决方案，如Audience Manager、Analytics、Advertising Cloud、Adobe Campaign、Target或Marketo。

![Experience Cloud受众目标，在目标目录中突出显示。](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* 此目标将替换 [旧版区段共享集成](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) 从Experience Platform到各种Experience Cloud解决方案。
>* 此目标当前为测试版。 文档和功能可能会发生更改。


## 用例和好处 {#use-cases}

为了帮助您更好地了解应该如何以及何时使用 [!UICONTROL Experience Cloud受众] 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 启用数据管理平台用例 {#dmp-use-cases}

在Audience Manager中，您可以将Experience Platform区段用于Data Management Platform用例，例如：

* 添加 [第三方数据](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) 至您的区段；
* [算法建模](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* 将区段激活到Experience Platform目标目录中尚不支持的基于Cookie的目标。

### 导出区段的精细控制 {#segments-control}

通过Experience Cloud受众目标使用新的自助区段共享集成，以选择要导出到Audience Manager和其他受众的区段。 这允许您确定要与其他Experience Cloud解决方案共享的区段以及要专门保留在Experience Platform中的区段。

旧版区段共享集成不允许精细地控制应将哪些区段导出到Audience Manager及其他。

### 与更多Experience Cloud解决方案共享Experience Platform区段 {#share-segments-with-other-solutions}

除了与Audience Manager共享区段外，通过Experience Platform受众目标卡，还可与您配置的任何其他Experience Cloud解决方案共享区段，包括：

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analytics
* Marketo

<!--

Note: briefly talk about when to share segments to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## 先决条件 {#prerequisites}

>[!IMPORTANT]
>
> * 此目标可供 [Adobe Real-time Customer Data Platform Prime和Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 客户。
> * 您需要Audience Manager许可证才能启用 [数据管理平台用例](#dmp-use-cases) 如上所述。
> * 您 *不需要* 用于与Adobe Advertising Cloud、Adobe Target、Marketo和其他Experience Platform解决方案共享Experience Cloud区段的Audience Manager许可证，如中所述 [上节](#share-segments-with-other-solutions).


### 适用于使用旧版区段共享解决方案的客户

如果您已通过，将区段从Experience Platform共享到Audience Manager和其他Experience Cloud解决方案， [旧版区段共享集成](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam)中，您必须联系客户关怀团队或您的Adobe帐户团队以禁用旧版集成。 客户关怀和Adobe帐户团队必须提交Jira票证(请参阅模板票证AAM-52354)才能禁用集成。

为测试版客户解决取消配置工单的周转时间为六个工作日（含）以内。 禁用现有的旧版集成后，您可以继续 [创建连接](#connect) 自助目的地卡。

>[!IMPORTANT]
>
>从Jira票证解析到通过目标卡建立新连接之间的时间，将停止从Experience Platform导出到其他解决方案的区段。 在Jira票证关闭后，您可以通过目标卡创建连接，从而最大限度地减少停机时间。

## 已知限制和标注 {#known-limitations}

请注意Experience Cloud受众信息卡测试版中的以下已知限制和重要标注：

* [数据流监测](/help/dataflows/ui/monitor-destinations.md) 不受支持。
* 连接到目标时，您可以看到一个选项 [启用数据流警报](#enable-alerts). 尽管在UI中可见，但是 **启用警报选项不受支持** （在测试版中）。
* **不支持回填**. 首次导出到Audience Manager或其他Experience Cloud解决方案时不包括区段的历史人口。
* 在测试版中，您可以创建 **到Experience Cloud受众目标的单个目标连接**，跨属于您的Experience Platform组织的所有沙盒。
* 有一个 **4小时延迟** 从Experience Platform中激活数据的时间到准备好将数据用于Audience Manager和其他Experience Cloud解决方案的时间。

## 支持的身份 {#supported-identities}

导出到的配置文件 [!UICONTROL Experience Cloud受众] 目标已映射到下表中描述的标识。 详细了解 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| ECID | Experience Cloud ID | 表示ECID的命名空间。 此命名空间还可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 请参阅以下文档： [ECID](/help/identity-service/ecid.md) 了解更多信息。 |
| GAID | Google广告ID | 可以将具有Google Advertising ID (GAID)主要标识的提取到Experience Platform中的配置文件导出到此目标。 |
| IDFA | 广告商的Apple ID | 可以将使用Apple ID作为广告商(IDFA)主要标识引入到广告的Experience Platform中的用户档案导出到此目标。 |
| email_lc_sha256 | 使用SHA256算法对电子邮件地址进行哈希处理 | 带有经过哈希处理的电子邮件地址的主要标识且被摄取到Experience Platform中的用户档案可以导出到此目标。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您正在导出以上部分中列出的标识作为关键字的区段（受众）的所有成员。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据区段评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

>[!IMPORTANT]
> 
>在测试版中，您可以跨属于您的Experience Platform组织的所有沙盒创建到Experience Cloud受众目标的单个目标连接。

### 向目标进行身份验证 {#authenticate}

要对目标进行身份验证，请选择 **[!UICONTROL 设置]** 在目标卡片视图中，然后选择 **[!UICONTROL 连接到目标]**.

![Experience Cloud受众目标的连接到目标选项视图。](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![配置新的目标屏幕，其中显示连接到Experience Cloud受众目标的必需和可选设置。](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.


## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [将配置文件和区段激活到流式区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。 请注意，否 [映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 是必需的，而不是 [计划步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 可用于此目标。

## 验证数据导出 {#exported-data}

要验证数据导出是否成功，您可以检查区段是否已成功导出到所需的Experience Cloud解决方案。

### 验证Audience Manager中的数据

您的Experience Platform区段在Audience Manager中显示为 [信号](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals)， [特征](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits)、和 [区段](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). 您可以在Audience Manager中验证数据是否已按照上述文档链接中的说明显示。

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关以下方面的详细信息： [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据治理概述](/help/data-governance/home.md).

Experience Platform中的数据治理由两者强制执行 [数据使用标签](/help/data-governance/labels/reference.md) 和营销活动。
数据使用标签将传输到应用程序，但营销操作不会。 这意味着一旦它们进入Audience Manager，Experience Platform中的区段可以导出到任何可用的目标。 在Audience Manager中，您可以使用 [数据导出控制](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) 阻止将区段导出到特定目标。

### Audience Manager中的权限管理

Audience Manager中的区段和特征受 [基于角色的访问控制](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=en) (RBAC)。

从Experience Platform导出的区段会分配给Audience Manager中名为的特定数据源 **[!UICONTROL Experience Platform区段]**.

要仅允许特定用户访问区段，您可以将访问控制应用于属于数据源的区段。 您必须在Audience Manager中为这些区段和从Experience Platform区段创建的特征设置新的访问控制权限。
