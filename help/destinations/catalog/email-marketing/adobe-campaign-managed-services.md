---
title: Adobe Campaign Managed Cloud Services连接
description: Adobe Campaign Managed Cloud Services提供了跨渠道客户体验设计平台，并为可视化的活动编排、实时互动管理和跨渠道执行提供了环境。
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '1721'
ht-degree: 2%

---

# [!DNL Adobe Campaign Managed Cloud Services]连接 {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>此集成适用于[[!DNL Adobe Campaign] 版本8.4或更高版本](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html?lang=zh-Hans#release-8-4-1)。

## 概述 {#overview}

[!DNL Adobe Campaign Managed Cloud Services]提供了跨渠道客户体验设计平台，并为可视化的活动编排、实时互动管理和跨渠道执行提供了环境。 [开始使用营销活动](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html?lang=zh-Hans)

使用 Campaign 可以：

* 通过可访问的单一客户视图推动个性化和参与，
* 将电子邮件、移动设备、线上和线下渠道整合到客户历程中，
* 自动投放有意义、及时的消息和优惠。

## 护栏 {#guardrails}

使用[!DNL Adobe Campaign Managed Cloud Services]连接时，请牢记以下护栏：

* 您最多可以[激活](#activate)25个受众到此目标。

  您可以通过更新Campaign资源管理器的&#x200B;**>** > **[!UICONTROL Administration]**&#x200B;文件夹中的&#x200B;**[!UICONTROL Platform]** NmsCdp_Aep_Audience_List_Limit **[!UICONTROL Options]**&#x200B;选项的值来更改此限制。 此护栏限制了在所有配置的目标中可导出到单个Campaign实例的Experience Platform受众总数。

* 对于每个受众，您最多可以添加20个字段到[映射](#map)到[!DNL Adobe Campaign]。

  您可以通过更新Campaign资源管理器的&#x200B;**>** > **[!UICONTROL Administration]**&#x200B;文件夹中的&#x200B;**[!UICONTROL Platform]** NmsCdp_Aep_Destinations_Max_Columns **[!UICONTROL Options]**&#x200B;选项的值来更改此限制。

* Azure Blob Storage Data Landing Zone (DLZ)上的数据保留：7天。
* 激活频率至少为3小时。
* 此连接支持的最大文件名长度为255个字符。 当您[配置导出的文件名](../../ui/activate-batch-profile-destinations.md#configure-file-names)时，请确保文件名不超过255个字符。 超过最大文件名长度会导致激活错误。
* 将受众导出到`&`时，不支持包含特殊字符（例如： [!DNL Adobe Campaign]）的区段/受众。

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用[!DNL Adobe Campaign]管理服务目标，以下是[!DNL Adobe Experience Platform]客户可以通过使用此目标解决的示例用例。

* [!DNL Adobe Experience Platform]创建一个客户个人资料，该资料包含身份图、来自analytics的行为数据、合并离线和在线数据等信息。 通过此集成，您可以使用[!DNL Adobe Campaign]支持的受众来增强[!DNL Adobe Experience Platform]中现有的分段功能，从而在Campaign中激活这些数据。

  例如，一家运动服装公司想要利用[!DNL Adobe Experience Platform]支持的受众，并使用[!DNL Adobe Campaign]激活他们，以便通过[!DNL Adobe Campaign]支持的不同渠道联系其客户群。 发送消息后，他们希望使用[!DNL Adobe Experience Platform]中的体验数据（如发送、打开和点击）增强[!DNL Adobe Campaign]中的客户配置文件。

  结果是跨渠道营销活动在整个Adobe Experience Cloud生态系统中变得更加一致，并拥有丰富的客户档案，可以快速适应和学习。


* 除了在Campaign中激活受众之外，您还可以利用[!DNL Adobe Campaign Managed Services]目标引入其他配置文件属性，这些属性与[!DNL Adobe Experience Platform]上的配置文件相关联并设置了同步流程，以便在[!DNL Adobe Campaign]数据库中更新。

  例如，假设您在[!DNL Adobe Experience Platform]中捕获了选择启用和选择禁用值。 通过此连接，您可以将这些值引入[!DNL Adobe Campaign]并设置同步进程，以便定期更新它们。

  >[!NOTE]
  >
  >配置文件属性同步可用于[!DNL Adobe Campaign]数据库中已存在的配置文件。

[了解有关 [!DNL Adobe Campaign] 与 [!DNL Adobe Experience Platform]集成的更多信息](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=zh-Hans)

## 支持的身份 {#supported-identities}

*[!DNL Adobe Campaign Managed Cloud Services]*&#x200B;支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| external_id | 自定义用户标识 | 当源身份是自定义命名空间时，请选择此目标身份。 我们建议使用此标识，并将其映射到您的Campaign实例中表示客户的ID(loyalty_ID、account_ID、customer_ID...) |
| ECID | Experience Cloud ID | 表示ECID的命名空间。 此命名空间还可以由以下别名引用：“Adobe Marketing Cloud ID”、“[!DNL Adobe Experience Cloud] ID”、“[!DNL Adobe Experience Platform] ID”。 有关详细信息，请参阅[ECID](/help/identity-service/features/ecid.md)上的以下文档。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | [!DNL Adobe Experience Platform]支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以便在激活时自动对[!DNL Experience Platform]数据进行哈希处理。 |
| phone_sha256 | 使用SHA256算法散列的电话号码 | [!DNL Adobe Experience Platform]支持纯文本和SHA256哈希电话号码。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以便在激活时自动对[!DNL Experience Platform]数据进行哈希处理。 |
| GAID | GOOGLE ADVERTISING ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 所有其他受众来源 | 否 | 此类别包括通过[!DNL Segmentation Service]生成的受众之外的所有受众来源。 了解[各种受众源](/help/segmentation/ui/audience-portal.md#customize)。 一些示例包括： <ul><li> 自定义上传受众[从CSV文件导入](../../../segmentation/ui/audience-portal.md#import-audience)到Experience Platform，</li><li> 相似的受众， </li><li> 联合受众， </li><li> 其他Experience Platform应用程序（如[!DNL Adobe Journey Optimizer]）中生成的受众， </li><li> 等等。 </li></ul> |

{style="table-layout:auto"}



按受众数据类型划分的受众支持：

| 受众数据类型 | 受支持 | 描述 | 用例 |
|--------------------|-----------|-------------|-----------|
| [人员受众](/help/segmentation/types/people-audiences.md) | 是 | 根据客户个人资料，允许您针对特定的营销活动人群组进行定位。 | 频繁购买者，购物车放弃者 |
| [帐户受众](/help/segmentation/types/account-audiences.md) | 否 | 针对特定组织内的个人，制定基于帐户的营销策略。 | B2B营销 |
| [潜在客户受众](/help/segmentation/types/prospect-audiences.md) | 否 | 定位尚未成为客户但与目标受众具有共同特征的个人。 | 利用第三方数据发现潜在客户 |
| [数据集导出](/help/catalog/datasets/overview.md) | 否 | 存储在[!DNL Adobe Experience Platform]数据湖中的结构化数据的集合。 | 报告、数据科学工作流 |

{style="table-layout:auto"}


## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Profile-based]** | 您正在导出受众的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如[目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的选择配置文件属性屏幕中所选。 |
| 导出频率 | **[!UICONTROL Batch]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 阅读有关[基于批处理文件的目标](/help/destinations/destination-types.md#file-based)的详细信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![[!DNL Adobe Campaign Managed Cloud Services]目标详细信息表单，其中显示了“名称”、“描述”、“实例选择”、“目标映射”和“同步类型”等字段。](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Select instance]**：您的&#x200B;**[!DNL Campaign]**&#x200B;营销实例。
* **[!UICONTROL Target mapping]**：选择您在&#x200B;**[!DNL Adobe Campaign]**&#x200B;中使用的目标映射以发送投放。 [了解详情](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html?lang=zh-Hans)。
* **[!UICONTROL Select sync type]**：

   * **[!UICONTROL Audience sync]**：使用此选项将[!DNL Adobe Experience Platform]受众发送到[!DNL Adobe Campaign]。
   * **[!UICONTROL Profile sync (Update only)]**：使用此选项将[!DNL Adobe Experience Platform]配置文件属性引入[!DNL Adobe Campaign]并设置同步进程，以便定期更新它们。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅有关使用UI订阅目标警报[的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

### 治理策略和实施行动 {#governance}

选择适用于要导出到目标的数据的营销操作。 对于[!DNL Adobe Campaign]，我们建议您选择&#x200B;**[!UICONTROL Email Targeting]**&#x200B;营销操作。

有关营销操作的更多信息，请参阅[数据使用策略概述](/help/data-governance/policies/overview.md)页面。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
>
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众数据激活到此目标的说明，请阅读[将受众数据激活到批量配置文件导出目标](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=zh-Hans)。

### 映射属性和身份 {#map}

选择要与配置文件一起导出的XDM字段，并将它们映射到相应的[!DNL Adobe Campaign]字段。[了解有关电子邮件营销目标的身份和属性选择的更多信息](overview.md)

1. 选择源字段：

   * 选择&#x200B;**标识符**（例如：电子邮件字段）作为源标识，该标识唯一标识[!DNL Adobe Experience Platform]和[!DNL Adobe Campaign]中的配置文件。

   * 选择需要导出到&#x200B;**的所有其他** XDM源配置文件属性[!DNL Adobe Campaign]。

   >[!NOTE]
   >
   >“segmentMembershipStatus”字段是反映segmentMembership状态的必需映射。 此字段默认添加，无法修改或删除。

1. 在[!DNL Adobe Campaign]中映射每个字段及其目标字段。 可用的目标字段由[创建目标](#destination-details)时选择的目标映射决定。

1. 确定必需属性和重复数据删除键。 请注意，标记为“必需”或“重复数据删除键”的属性中的值不能为空。

   * [必需属性](../../ui/activate-batch-profile-destinations.md#mandatory-attributes)确保所有配置文件记录都包含所选属性。 例如：所有导出的用户档案都包含电子邮件地址。 建议将标识字段和用作重复数据删除键的字段均设置为必填字段。
   * [重复数据删除键](../../ui/activate-batch-profile-destinations.md#mandatory-attributes)是一个主键，它决定了用户希望为其配置文件进行重复数据删除的身份。

     >[!IMPORTANT]
     >
     >确保重复数据删除键属性的名称与所选目标映射的列名称匹配。

   ![属性映射屏幕显示映射到[!DNL Adobe Campaign]目标字段的XDM源字段，带有必需键指示符和重复数据删除键指示符。](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. 执行映射后，您可以查看并完成目标配置以开始向&#x200B;**[!DNL Campaign]**&#x200B;发送数据。
   [了解如何查看和完成目标配置](/help/destinations/destination-types.md#destination-types-and-categories)。

## 导出的数据/验证数据导出 {#exported-data}

激活目标后，您可以在Campaign中访问相应的作业和导出的数据。

### 监测数据导出作业 {#jobs}

导航到&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Audit]** > **[!UICONTROL Audience load jobs]**&#x200B;菜单，以监视从[!DNL Adobe Experience Platform]激活的所有导出作业。

![[!DNL Adobe Campaign]受众加载作业屏幕显示从[!DNL Adobe Experience Platform].](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)激活的导出作业

### 访问导出的数据 {#data}

对于&#x200B;**[!UICONTROL Audience sync]**，您可以通过导航到&#x200B;**[!UICONTROL Profile and target]** > **[!UICONTROL List]** > **[!UICONTROL AEP audiences]**&#x200B;菜单来检查导出的受众。

![[!DNL Adobe Campaign] AEP受众列表视图显示在配置文件和target下可用的从Experience Platform导出的受众。](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

对于&#x200B;**[!UICONTROL Profile sync (Update only)]**，目标中激活的受众所定向的每个用户档案，其数据都会自动更新到Campaign数据库中。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请阅读[数据治理概述](/help/data-governance/home.md)。
