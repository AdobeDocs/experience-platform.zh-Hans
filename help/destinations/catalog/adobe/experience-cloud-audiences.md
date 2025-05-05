---
title: Experience Cloud 受众
description: 了解如何将Real-time Customer Data Platform中的受众共享到各种Experience Cloud应用程序。
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1703'
ht-degree: 2%

---


# [!UICONTROL Experience Cloud受众]连接

>[!AVAILABILITY]
>
> 此目标对[Adobe Real-time Customer Data Platform Prime和Ultimate](https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform.html)客户可用。

使用此目标可将受众从Real-Time CDP激活到Audience Manager和Adobe Analytics。

要将受众发送到Adobe Analytics，您需要Audience Manager许可证。 有关详细信息，请参阅[Audience Analytics概述](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html?lang=zh-Hans)。

若要将受众发送到其他Adobe解决方案，请使用从Real-Time CDP到[Adobe Target](../personalization/adobe-target-connection.md)、[Adobe Advertising](../advertising/adobe-advertising-cloud-connection.md)、[Adobe Campaign](../email-marketing/adobe-campaign.md)和[Marketo Engage](../adobe/marketo-engage.md)的直接连接。

>[!IMPORTANT]
>
>此目标将Real-time Customer Data Platform中的[旧版受众共享集成](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=zh-Hans#aep-segments-in-aam)替换为各种Experience Cloud解决方案。
> 
>如果您已通过[旧版受众共享集成](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=zh-Hans#aep-segments-in-aam)将受众从Real-Time CDP共享到Audience Manager和其他Experience Cloud解决方案，则必须联系客户关怀部门以禁用旧版集成，然后才能使用此目标。

![Experience Cloud受众目标，在目标目录中突出显示。](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

## 用例和好处 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用[!UICONTROL Experience Cloud受众]目标，以下是Real-Time CDP客户可以使用此目标解决的示例用例。

### 启用数据管理平台用例 {#dmp-use-cases}

在Audience Manager中，您可以将Real-Time CDP受众用于数据管理平台用例，例如：

* 正在将[第三方数据](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=zh-Hans#third-party-data)添加到您的区段；
* [算法建模](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=zh-Hans)；
* 将受众激活到基于Cookie的目标，而Real-Time CDP目标目录尚不支持这些目标。

### 对导出受众的精细控制 {#segments-control}

要选择要导出到Audience Manager及其他受众的受众，请通过Experience Cloud受众目标使用新的自助受众共享集成。  这允许您确定要与其他Experience Cloud解决方案共享的受众，以及要专门保留在Real-Time CDP中的受众。

旧版受众共享集成不允许精确控制应将哪些受众导出到Audience Manager及其他。

### 与Adobe Analytics共享Real-Time CDP受众 {#share-audiences-with-analytics}

您发送到Experience Cloud受众目标的受众不会自动显示在Adobe Analytics中。

在将受众发送到Adobe Analytics之前，您必须[实施适用于Analytics和Audience Manager的Experience Cloud标识服务](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-aam-analytics.html?lang=zh-Hans)。

>[!IMPORTANT]
>
>要通过Experience Cloud受众目标将受众从Real-Time CDP发送到Adobe Analytics，您必须具有Audience Manager许可证。

### 与其他Experience Cloud解决方案共享Real-Time CDP受众 {#share-segments-with-other-solutions}

您可以使用Real-Time CDP Audiences目标卡与其他Experience Cloud解决方案共享受众。

但是，如果要与这些解决方案共享Adobe，受众强烈建议使用以下专用目标卡：

* [Adobe Campaign](../email-marketing/adobe-campaign.md)
* [Adobe Target](../personalization/adobe-target-connection.md)
* [Advertising Cloud](../advertising/adobe-advertising-cloud-connection.md)
* [Marketo](../adobe/marketo-engage.md)

## 先决条件 {#prerequisites}

>[!IMPORTANT]
>
> * 您需要Audience Manager许可证才能启用上面进一步提到的[数据管理平台用例](#dmp-use-cases)。
> * 您&#x200B;*do*&#x200B;需要Audience Manager许可证才能与Adobe Analytics共享Real-Time CDP受众。
> * 您&#x200B;*不需要* Audience Manager许可证即可与以上[&#128279;](#share-segments-with-other-solutions)的部分中提到的Adobe Advertising Cloud、Adobe Target、Marketo和其他Experience Cloud解决方案共享Real-Time CDP受众。

### 适用于使用旧版受众共享解决方案的客户

如果您已通过[旧版受众共享集成](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=zh-Hans#aep-segments-in-aam)将受众从Real-Time CDP共享到Audience Manager和其他Experience Cloud解决方案，则必须联系客户关怀团队以禁用旧版集成。

解决取消置备票证的周转时间为六个工作日或更短。 禁用现有的旧版集成后，您可以通过自助服务目标卡继续[创建连接](#connect)。

>[!IMPORTANT]
>
>从票证解析到通过目标卡建立新连接期间，从Real-Time CDP导出到您其他解决方案的受众操作将停止。 您可以在票证关闭后通过目标卡创建连接，从而最大程度地缩短停机时间。

## 已知限制和标注 {#known-limitations}

使用Experience Cloud受众信息卡时，请注意以下已知限制和重要标注：

* 目前，支持单个Experience Cloud受众目标。 尝试配置第二个目标连接会导致错误。
* 连接到目标时，您可以看到[启用数据流警报](../../ui/alerts.md)的选项。 虽然在UI中可见，但目前不支持&#x200B;**启用警报选项**。
* **受众回填支持**：首次导出到Audience Manager或其他Experience Cloud解决方案时包含受众的历史群体。 [旧版受众共享集成](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=zh-Hans#aep-segments-in-aam)的用户在配置此目标时，应当预期回填差异约为6小时。
* 不直接支持源自[受众合成](../../../segmentation/ui/audience-composition.md)的受众。 若要将复合受众激活到此目标，您必须根据复合受众，通过[区段生成器](../../../segmentation/ui/segment-builder.md)创建受众定义，并激活新创建的受众。

### 激活受众时的延迟 {#audience-activation-latency}

从首次在Real-Time CDP中激活受众到准备好在Audience Manager和其他Experience Cloud解决方案中使用受众，会延迟4小时。

受众可能需要24小时才能在Audience Manager中完全可用于所有用例。 Experience Cloud受众中的受众可能需要48小时才能显示在Audience Manager报表中。

在设置导出到Experience Cloud受众目标的过程后的几分钟内，Audience Manager即可提供元数据，例如受众名称。

## 支持的身份 {#supported-identities}

导出到[!UICONTROL Experience Cloud受众]目标的配置文件将映射到下表中描述的身份。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| ECID | Experience Cloud ID | 表示ECID的命名空间。 此命名空间还可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 有关详细信息，请参阅[ECID](/help/identity-service/features/ecid.md)上的以下文档。 |
| GAID | GOOGLE ADVERTISING ID | 提取到Real-Time CDP中以主要标识Google Advertising ID (GAID)的用户档案可导出到此目标。 |
| IDFA | 广告商的Apple ID | 提取到Real-Time CDP的以广告商Apple ID (IDFA)为主要标识的用户档案可导出到此目标。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | 摄取到Real-Time CDP并具有经过哈希处理的电子邮件地址的主要标识的用户档案，可导出到此目标。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

本节介绍可导出到此目标的受众类型。

| 受众来源 | 支持 | 描述 |
| ---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform[分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ {\f13 } | 受众[已将](../../../segmentation/ui/audience-portal.md#import-audience)从CSV文件导入到Experience Platform中。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在导出以上部分中列出的以身份作为关键字的受众的所有成员。 |
| 导出频率 | **[!UICONTROL 正在流式传输]** | 流目标为基于API的“始终运行”连接。 当基于受众评估在Real-Time CDP中更新用户档案时，连接器会将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证目标，请在目录中的目标卡片视图中选择&#x200B;**[!UICONTROL 设置]**，然后选择&#x200B;**[!UICONTROL 连接到目标]**。

![Experience Cloud受众目标的“连接到目标”选项视图。](../../assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![配置新的目标屏幕，其中显示连接到Experience Cloud受众目标的必需和可选设置。](../..//assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。 不需要[映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)，并且没有可用于此目标的[计划步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling)。

## 验证数据导出 {#exported-data}

要验证数据导出是否成功，您可以检查受众是否已成功导出到所需的Experience Cloud解决方案。

### 验证Audience Manager中的数据

您的Real-Time CDP受众在Audience Manager中显示为[信号](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=zh-Hans#aep-segments-as-aam-signals)、[特征](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=zh-Hans#aep-segments-as-aam-traits)和[区段](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=zh-Hans#aep-segments-as-aam-segments)。 您可以在Audience Manager中验证数据是否已按照上述文档链接中的说明显示。

从Real-Time CDP发送Audience Manager15分钟后，区段名称即开始填充受众。

区段人口在从Real-Time CDP发送后的6小时内开始流入Audience Manager，并在Audience Manager中每24小时更新一次。

72小时后，整个群体将在Audience Manager中可见，并且群体将继续流入Audience Manager，除非从Real-Time CDP中的目标删除受众。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Real-Time CDP]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](/help/data-governance/home.md)。

Real-Time CDP中的数据治理由[数据使用标签](/help/data-governance/labels/reference.md)和营销操作强制执行。
数据使用标签会传输到应用程序，但营销操作不会。 这意味着，一旦受众进入Audience Manager，Real-Time CDP的受众就可以导出到任何可用的目标。 在Audience Manager中，您可以使用[数据导出控件](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=zh-Hans)来阻止将受众导出到特定目标。

使用[!DNL HIPAA]营销操作标记的受众不会从Real-Time CDP发送到Audience Manager。

### Audience Manager中的权限管理

Audience Manager中的受众和特征受基于[角色的访问控制](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=zh-Hans) (RBAC)的约束。

从Real-Time CDP导出的受众将分配给名为&#x200B;**[!UICONTROL Experience Platform区段]**&#x200B;的Audience Manager中的特定数据源。

要仅允许某些用户访问受众，请使用[基于角色的访问控制](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=zh-Hans)配置用户对从Real-Time CDP受众创建的受众和特征的访问权限。
