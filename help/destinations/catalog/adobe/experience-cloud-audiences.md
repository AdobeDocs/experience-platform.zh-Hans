---
title: （测试版）Experience Cloud受众
description: 了解如何将区段从Experience Platform共享到各种Experience Platform解决方案。
source-git-commit: 75eb72a8325c92961d9fe26f7e86d15fecf97043
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 2%

---


# （测试版） [!UICONTROL Experience Cloud受众] 连接

此目标允许您将区段从Experience Platform共享到各种Experience Cloud解决方案，如Audience Manager、Analytics、Advertising Cloud、Adobe Campaign、Target或Marketo。

![Experience Cloud受众目标，在目标目录中突出显示。](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* 此目标将 [旧版区段共享集成](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) 从Experience Platform到各种Experience Cloud解决方案。
>* 此目标当前处于测试阶段。 文档和功能可能会发生更改。


## 用例和优势 {#use-cases}

为了帮助您更好地了解应如何以及何时应使用 [!UICONTROL Experience Cloud受众] 目标中，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 启用数据管理平台用例 {#dmp-use-cases}

在Audience Manager中，您可以将Experience Platform区段用于数据管理平台用例，例如：

* 添加 [第三方数据](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) 到您的区段；
* [算法建模](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* 将区段激活到基于Cookie的目标，这些目标在Experience Platform目录中尚不受支持。

### 精细控制导出的区段 {#segments-control}

通过“Experience Cloud受众”目标使用新的自助区段共享集成，选择要导出到Audience Manager及其他区段的区段。 这允许您确定要与其他Experience Cloud解决方案共享的区段，以及要专门保留Experience Platform的区段。

旧版区段共享集成不允许精细控制应将哪些区段导出到Audience Manager及其他区段。

### 与更多Experience Platform解决方案共享Experience Cloud区段 {#share-segments-with-other-solutions}

除了与Audience Manager共享区段外，Experience Platform受众目标卡还允许您与您配置的任何其他Experience Cloud解决方案共享区段，包括：

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
> * 此目标可用于 [Adobe Real-time Customer Data Platform Prime和Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 客户。
> * 您需要获得Audience Manager许可证才能启用上面部分中所述的数据管理平台用例。
> * 您 *不需要* 通过“Experience Platform受众”集成，可与Adobe Advertising Cloud、Adobe Target、Marketo及其他Experience Cloud解决方案共享Experience Cloud区段的Audience Manager许可证。


### 对于使用旧版区段共享解决方案的客户

如果您已经通过 [旧版区段共享集成](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam)，则要禁用旧版集成，您必须联系客户关怀或客户成功经理。 客户关怀和客户支持管理团队必须提交Jira票证(请参阅模板票证AAM-52354)才能禁用集成。

为测试版客户解决取消置备票证的周转时间为6个工作日或更短。 禁用现有旧版集成后，您可以继续 [创建连接](#connect) 通过自助服务目的卡。

>[!IMPORTANT]
>
>从Experience Platform到通过目标卡建立新连接之间的时间，将停止从客户导出到其他解决方案的区段。 在Jira票证关闭后，您可以通过目标卡创建连接，从而最大限度地减少此停机时间。

## 已知限制和标注 {#known-limitations}

请注意以下已知限制和“Experience Cloud受众”卡测试版中的重要标注：

* [数据流监控](/help/dataflows/ui/monitor-destinations.md) 不支持。
* 连接到目标时，您可以看到 [启用数据流警报](#enable-alerts). 尽管在UI中可见，但 **不支持“启用警报”选项** 测试版中。
* **不支持回填**. 首次导出到Audience Manager或其他Experience Cloud解决方案不包括区段的历史群体。
* 在测试版中，您可以创建 **到Experience Cloud受众目标的单个目标连接**，跨属于您的Experience Platform组织的所有沙箱。
* 有 **4小时延迟** 从Experience Platform中激活数据到准备在Audience Manager和其他Experience Cloud解决方案中使用数据的时间。

## 支持的身份 {#supported-identities}

导出到的用户档案 [!UICONTROL Experience Cloud受众] 目标映射到下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| ECID | Experience Cloud ID | 表示ECID的命名空间。 此命名空间也可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 请参阅以下文档(位于 [ECID](/help/identity-service/ecid.md) 以了解更多信息。 |
| GAID | Google Advertising ID | 通过Google广告ID(GAID)主标识摄取到Experience Platform的用户档案，可以导出到此目标。 |
| IDFA | Apple ID for Advertisers | 使用Apple ID for Advertisers(IDFA)的主标识摄取到Experience Platform的用户档案，可以导出到此目标。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | 被摄取到具有经过哈希处理的电子邮件地址主标识的Experience Platform的用户档案，可以导出到此目标。 |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您要导出区段（受众）的所有成员，这些成员无需使用上述部分中列出的标识。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

>[!IMPORTANT]
> 
>在测试版中，您可以在属于您的Experience Cloud组织的所有沙箱中，创建到Experience Platform受众目标的单个目标连接。

### 对目标进行身份验证 {#authenticate}

要对目标进行身份验证，请选择 **[!UICONTROL 设置]** 在目录的目标卡片视图中，选择 **[!UICONTROL 连接到目标]**.

![“Experience Cloud受众”目标的“连接到目标”选项的视图。](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![配置新目标屏幕，其中显示连接到Experience Cloud受众目标的必需和可选设置。](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.


## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活用户档案和区段以流式传输区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。 请注意，否 [映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 是必需的，否 [计划步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 可用于此目标。

## 验证数据导出 {#exported-data}

要验证数据导出是否成功，您可以检查区段是否已成功导入所需的Experience Cloud解决方案。

### 在Audience Manager中验证数据

您的Experience Platform区段在Audience Manager中显示为 [信号](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [特征](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits)和 [区段](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). 您可以在Audience Manager中验证数据是否已按照上述文档链接中的说明显示。

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，读取 [数据管理概述](/help/data-governance/home.md).

Experience Platform中的数据管理由两者强制执行 [数据使用标签](/help/data-governance/labels/reference.md) 和营销操作。
数据使用标签将传输到应用程序，但营销操作不会。 这意味着，一旦客户登陆Audience Manager,Experience Platform中的区段便可导出到任何可用目标。 在Audience Manager中，您可以使用 [数据导出控件](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) 阻止区段导出到特定目标。

### Audience Manager中的权限管理

Audience Manager中的区段和特征受 [基于角色的访问控制](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=zh-Hans) (RBAC)。

从Experience Platform导出的区段会分配给Audience Manager中名为 **[!UICONTROL Experience Platform区段]**.

要仅允许特定用户访问区段，您可以将访问控制应用于属于数据源的区段。 您必须在Audience Manager中为这些区段和从Experience Platform区段创建的特征设置新的访问控制权限。