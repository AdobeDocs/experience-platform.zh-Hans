---
title: Adobe Campaign Managed Cloud Services连接
description: Adobe Campaign Managed Cloud Services提供了一个平台，用于设计跨渠道客户体验以及可视活动编排、实时交互管理和跨渠道执行的环境。
source-git-commit: ea4d17459dcd7abd981260fe6733320b08af15e8
workflow-type: tm+mt
source-wordcount: '1487'
ht-degree: 4%

---

# Adobe Campaign Managed Cloud Services连接 {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>此集成适用于Adobe Campaign版本8.4或更高版本。 版本8.4计划于2022年9月30日发布。

## 概述 {#overview}

Adobe Campaign Managed Cloud Services提供了一个平台，用于设计跨渠道客户体验以及可视活动编排、实时交互管理和跨渠道执行的环境。 [Campaign快速入门](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)

使用 Campaign 可以：
* 通过客户的单一可访问视图推动个性化和参与,
* 将电子邮件、移动、线上和线下渠道整合到客户历程中,
* 自动投放有意义、及时的消息和优惠.

>[!IMPORTANT]
>
>使用Adobe Campaign Managed Cloud Services连接时请记住以下护栏：
>
>* 最多50个区段可以 [激活](#activate) 对于目标，
>* 对于每个区段，您最多可以在 [地图](#map) Adobe Campaign,
>* Azure Blob存储数据登陆区(DLZ)上的数据保留：7天，
>* 激活频率最少3小时。


## 用例 {#use-cases}

为了帮助您更好地了解如何以及何时使用Adobe Campaign管理服务目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

Adobe Experience Platform会创建一个客户配置文件，其中包含身份图、analytics中的行为数据、合并离线和在线数据等信息。 通过此集成，您可以使用那些支持Adobe Experience Platform的受众来增强Adobe Campaign中已有的分段功能，从而在Campaign中激活该数据。

例如，一家体育服装公司希望利用Adobe Experience Platform支持的智能区段，并使用Adobe Campaign激活这些区段，以通过Adobe Campaign支持的不同渠道联系其客户群。

发送消息后，他们希望使用Adobe Campaign中的体验数据（如发送、打开和单击）来增强Adobe Experience Platform中的客户用户档案。

这样，跨渠道营销活动在Adobe Experience Cloud生态系统中会更加一致，并且客户档案丰富，能够快速进行调整和学习。

[进一步了解Adobe Campaign与Adobe Experience Platform的集成](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html)


## 先决条件 {#prerequisites}

为了使Campaign能够从Adobe Experience Platform中检索数据，您需要创建Campaign API项目，并请求客户关怀将关联的客户ID添加到允许列表。

>[!NOTE]
>
>有关如何创建API项目的全局信息详见 [本文档](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/set-up-developer-console-and-postman.html)

1. 登录到 [Adobe Developer控制台](https://console.adobe.io/) 并创建一个新项目。

1. 选择 **[!UICONTROL 添加API]** 选择 **[!UICONTROL Adobe Campaign]**.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/create-api.png)

1. 生成键对。

1. 选择 `<Instance Name> - admin` 产品配置文件并选择 **[!UICONTROL 保存配置的API]**.

1. 将创建您的API项目。 记下 **[!UICONTROL 客户端ID]** 显示在您的项目中。 联系Adobe客户关怀团队，要求他们将您的客户ID添加到允许列表。

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/client-id.png)

## 支持的身份 {#supported-identities}

*Adobe Campaign Managed Cloud Services* 支持激活下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| external_id | 自定义用户ID | 如果源标识是自定义命名空间，请选择此目标标识。 我们建议使用此标识并将其映射到您的Campaign实例中代表客户的ID(loyaty_ID、account_ID、customer_ID...) |
| ECID | Experience Cloud ID | 表示ECID的命名空间。 此命名空间也可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 请参阅以下文档(位于 [ECID](/help/identity-service/ecid.md) 以了解更多信息。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。 |
| phone_sha256 | 使用SHA256算法进行哈希处理的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 当源字段包含未哈希属性时，请检查 **[!UICONTROL 应用转换]** 选项， [!DNL Platform] 自动对激活时的数据进行哈希处理。 |
| GAID | Google Advertising ID | 如果源标识是GAID命名空间，请选择GAID目标标识。 |
| IDFA | Apple ID for Advertisers | 如果源标识是IDFA命名空间，请选择IDFA目标标识。 |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您要导出区段的所有成员，以及所需的架构字段(例如：电子邮件地址、电话号码、姓氏)，在 [目标激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 导出频度 | **[!UICONTROL 批次]** | 批量目标可将文件以3、6、8、12或24小时为增量导出到下游平台。 有关更多信息 [批量基于文件的目标](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 选择实例]**:您的 **[!DNL Campaign]** 营销实例。
* **[!UICONTROL 目标映射]**:选择您在中使用的目标映射 **[!DNL Adobe Campaign]** 发送投放。 [了解详情](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html)。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

### 治理政策和执法行动 {#governance}

选择适用于要导出到目标的数据的营销操作。 对于Adobe Campaign，我们建议您选择 **[!UICONTROL 电子邮件定位]** 营销操作。

有关营销操作的更多信息，请参阅 [数据使用策略概述](/help/data-governance/policies/overview.md) 页面。

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活受众数据以批量配置文件导出目标](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html) 有关将受众数据激活到此目标的说明。

### 映射属性和标识 {#map}

选择要与用户档案一起导出的XDM字段，并将其映射到相应的Adobe Campaign字段。[了解有关电子邮件营销目标的身份和属性选择的更多信息](overview.md)

1. 选择源字段：

   * 选择 **标识符** (例如：电子邮件字段)，用作唯一标识Adobe Experience Platform和Adobe Campaign中用户档案的源标识。

   * 选择所有其他 **XDM源配置文件属性** 需要输出到Adobe Campaign。
   >[!NOTE]
   >
   >“segmentMembershipStatus”字段是反映segmentMembership状态的必需映射。 此字段默认添加，无法修改或删除。

1. 在Adobe Campaign中将每个字段与其目标字段映射。 可用目标字段由在 [创建目标](#destination-details).

1. 确定强制属性和重复数据删除键。 请注意，标记为“必需”或“重复数据删除键”的属性中的值不能为null。

   * [必需属性](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) 确保所有配置文件记录都包含选定的属性。 例如：所有导出的用户档案都包含电子邮件地址。 建议将标识字段和用作重复数据删除键的字段均设置为必填项。
   * [重复数据删除键](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) 是一个主键，可确定用户希望用户档案进行重复数据删除的身份。

      >[!IMPORTANT]
      >
      >确保重复数据删除键属性的名称与选定目标映射的列名称匹配。
   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. 执行映射后，您可以查看并完成目标配置，以开始向发送数据 **[!DNL Campaign]**.
   [了解如何查看和完成目标配置](/help/destinations/destination-types.md#review).

## 导出的数据/验证数据导出 {#exported-data}

激活目标后，即可在Campaign中访问相应的作业和导出数据。

### 监视数据导出作业 {#jobs}

导航到 **[!UICONTROL 管理]** > **[!UICONTROL 审核]** > **[!UICONTROL 受众加载作业]** 菜单，用于监视从Adobe Experience Platform激活的所有导出作业。

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### 访问导出的数据 {#data}

导航到 **[!UICONTROL 用户档案和目标]** > **[!UICONTROL 列表]** > **[!UICONTROL AEP受众]** 菜单访问激活目标后创建的受众。

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，读取 [数据管理概述](/help/data-governance/home.md).
