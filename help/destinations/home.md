---
title: 目标概述
description: 目标是预先构建的与目标平台的集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用Adobe Experience Platform中的“目标”来激活跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例的已知和未知数据。
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 8d57694ffe0ac962b988ebcf9f35fbb7bf816c04
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 3%

---

# [!DNL Destinations] 概述 {#overview}

![目标概述横幅。](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## 目标和源 {#destinations-and-sources}

Platform的核心功能之一是摄取您的第一方数据，并根据您的业务需求激活该数据。 使用[源](../sources/home.md)将数据摄取到Platform中，并使用目标从Platform导出数据。

## 目标步骤 {#steps}

* 从Platform中所有可用目标的[自助服务目录](./catalog/overview.md)中进行选择。
* 使用目标将受众或数据集发送到营销自动化平台、数字广告平台等。
* 定期安排数据导出到您的首选目标。

## 控件 {#controls}

[目标工作区](./ui/destinations-workspace.md)中的控件允许您：

* 浏览可在其中激活数据的目标平台目录；
* 创建、编辑、激活和禁用流向目录中的目标的数据流；
* 在存储位置创建一个帐户，或将Platform链接到目标平台中的帐户；
* 选择应将哪些受众或数据集激活到目标；
* 选择在将受众激活到某些目标（如电子邮件营销目标、CRM平台、云存储位置等）时要导出的[体验数据模型(XDM)字段](../xdm/home.md)。
* 将不同类型的用户档案和受众激活到目标 — 人员、帐户和潜在客户。

## 目标类型和类别 {#types-and-categories}

借助Experience Platform，您可以将数据激活到各种类型的目标，以满足您的激活用例要求。 目标范围从基于API的集成，到与文件接收系统、配置文件查找目标的集成，等等。 有关所有可用目标的详细信息，请阅读[目标类型和类别概述](./destination-types.md)。

## Adobe构建和合作伙伴构建的目标 {#adobe-and-partner-built-destinations}

Experience Platform目标目录中的某些连接器是由Adobe生成和维护的，而其他连接器是由使用[Destination SDK](/help/destinations/destination-sdk/overview.md)的合作伙伴公司生成和维护的。 如果合作伙伴创建并维护了目标，则每个合作伙伴构建的连接器在文档页面顶部的注释会标出。 例如，[Amazon S3连接器](/help/destinations/catalog/cloud-storage/amazon-s3.md)由Adobe创建，而[TikTok连接器](/help/destinations/catalog/social/tiktok.md)由TikTok团队创建和维护。

对于合作伙伴创作并维护的连接器，这意味着连接器问题可能需要由合作伙伴团队解决（文档页面注释中提供的联系方法）。 有关Adobe创作和维护的连接器出现的问题，请联系您的Adobe代表或客户关怀。

## 目标和访问控制 {#access-controls}

Platform中的目标功能可与Adobe Experience Platform访问控制权限配合使用。 根据用户的权限级别，您可以查看、管理和激活目标。 有关各个权限的信息，请转到Adobe Experience Platform中的[访问控制](../access-control/home.md)，然后向下滚动到页面底部的表。

下表概述了对目标执行某些操作所需的权限和权限组合。

| 权限级别 | 描述 |
| ---- | ---- |
| **[!UICONTROL 查看目标]** | 要访问Experience Platform UI中的“目标”选项卡，您需要&#x200B;**[!UICONTROL 查看目标]** [访问控制权限](/help/access-control/home.md#permissions)。 |
| **[!UICONTROL 查看目标]**，**[!UICONTROL 管理目标]** | 若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 |
| **[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** | 要将受众激活到目标并启用工作流的[映射步骤](ui/activate-batch-profile-destinations.md#mapping)，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 |
| **[!UICONTROL 查看目标]**、**[!UICONTROL 激活没有映射的区段]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** | 要在没有访问工作流的[映射步骤](ui/activate-batch-profile-destinations.md#mapping)的情况下在现有数据流中添加或删除受众，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活没有映射的区段]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 |
| **[!UICONTROL 查看目标]**，**[!UICONTROL 管理和激活数据集目标]** | 要将数据集导出到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理和激活数据集目标]** [访问控制权限](/help/access-control/home.md#permissions)。 |
| **[!UICONTROL 查看身份图]** | 要将&#x200B;*标识*&#x200B;导出到目标，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"} |

{style="table-layout:auto"}

根据您想要对目标执行的操作，下图直观地显示了您需要哪些权限。

![显示对目标执行某些操作所需权限的关系图。](/help/destinations/assets/overview/permissions-diagram.png)

有关访问控制的详细信息，请参阅[访问控制用户指南](../access-control/ui/overview.md)。

### 目标的基于属性的访问控制 {#attribute-based-access}

Adobe Experience Platform中基于属性的访问控制允许管理员根据属性控制对特定对象和/或权能的访问。

通过基于属性的访问控制，您可以将映射配置应用到您拥有权限的字段。 此外，如果您无权访问数据集中的所有字段，则无法将数据导出到目标。

有关目标如何使用基于属性的访问控制的详细信息，请阅读[基于属性的访问控制概述](../access-control/abac/overview.md#destinations)。

## 从目标中删除配置文件 {#profile-removal}

在从激活到目标的受众中删除配置文件时，该配置文件也会从目标平台中的相应受众中删除。 例如，如果从先前激活到LinkedIn的受众中删除某个用户档案，则该用户档案将从关联的[!UICONTROL LinkedIn匹配的受众]中删除。

从目标中删除配置文件（也称为取消分段）的频率与分段相同。 从Experience Platform的受众中删除配置文件后，下一个发送到目标的计划数据流就会反映该更改，并从目标受众中删除该配置文件。

配置文件删除在目标平台中生效的实际速度可能会因目标的摄取和处理行为而异。

## 目标监控 {#destinations-monitoring}

在建立与目标连接并完成激活工作流后，您可以监控向接收系统导出的数据。 有关详细信息，请参阅[指南，了解如何在UI](/help/dataflows/ui/monitor-destinations.md)中监视到目标的数据流。

![目标监视页面示例。](./assets/overview/monitoring-page-example.png)

您还可以验证数据是否已成功到达您的目标。 目录中的大多数目标文档页面都有&#x200B;*验证数据导出部分*，该部分指示您如何在目标平台中检查数据是否已成功从Experience Platform导入。 查看[Amazon广告目标](/help/destinations/catalog/advertising/amazon-ads.md#exported-data)的此部分示例。

## 将数据激活到目标的数据治理限制 {#data-governance}

通过以下方式为Platform目标强制执行数据管理：

* 可在创建目标工作流中选择的&#x200B;*营销操作*；
* *数据使用策略*，用于限制将包含特定使用标签的数据激活到具有特定营销操作的目标。

有关[营销操作](../data-governance/policies/overview.md)和[解决数据策略违规](../data-governance/enforcement/auto-enforcement.md)的更多信息，请参阅Platform文档中的数据治理。

有关在创建目标工作流中选择营销操作的更多信息，请参阅Platform中不同目标类型的以下页面：

* [Advertising目标 — Google Ad Manager](./catalog/advertising/google-ad-manager.md)
* [Advertising目标 — Google Ads](./catalog/advertising/google-ads-destination.md)
* [Advertising目标 — Google显示和视频360](./catalog/advertising/google-dv360.md)
* [云存储目标](./catalog/cloud-storage/overview.md)
* [电子邮件营销目标](./catalog/email-marketing/overview.md)
* [社交目标](./catalog/social/overview.md)

有关受众激活工作流中数据策略违规的详细信息，请参阅以下指南中的&#x200B;**[!UICONTROL 审核]**&#x200B;步骤：

* [将受众数据激活到流式受众导出目标](./ui/activate-segment-streaming-destinations.md#review)
* [将受众数据激活到流式配置文件导出目标](./ui/activate-streaming-profile-destinations.md#review)
* [将受众数据激活到批量配置文件导出目标](./ui/activate-batch-profile-destinations.md#review)

## 条款和条件 {#terms-and-conditions}

使用标记为Beta的任何目标(“Beta”)，即表示您在此确认Beta按“原样”提供，不提供任何形式的担保&#x200B;***。***

Adobe没有义务维护、更正、更新、更改、修改或以其他方式支持Beta。 建议您使用信息性的，切勿依赖此类Beta和/或随附材料的正确功能或性能。 Beta被视为Adobe的机密信息。

您向Beta提供的任何“反馈”(有关Beta的信息，包括但不限于您在使用Adobe时遇到的问题或缺陷、建议、改进和推荐)均会分配给Adobe，其中包括针对该反馈的所有权利、标题和兴趣。

提交开放反馈或创建支持工单以共享您的建议或报告错误，寻求功能改进。