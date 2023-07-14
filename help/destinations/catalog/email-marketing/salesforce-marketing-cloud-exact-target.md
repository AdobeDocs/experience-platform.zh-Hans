---
keywords: 电子邮件；电子邮件；电子邮件目标；salesforce；api salesforce marketing cloud目标
title: (API) SalesforceMarketing Cloud连接
description: SalesforceMarketing Cloud（以前称为ExactTarget）目标允许您导出帐户数据，并在SalesforceMarketing Cloud中根据您的业务需求激活该数据。
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: d1bfd85bf7a318692fb6ae87e163dca105d531c6
workflow-type: tm+mt
source-wordcount: '2924'
ht-degree: 1%

---

# [!DNL (API) Salesforce Marketing Cloud] 连接

## 概述 {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/engagement/) (以前称为 [!DNL ExactTarget])是一款数字营销套件，可让您为访客和客户构建和自定义历程，以个性化其体验。

>[!IMPORTANT]
>
>请注意此连接与其他连接之间的区别 [[!DNL Salesforce Marketing Cloud] 连接](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) 电子邮件营销目录部分中存在的电子邮件营销目录。 另一个SalesforceMarketing Cloud连接允许您将文件导出到指定的存储位置，而这是一个基于API的流连接。

比较对象 [!DNL Salesforce Marketing Cloud Account Engagement] 更加面向 **B2B** 营销， [!DNL (API) Salesforce Marketing Cloud] 目标非常适合 **B2C** 事务性决策周期较短的用例。 您可以合并表示目标受众行为的较大数据集，以便通过优先排序和划分联系人（尤其是来自外部数据集）来调整和改进营销活动 [!DNL Salesforce]. *注意，Experience Platform还连接了 [[!DNL Salesforce Marketing Cloud Account Engagement]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md).*

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [!DNL Salesforce Marketing Cloud] [更新联系人](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API，允许您 **添加联系人并更新联系人数据** 满足贵机构的业务需求（在新版本中激活这些功能后） [!DNL Salesforce Marketing Cloud] 区段。

[!DNL Salesforce Marketing Cloud] 使用带有客户端凭据的OAuth 2作为身份验证机制来与 [!DNL Salesforce Marketing Cloud] API。 向您的验证的说明 [!DNL Salesforce Marketing Cloud] 实例位于 [向目标进行身份验证](#authenticate) 部分。

## 用例 {#use-cases}

为了帮助您更好地了解应该如何以及何时使用 [!DNL (API) Salesforce Marketing Cloud] 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 向营销活动的联系人发送电子邮件 {#use-case-send-emails}

家庭租赁平台的销售部门希望向目标客户受众广播营销电子邮件。 平台的营销团队可以添加新联系人/更新现有联系人 *（及其电子邮件地址）* 通过Adobe Experience Platform，根据受众自己的离线数据构建受众，并将这些受众发送到 [!DNL Salesforce Marketing Cloud]，然后可以将其用于发送营销活动电子邮件。

## 先决条件 {#prerequisites}

### Experience Platform中的先决条件 {#prerequisites-in-experience-platform}

将数据激活到之前 [!DNL (API) Salesforce Marketing Cloud] 目标，您必须拥有 [架构](/help/xdm/schema/composition.md)， a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)、和 [区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 创建于 [!DNL Experience Platform].

### 中的先决条件 [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

请注意以下先决条件，以便将数据从Platform导出到 [!DNL Salesforce Marketing Cloud] 帐户：

#### 您需要拥有 [!DNL Salesforce Marketing Cloud] 帐户 {#prerequisites-account}

A [!DNL Salesforce Marketing Cloud] 订购 [[!DNL Marketing Cloud Engagement]](https://www.salesforce.com/products/marketing-cloud/engagement/) 必须提供产品才能继续。

联系至 [[!DNL Salesforce] 支持](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) 如果您没有 [!DNL Salesforce Marketing Cloud] 帐户或您的帐户缺少 [!DNL Marketing Cloud Engagement] 产品订阅。

#### 在中创建属性 [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

将受众激活到 [!DNL (API) Salesforce Marketing Cloud] 目标，则必须在 **[!UICONTROL 映射Id]** 每个已激活受众的字段，位于 **[受众计划](#schedule-segment-export-example)** 步骤。

[!DNL Salesforce] 需要此值才能正确读取和解释从Experience Platform传入的受众，并在中更新其受众状态 [!DNL Salesforce Marketing Cloud]. 请参阅Experience Platform文档，了解 [受众成员资格详细信息架构字段组](/help/xdm/field-groups/profile/segmentation.md) 如果您需要有关受众状态的指南。

对于您从Platform激活到的每个受众 [!DNL Salesforce Marketing Cloud]，您需要创建类型的属性 `Text` 范围 [!DNL Salesforce]. 使用 [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder] 以创建属性。 属性字段名称用于 [!DNL (API) Salesforce Marketing Cloud] 目标字段 **[!UICONTROL 映射]** 步骤。 您可以根据业务需求定义最多4000个字符的字段字符。 请参阅 [!DNL Salesforce Marketing Cloud] [数据扩展数据类型](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) 文档页面，以了解有关属性类型的更多信息。

请参阅 [!DNL Salesforce Marketing Cloud] 文档目标 [创建属性](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) 如果您需要有关创建属性的指导。

中的数据设计器屏幕示例 [!DNL Salesforce Marketing Cloud]，您将向其中添加属性，如下所示：
![SalesforceMarketing CloudUI数据设计器。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

查看 [!DNL Salesforce Marketing Cloud] [!DNL Email Demographics] attribute-set如下所示：
![SalesforceMarketing CloudUI电子邮件人口统计属性集。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demograhics-fields.png)

此 [!DNL (API) Salesforce Marketing Cloud] 目标使用 [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) 以动态检索在中定义的属性及其属性集 [!DNL Salesforce Marketing Cloud].

这些组件会显示在 **[!UICONTROL 目标字段]** 选择窗口 [映射](#mapping-considerations-example) 在至的工作流中 [将受众激活到目标](#activate).

>[!IMPORTANT]
>
>范围 [!DNL Salesforce Marketing Cloud]，您必须使用创建属性 **[!UICONTROL 字段名称]** 与中指定的值完全匹配的值 **[!UICONTROL 映射Id]** 每个已激活的Platform区段。 例如，下面的屏幕快照显示了一个名为的属性 `salesforce_mc_segment_1`. 将受众激活到此目标时，添加 `salesforce_mc_segment_1` 作为 **[!UICONTROL 映射Id]** 将受众受众从Experience Platform填充到此属性中。

中属性创建的示例 [!DNL Salesforce Marketing Cloud]，如下所示：
![显示属性的SalesforceMarketing CloudUI屏幕截图。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
>* 创建属性时，请勿在字段名称中包含空白字符。 请改用下划线 `(_)` 字符。
>* 区分用于Platform受众的属性以及中的其他属性 [!DNL Salesforce Marketing Cloud]中，您可以为用于Adobe区段的属性包含可识别的前缀或后缀。 例如，而不是 `test_segment`，使用 `Adobe_test_segment` 或 `test_segment_Adobe`.
>* 如果您已在中创建其他属性 [!DNL Salesforce Marketing Cloud]，您可以使用与Platform区段相同的名称，轻松地识别中的受众 [!DNL Salesforce Marketing Cloud].

#### 在中分配用户角色和权限 [!DNL Salesforce Marketing Cloud] {#prerequisites-roles-permissions}

作为 [!DNL Salesforce Marketing Cloud] 支持自定义角色，根据您的用例，应该为您的用户分配相关角色，以更新您的属性 [!DNL Salesforce Marketing Cloud] 属性集。 下面显示了分配给用户的角色示例：
![选定用户的SalesforceMarketing CloudUI，其中显示为其分配的角色。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-edit-roles.png)

根据您所使用的角色 [!DNL Salesforce Marketing Cloud] 用户已分配，您还需要将权限分配给 [!DNL Salesforce Marketing Cloud] 属性集，其中包含您要更新的字段。

由于此目标需要访问 `[!DNL attribute-set]`，您需要允许这些实例。 例如， `Email` [!DNL attribute-set] 您需要允许，如下所示：

![SalesforceMarketing CloudUI显示具有允许权限的电子邮件属性集。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-permisions-list.png)

要限制访问级别，您还可以使用粒度权限覆盖单个访问。
![SalesforceMarketing CloudUI显示具有粒度权限的电子邮件属性集。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/sales-email-attribute-set-permission.png)

请参阅 [[!DNL Marketing Cloud Roles]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_marketing_cloud_roles.htm&amp;type=5) 和 [[!DNL Marketing Cloud Roles and Permissions]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_roles.htm&amp;type=5) 详细指导页面。

#### 收集 [!DNL Salesforce Marketing Cloud] 凭据 {#gather-credentials}

在对进行身份验证之前，请记下以下各项 [!DNL (API) Salesforce Marketing Cloud] 目标。

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| Subdomain | 参见 [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) 以了解如何从获取此值 [!DNL Salesforce Marketing Cloud] 界面。 | 如果您的 [!DNL Salesforce Marketing Cloud] 域为<br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*， <br>您需要提供 `mcq4jrssqdlyc4lph19nnqgzzs84` 作为值。 |
| 客户端ID | 请参阅 [!DNL Salesforce Marketing Cloud] [文档](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) 以了解如何从获取此值 [!DNL Salesforce Marketing Cloud] 界面。 | r23kxxxxxxxx0z05xxxxxx |
| 客户端密码 | 请参阅 [!DNL Salesforce Marketing Cloud] [文档](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) 以了解如何从获取此值 [!DNL Salesforce Marketing Cloud] 界面。 | ipxxxxxxxxxxT4xxxxxxxxxx |

{style="table-layout:auto"}

### 护栏 {#guardrails}

* Salesforce强制特定 [速率限制](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * 请参阅 [!DNL Salesforce Marketing Cloud] [文档](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) 解决您在执行期间可能会遇到的任何可能的限制并减少错误。
   * 请参阅 [[!DNL Salesforce Marketing Cloud] 参与定价](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) 页面至 *下载完整版比较表* 作为PDF，详细说明您的计划所施加的限制。
   * 此 [API概述](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) 页面详细信息附加限制。
   * 参考 [此处](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) ，以了解有关这些详细信息的页面。
* 计数 *每个对象允许的自定义字段* 根据您的Salesforce版而有所不同。
   * 请参阅 [!DNL Salesforce] [文档](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) 以获取其他指导。
   * 如果您已达到为定义的限制 *每个对象允许的自定义字段* 范围 [!DNL Salesforce Marketing Cloud] 您将需要
      * 在新属性中添加之前删除旧属性 [!DNL Salesforce Marketing Cloud].
      * 更新或删除Platform目标中的任何激活受众，这些受众使用这些较旧的属性名称作为提供的值 **[!UICONTROL 映射Id]** 期间 [受众调度](#schedule-segment-export-example) 步骤。

## 支持的身份 {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] 支持激活下表中描述的标识。 详细了解 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 联系人密钥 | [!DNL Salesforce Marketing Cloud] 联系键。 请参阅 [!DNL Salesforce Marketing Cloud] [文档](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) 如果您需要其他指导。 | 必需 |

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | <ul><li>您正在导出区段的所有成员以及所需的架构字段 *（例如：电子邮件地址、电话号码、姓氏）*，根据您的字段映射。</li><li> 中的每个区段状态 [!DNL Salesforce Marketing Cloud] 将根据 **[!UICONTROL 映射Id]** 在以下时段提供的值： [受众调度](#schedule-segment-export-example) 步骤。</li></ul> |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

范围 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**，搜索 [!DNL (API) Salesforce Marketing Cloud]. 或者，您也可以在 **[!UICONTROL 电子邮件营销]** 类别。

### 向目标进行身份验证 {#authenticate}

要向目标进行身份验证，请填写以下必填字段并选择 **[!UICONTROL 连接到目标]**. 请参阅 [收集 [!DNL Salesforce Marketing Cloud] 凭据](#gather-credentials) 部分获取任何指导。

| [!DNL (API) Salesforce Marketing Cloud] 目标 | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Subdomain]** | 您的 [!DNL Salesforce Marketing Cloud] 域前缀。 <br>例如，如果您的域是 <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*， <br> 您需要提供 `mcq4jrssqdlyc4lph19nnqgzzs84` 作为值。 |
| **[!UICONTROL 客户端ID]** | 您的 [!DNL Salesforce Marketing Cloud] `Client ID`. |
| **[!UICONTROL 客户端密码]** | 您的 [!DNL Salesforce Marketing Cloud] `Client Secret`. |

![显示如何对SalesforceMarketing Cloud进行身份验证的Platform UI屏幕快照。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

如果提供的详细信息有效，则UI将显示 **[!UICONTROL 已连接]** 状态，带有绿色复选标记，您可以继续下一步骤。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![显示目标详细信息的Platform UI屏幕快照。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
>
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [将用户档案和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

### 映射注意事项和示例 {#mapping-considerations-example}

要正确地将受众数据从Adobe Experience Platform发送到 [!DNL (API) Salesforce Marketing Cloud] 目标，您需要完成字段映射步骤。 映射包括在Platform帐户中的Experience Data Model (XDM)架构字段与其与目标目标中的相应等效字段之间创建链接。

要将XDM字段正确映射到 [!DNL (API) Salesforce Marketing Cloud] 目标字段，请执行以下步骤。

>[!IMPORTANT]
>
>* 尽管您的属性名称将根据 [!DNL Salesforce Marketing Cloud] 帐户，两者的映射 `contactKey` 和 `personalEmail.address` 是必填项。
>
>* 与集成 [!DNL Salesforce Marketing Cloud] API受Experience Platform可以从Salesforce检索的属性数量的分页限制的约束。 这意味着在 **[!UICONTROL 映射]** 步骤，目标字段架构最多可以显示2000个Salesforce帐户属性。

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您将在屏幕上看到一个新映射行。
   ![“添加新映射”的平台UI屏幕快照示例。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. 在 **[!UICONTROL 选择源字段]** 窗口中，选择 **[!UICONTROL 选择属性]** 类别并选择XDM属性或选择 **[!UICONTROL 选择身份命名空间]** 并选择身份。
1. 在 **[!UICONTROL 选择目标字段]** 窗口中，选择 **[!UICONTROL 选择身份命名空间]** 并选择身份或选择 **[!UICONTROL 选择属性]** 类别，并根据需要从显示的属性集中选择一个属性。 此 [!DNL (API) Salesforce Marketing Cloud] 目标使用 [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) 动态检索在中定义的属性及其属性集 [!DNL Salesforce Marketing Cloud]. 这些组件会显示在 **[!UICONTROL 目标字段]** 弹出窗口 [映射](#mapping-considerations-example) 在 [激活受众工作流](#activate).

   * 重复这些步骤以在XDM配置文件架构和 [!DNL (API) Salesforce Marketing Cloud]：

     | 源字段 | 目标字段 | 必需 |
     |---|---|---|
     | `IdentityMap: contactKey` | `Identity: salesforceContactKey` | `Mandatory` |
     | `xdm: person.name.firstName` | `Attribute: First Name` 所需的属性集。 | - |
     | `xdm: personalEmail.address` | `Attribute: Email Address` 所需的属性集。 | - |

   * 下面显示了使用这些映射的示例：
     ![显示Target映射的平台UI屏幕快照示例。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

完成提供目标连接的映射后，选择 **[!UICONTROL 下一个]**.

### 计划受众导出和示例 {#schedule-segment-export-example}

执行 [计划受众导出](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 步骤，您必须手动将Platform受众映射到 [属性](#prerequisites-attribute) 在 [!DNL Salesforce Marketing Cloud].

要执行此操作，请选择每个区段，然后输入属性名称 [!DNL Salesforce Marketing Cloud] 在 [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 映射Id]** 字段。 请参阅 [在中创建属性 [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) 有关在中创建属性的指导和最佳实践的部分 [!DNL Salesforce Marketing Cloud].

例如，如果您的 [!DNL Salesforce Marketing Cloud] 属性为 `salesforce_mc_segment_1`，请在 [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 映射Id]** 将受众受众从Experience Platform填充到此属性中。

示例属性来自 [!DNL Salesforce Marketing Cloud] 如下所示：
![显示属性的SalesforceMarketing CloudUI屏幕截图。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

一个示例，指示的位置 [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 映射Id]** 如下所示：
![显示计划受众导出的Platform UI屏幕快照示例。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

如所示 [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 映射Id]** 应完全匹配中指定的值 [!DNL Salesforce Marketing Cloud] **[!UICONTROL 字段名称]**.

对每个激活的Platform区段重复此部分。

根据您的用例，所有激活的受众都可以映射到相同的 [!DNL Salesforce Marketing Cloud] **[!UICONTROL 字段名称]** 或变更为其他 **[!UICONTROL 字段名称]** 在 [!DNL (API) Salesforce Marketing Cloud]. 基于上述图像的典型示例可以是。
| [!DNL (API) Salesforce Marketing Cloud] 区段名称 | [!DNL Salesforce Marketing Cloud] **[!UICONTROL 字段名称]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 映射Id]** | | — | — | — | | salesforce mc audience 1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` | | salesforce mc audience 2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

1. 选择 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]** 导航到目标列表。
   ![显示浏览目标的平台UI屏幕截图。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. 选择目标并验证状态为 **[!UICONTROL 已启用]**.
   ![显示目标数据流运行的平台UI屏幕截图。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. 切换到 **[!DNL Activation data]** 选项卡，然后选择受众名称。
   ![显示目标激活数据的平台UI屏幕截图示例。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. 监控受众摘要，并确保用户档案计数对应于在区段内创建的计数。
   ![显示区段的平台UI屏幕快照示例。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. 登录到 [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/) 网站。 然后导航到 **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** 页面，并检查是否已添加受众中的配置文件。
   ![SalesforceMarketing CloudUI屏幕截图，其中显示了“联系人”页面以及区段中使用的配置文件。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. 要检查是否已更新任何用户档案，请导航到 **[!UICONTROL 电子邮件]** 页面，并验证受众中配置文件的属性值是否已更新。 如果成功，您可以在中看到每个受众状态 [!DNL Salesforce Marketing Cloud] 已根据，从Platform更新了相应的受众状态 **[!UICONTROL 映射Id]** 中提供的值 [受众调度](#schedule-segment-export-example) 步骤。
   ![SalesforceMarketing CloudUI屏幕截图，其中显示了具有更新受众状态的选定“联系人电子邮件”页面。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关以下方面的详细信息： [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据治理概述](/help/data-governance/home.md).

## 错误和疑难解答 {#errors-and-troubleshooting}

### 将事件推送到SalesforceMarketing Cloud时遇到未知错误 {#unknown-errors}

* 在检查数据流运行时，您可能会遇到以下错误消息： `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![平台UI屏幕截图显示错误。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * 要修复此错误，请验证 **[!UICONTROL 映射Id]** 您在激活工作流中提供给的 [!DNL (API) Salesforce Marketing Cloud] 目标与您在中创建的属性的名称完全匹配 [!DNL Salesforce Marketing Cloud]. 请参阅 [在中创建属性 [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) 部分提供指导。

* 激活区段时，您可能会收到一条错误消息： `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * 要修复此错误，请联系贵机构的 [!DNL Salesforce Marketing Cloud] 要添加的客户管理员 [Experience PlatformIP地址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 敬您的 [!DNL Salesforce Marketing Cloud] 帐户的受信任IP范围。 请参阅 [!DNL Salesforce Marketing Cloud] [允许列表 Marketing Cloud中包含的IP地址](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) 文档（如果您需要其他指导）。

## 其他资源 {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [文档](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) 说明如何使用指定属性组中的指定信息更新联系人。

### Changelog {#changelog}

此部分捕获此目标连接器的功能和重要文档更新。

+++ 查看更改日志

| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2023 年 4 月 | 文档更新 | <ul><li>我们更正了 [(API) SalesforceMarketing Cloud中的先决条件](#prerequisites-destination) 部分，用于指出 [!DNL Salesforce Marketing Cloud Engagement] 是使用此目标的必需订阅。 之前错误地指出用户需要订阅Marketing Cloud的部分 **帐户** 参与以继续。</li> <li>我们在 [先决条件](#prerequisites) 对象 [角色和权限](#prerequisites-roles-permissions) 将分配给 [!DNL Salesforce] 用户才能使此目标正常工作。 (PLATIR-26299)</li></ul> |
| 2023 年 2 月 | 文档更新 | 我们更新了 [(API) SalesforceMarketing Cloud中的先决条件](#prerequisites-destination) 部分，以包括一个引用链接，调用 [!DNL Salesforce Marketing Cloud Engagement] 是使用此目标的必需订阅。 |
| 2023 年 2 月 | 功能更新 | 我们修复了目标中的错误配置导致向Salesforce发送格式错误的JSON的问题。 这导致某些用户看到大量身份激活失败。 (PLATIR-26299) |
| 2023 年 1 月 | 文档更新 | <ul><li>我们更新了 [中的先决条件 [!DNL Salesforce]](#prerequisites-destination) 部分，用于标注需要在 [!DNL Salesforce] 侧面。 此部分现在包含有关如何执行此操作的详细说明以及有关在中命名属性的最佳实践 [!DNL Salesforce]. (PLATIR-25602)</li><li>我们添加了有关如何在中为每个激活的受众使用映射ID的明确说明 [受众调度](#schedule-segment-export-example) 步骤。 (PLATIR-25602)</li></ul> |
| 2022 年 10 月 | 初始版本 | 初始目标版本和文档发布。 |

{style="table-layout:auto"}

+++
