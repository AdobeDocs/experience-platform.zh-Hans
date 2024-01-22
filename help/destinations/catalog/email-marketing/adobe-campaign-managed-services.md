---
title: Adobe Campaign Managed Cloud Services连接
description: Adobe Campaign Managed Cloud Services提供了跨渠道客户体验设计平台，并为可视化的活动编排、实时互动管理和跨渠道执行提供了环境。
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 1%

---

# Adobe Campaign Managed Cloud Services连接 {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>此集成可与 [Adobe Campaign版本8.4或更高版本](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1).

## 概述 {#overview}

Adobe Campaign Managed Cloud Services提供了跨渠道客户体验设计平台，并为可视化的活动编排、实时互动管理和跨渠道执行提供了环境。 [Campaign入门](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)

使用 Campaign 可以：
* 通过可访问的单一客户视图推动个性化和参与，
* 将电子邮件、移动设备、线上和线下渠道整合到客户历程中，
* 自动投放有意义、及时的消息和优惠。

>[!IMPORTANT]
>
>使用Adobe Campaign Managed Cloud Services连接时，请牢记以下护栏：
>
>* 最多50个区段可以 [已激活](#activate) 对于目标，
>* 对于每个区段，您最多可以添加20个字段到 [映射](#map) Adobe Campaign，
>* Azure Blob Storage数据登陆区(DLZ)上的数据保留：7天，
>* 激活频率至少为3小时。

## 用例 {#use-cases}

为了帮助您更好地了解您应该如何以及何时使用Adobe Campaign管理服务目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

* Adobe Experience Platform创建客户个人资料，整合了身份图、来自analytics的行为数据、合并离线和在线数据等信息。 利用此集成，您可以利用Adobe Experience Platform支持的受众来增强Adobe Campaign中已存在的分段功能，从而在Campaign中激活这些数据。

  例如，一家运动服装公司希望利用Adobe Experience Platform支持的智能区段，并使用Adobe Campaign激活它们，以便通过Adobe Campaign支持的各种渠道联系其客户群。 发送消息后，他们希望使用Adobe Campaign的体验数据（如发送、打开和点击）增强AdobeExperience Platform中的客户配置文件。

  结果是跨渠道营销活动在整个AdobeExperience Cloud生态系统中变得更加一致，并拥有丰富的客户档案，可以快速适应和学习。


* 除了Campaign中的区段激活之外，您还可以利用Adobe Campaign Managed Services目标引入其他配置文件属性，这些属性与Adobe Experience Platform上的配置文件相关联并具有同步流程，以便在Adobe Campaign数据库中更新。

  例如，假设您捕获Adobe Experience Platform中的“选择启用”和“选择禁用”值。 通过此连接，您可以将这些值引入Adobe Campaign并实施同步过程，以便定期更新它们。

  >[!NOTE]
  >
  >配置文件属性同步适用于Adobe Campaign数据库中已存在的配置文件。

[详细了解Adobe Campaign与Adobe Experience Platform的集成](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html)

## 支持的身份 {#supported-identities}

*Adobe Campaign Managed Cloud Services* 支持激活下表中描述的标识。 了解有关 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| external_id | 自定义用户标识 | 当源身份是自定义命名空间时，请选择此目标身份。 我们建议使用此标识，并将其映射到您的Campaign实例中表示客户的ID(loyalty_ID、account_ID、customer_ID...) |
| ECID | Experience Cloud ID | 表示ECID的命名空间。 此命名空间还可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 请参阅以下文档： [ECID](/help/identity-service/ecid.md) 以了解更多信息。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 在激活时自动散列数据。 |
| phone_sha256 | 使用SHA256算法散列的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 在激活时自动散列数据。 |
| GAID | Google广告ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出区段的所有成员，以及所需的架构字段（例如：电子邮件地址、电话号码、姓氏），如 [目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频率 | **[!UICONTROL 批次]** | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 详细了解 [批处理基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 选择实例]**：您的 **[!DNL Campaign]** 营销实例。
* **[!UICONTROL 目标映射]**：选择您在中使用的目标映射 **[!DNL Adobe Campaign]** 以发送投放。 [了解详情](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html)。
* **[!UICONTROL 选择同步类型]**：

   * **[!UICONTROL 受众同步]**：使用此选项可将Adobe Experience Platform受众发送到Adobe Campaign。
   * **[!UICONTROL 配置文件同步（仅更新）]**：使用此选项可将Adobe Experience Platform配置文件属性引入Adobe Campaign并实施同步流程，以便定期更新这些属性。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

### 治理策略和实施行动 {#governance}

选择适用于要导出到目标的数据的营销操作。 对于Adobe Campaign，我们建议您选择 **[!UICONTROL 电子邮件定位]** 营销活动。

有关营销活动的更多信息，请参阅 [数据使用策略概述](/help/data-governance/policies/overview.md) 页面。

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将受众数据激活到批量配置文件导出目标](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html) 有关将受众数据激活到此目标的说明。

### 映射属性和身份 {#map}

选择要与配置文件一起导出的XDM字段，并将它们映射到相应的Adobe Campaign字段。[了解有关电子邮件营销目标的身份和属性选择的更多信息](overview.md)

1. 选择源字段：

   * 选择 **标识符** （例如：电子邮件字段）作为源标识，用于唯一标识Adobe Experience Platform和Adobe Campaign中的用户档案。

   * 选择所有其他 **XDM源配置文件属性** 需要导出到Adobe Campaign的内容。

   >[!NOTE]
   >
   >“segmentMembershipStatus”字段是反映segmentMembership状态的必需映射。 此字段默认添加，无法修改或删除。

1. 在Adobe Campaign中将每个字段映射到其目标字段。 可用的目标字段由以下情况下选择的目标映射决定： [创建目标](#destination-details).

1. 确定必需属性和重复数据删除键。 请注意，标记为“必需”或“重复数据删除键”的属性中的值不能为空。

   * [必需属性](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) 确保所有配置文件记录都包含所选属性。 例如：所有导出的用户档案都包含电子邮件地址。 建议将标识字段和用作重复数据删除键的字段均设置为必填字段。
   * [重复数据删除键](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) 是一个主键，可确定用户希望为其配置文件删除重复数据的身份。

     >[!IMPORTANT]
     >
     >确保重复数据删除键属性的名称与所选目标映射的列名称匹配。

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. 执行映射后，您可以查看并完成目标配置以开始将数据发送到 **[!DNL Campaign]**.
   [了解如何查看和完成目标配置](/help/destinations/destination-types.md#review).

## 导出的数据/验证数据导出 {#exported-data}

激活目标后，您可以在Campaign中访问相应的作业和导出的数据。

### 监测数据导出作业 {#jobs}

导航至 **[!UICONTROL 管理]** > **[!UICONTROL 审核]** > **[!UICONTROL 受众加载作业]** 菜单，用于监视从Adobe Experience Platform激活的所有导出作业。

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### 访问导出的数据 {#data}

对象 **[!UICONTROL 受众同步]**，您可以通过导航到 **[!UICONTROL 配置文件和目标]** > **[!UICONTROL 列表]** > **[!UICONTROL aep受众]** 菜单。

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

对象 **[!UICONTROL 配置文件同步（仅更新）]**，则目标中激活的区段所定向的每个用户档案的数据会自动更新到Campaign数据库中。

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据管理概述](/help/data-governance/home.md).
