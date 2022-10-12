---
keywords: 电子邮件；电子邮件；电子邮件；电子邮件目标；Salesforce;API Salesforce Marketing Cloud目标
title: (API)SalesforceMarketing Cloud连接
description: SalesforceMarketing Cloud（以前称为ExactTarget）目标允许您导出帐户数据，并在SalesforceMarketing Cloud中激活它以满足您的业务需求。
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 2c778fe087a04261c79b9daf8579666cd0794eb4
workflow-type: tm+mt
source-wordcount: '1912'
ht-degree: 1%

---

# [!DNL (API) Salesforce Marketing Cloud] 连接

## 概述 {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/overview/) (以前称为 [!DNL ExactTarget])是一款数字营销套装，它允许您构建和自定义访客和客户的历程，以个性化其体验。

>[!IMPORTANT]
>
>请注意此连接与 [[!DNL Salesforce Marketing Cloud] 连接](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) 电子邮件营销目录部分中存在的问题。 其他SalesforceMarketing Cloud连接允许您将文件导出到指定的存储位置，而这是基于API的流连接。

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [!DNL Salesforce Marketing Cloud] [更新联系人](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API，用于在新的 [!DNL Salesforce Marketing Cloud] 区段。

[!DNL Salesforce Marketing Cloud] 使用带有客户端凭据的OAuth 2作为与 [!DNL Salesforce Marketing Cloud] API。 验证的说明 [!DNL Salesforce Marketing Cloud] 实例位于下面的 [对目标进行身份验证](#authenticate) 中。

## 用例 {#use-cases}

为了帮助您更好地了解应如何以及何时应使用 [!DNL Salesforce Marketing Cloud] 目标中，以下是Adobe Experience Platform客户可通过使用此目标解决的示例用例。

### 向营销活动的联系人发送电子邮件 {#use-case-send-emails}

家庭租赁平台的销售部门希望向目标客户受众广播营销电子邮件。 平台的营销团队可以添加新联系人/更新现有联系人 *（及其电子邮件地址）* 通过Adobe Experience Platform，根据自己的离线数据构建区段，并将这些区段发送到 [!DNL Salesforce Marketing Cloud]，然后用于发送营销活动电子邮件。

## 先决条件 {#prerequisites}

### Experience Platform中的先决条件 {#prerequisites-in-experience-platform}

在将数据激活到 [!DNL Salesforce Marketing Cloud] 目标，您必须具有 [模式](/help/xdm/schema/composition.md), a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)和 [区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 创建于 [!DNL Experience Platform].

### 先决条件 [!DNL Salesforce Marketing Cloud] {#prerequisites-destination}

请注意以下先决条件，以便将数据从Platform导出到 [!DNL Salesforce Marketing Cloud] 帐户：

#### 你需要 [!DNL Salesforce Marketing Cloud] 帐户 {#prerequisites-account}

联系您的 [!DNL Salesforce Account Executive] 订购 [!DNL Salesforce Marketing Cloud Account Engagement] 产品（如果您尚未提供）。

#### 在中创建自定义字段 [!DNL Salesforce Marketing Cloud] {#prerequisites-custom-field}

您必须创建类型的自定义属性 `Text Area Long`，该Experience Platform将用于更新 [!DNL Salesforce Marketing Cloud]. 在将区段激活到目标的工作流中，通过 **[区段计划](#schedule-segment-export-example)** 步骤中，您将使用自定义属性作为 **[!UICONTROL 映射ID]** 为您激活的每个区段。

请参阅 [!DNL Salesforce Marketing Cloud] 文档 [创建自定义字段](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) 如果您需要其他指导，请执行以下操作。

>[!IMPORTANT]
>
> 确保在 `Email Demographics` 属性集 [!DNL Salesforce Marketing Cloud] 帐户。

请参阅Adobe Experience Platform文档，以了解 [区段成员资格详细信息架构字段组](/help/xdm/field-groups/profile/segmentation.md) 如果您需要有关区段状态的指导，请执行以下操作：

#### 收集Salesforce凭据 {#gather-credentials}

在验证到 [!DNL Salesforce Marketing Cloud] 目标。

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| <ul><li>[!DNL Salesforce Marketing Cloud] 前缀</li></ul> | 请参阅 [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) 以获取其他指导。 | <ul><li>如果您的域如下所示，则需要突出显示的值。<br> <i>`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com</i></li></ul> |
| <ul><li>客户端ID</li><li>客户端密钥</li></ul> | 请参阅 [!DNL Salesforce Marketing Cloud] [文档](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) 如果您需要其他指导，请执行以下操作。 | <ul><li>r23kxxxxxxxxx0z05xxxxx</li><li>ipxxxxxxxxxxxxT4xxxxxxxxxxxx</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 限制 [!DNL Salesforce Marketing Cloud] {#limits}

* Salesforce强加了 [速率限制](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * 请参阅 [!DNL Salesforce Marketing Cloud] [文档](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) 以解决您在执行过程中可能遇到的任何可能限制并减少错误。
   * 请参阅 [[!DNL Salesforce Marketing Cloud] 参与度定价](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) 页面 *下载完整版比较图* 作为pdf，其中详细列出了您的计划所施加的限制。
   * 的 [API概述](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) 页面详细信息其他限制。
   * 请参阅 [此处](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) ，以查看可以整理这些详细信息的页面。
* 计数 *每个对象允许的自定义字段* 会因您的Salesforce版本而异。
   * 请参阅 [!DNL Salesforce] [文档](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) 以获取其他指导。
   * 如果您已达到 *每个对象允许的自定义字段* within [!DNL Salesforce Marketing Cloud] 您需要
      * 在中添加新的自定义字段之前，请删除旧的自定义字段 [!DNL Salesforce Marketing Cloud].
      * 更新或删除平台中使用这些旧版自定义字段名称作为 **[!UICONTROL 映射ID]** 在 [区段计划](#schedule-segment-export-example) 中。

## 支持的身份 {#supported-identities}

[!DNL Salesforce Marketing Cloud] 支持激活下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] 联系密钥。 请参阅 [!DNL Salesforce Marketing Cloud] [文档](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) 如果您需要其他指导，请执行以下操作。 | 必需 |

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | <ul><li>您正在导出区段的所有成员，以及所需的架构字段 *(例如：电子邮件地址、电话号码、姓氏)*，则会根据字段映射。</li><li> 每个区段状态位于 [!DNL Salesforce Marketing Cloud] 会根据 **[!UICONTROL 映射ID]** 值 [区段计划](#schedule-segment-export-example) 中。</li></ul> |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

在 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**，搜索 [!DNL (API) Salesforce Marketing Cloud]. 或者，您也可以在 **[!UICONTROL 电子邮件营销]** 类别。

### 对目标进行身份验证 {#authenticate}

要对目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.
![Platform UI屏幕截图，其中显示了如何对SalesforceMarketing Cloud进行身份验证。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

* **[!UICONTROL 子域]**:您的 [!DNL Salesforce Marketing Cloud] 域前缀。 例如，如果您的域为 *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*，则需要突出显示的值。
* **[!UICONTROL 客户端ID]**:您的 [!DNL Salesforce Marketing Cloud] 客户端ID。
* **[!UICONTROL 客户端密钥]**:您的 [!DNL Salesforce Marketing Cloud] 客户端密钥。

如果提供的详细信息有效，UI会显示 **[!UICONTROL 已连接]** 状态中显示绿色复选标记，则可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![Platform UI屏幕截图，显示目标详细信息。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
>
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活用户档案和区段以流式传输区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射注意事项和示例 {#mapping-considerations-example}

要将受众数据从Adobe Experience Platform正确发送到 [!DNL Salesforce Marketing Cloud] 目标，您需要完成字段映射步骤。 映射包括在Platform帐户中的体验数据模型(XDM)架构字段与目标目标中相应的对等字段之间创建一个链接。 要将XDM字段正确映射到 [!DNL Salesforce Marketing Cloud] 目标字段中，请按照以下步骤操作。

>[!IMPORTANT]
>
>尽管属性名称与 [!DNL Salesforce Marketing Cloud] 帐户，这两个帐户的映射 `contactKey` 和 `personalEmail.address` 为必填项。

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您将在屏幕上看到一个新的映射行。
   ![Platform UI中“添加新映射”的屏幕截图示例。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)

1. 在 **[!UICONTROL 选择源字段]** 窗口，选择 **[!UICONTROL 选择属性]** 类别和选择 `contactKey`.
   ![Platform UI源映射的屏幕截图示例。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/source-mapping.png)

1. 在 **[!UICONTROL 选择目标字段]** 窗口，选择要将源字段映射到的目标字段类型。
   * **[!UICONTROL 选择身份命名空间]**:选择此选项可将源字段从列表中映射到标识命名空间。
      ![Platform UI屏幕截图，显示SalesforceContactKey的Target映射。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping.png)

   * 在XDM配置文件架构和 [!DNL Salesforce Marketing Cloud] 实例： |XDM配置文件架构|[!DNL Salesforce Marketing Cloud] Instance|必填| |—|—|—| |`contactKey`|`salesforceContactKey`|是 |

   * **[!UICONTROL 选择自定义属性]**:选择此选项可将源字段映射到您在中定义的自定义属性 **[!UICONTROL 属性名称]** 字段。 请参阅 [!DNL Salesforce Marketing Cloud] [文档](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) ，以查看支持的属性列表。 另请注意，目标使用 [Salesforce搜索属性集定义REST API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) 用于检索在Salesforce中为您的联系人定义且特定于您帐户的属性。
      ![显示Target映射的平台UI屏幕截图。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping-custom.png)

   * 例如，根据要更新的值，在XDM配置文件架构和 [!DNL Salesforce Marketing Cloud] 实例： |XDM配置文件架构|[!DNL Salesforce Marketing Cloud] 实例| |—|—| |`person.name.firstName`|`Email Demographics.First Name`| |`personalEmail.address`|`Email Addresses.Email Address`|

   * 使用这些映射的示例如下所示：
      ![平台UI屏幕截图示例，其中显示了目标映射。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

### 计划区段导出和示例 {#schedule-segment-export-example}

执行 [计划区段导出](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 步骤中，您必须手动将平台区段映射到 [自定义属性](#prerequisites-custom-field) 在Salesforce中。

为此，请选择每个区段，然后在 **[!UICONTROL 映射ID]** 字段。

>[!IMPORTANT]
>
>用于映射ID的值应与Salesforce中在“电子邮件人口统计”属性集下创建的自定义属性的名称完全匹配。

示例如下所示：
![Platform UI屏幕截图示例显示了计划区段导出。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

## 验证数据导出 {#exported-data}

要验证您是否已正确设置目标，请执行以下步骤：

1. 选择 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]** 导航到目标列表。
   ![显示浏览目标的平台UI屏幕截图。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. 选择目标并验证状态是否为 **[!UICONTROL 已启用]**.
   ![Platform UI屏幕截图，其中显示了目标数据流运行。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. 切换到 **[!DNL Activation data]** ，然后选择区段名称。
   ![Platform UI屏幕截图示例，其中显示了目标激活数据。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. 监控区段摘要，并确保配置文件计数与区段内创建的计数相对应。
   ![平台UI屏幕截图示例，其中显示了区段。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. 登录到 [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/) 网站。 然后，导航到 **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** 页面，并检查是否已添加区段中的用户档案。
   ![SalesforceMarketing CloudUI屏幕截图，显示“联系人”页面以及区段中使用的配置文件。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. 要检查是否更新了任何用户档案，请导航至 **[!UICONTROL 电子邮件]** 页面，并验证区段中配置文件的属性值是否已更新。 如果成功，您可以在 [!DNL Salesforce Marketing Cloud] 更新时，会根据 **[!UICONTROL 映射ID]** 值 [区段计划](#schedule-segment-export-example) 中。
   ![SalesforceMarketing CloudUI屏幕截图显示了具有更新区段状态的选定“联系人电子邮件”页面。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](/help/data-governance/home.md).

## 错误和疑难解答 {#errors-and-troubleshooting}

### 将事件推送到SalesforceMarketing Cloud时遇到未知错误 {#unknown-errors}

检查数据流运行时，您可能会遇到以下错误消息： `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

![显示错误的平台UI屏幕截图。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

要修复此错误，请验证 **[!UICONTROL 映射ID]** 您在 [!DNL Salesforce Marketing Cloud] ，且该区段在 [!DNL Salesforce Marketing Cloud].

## 其他资源 {#additional-resources}

* [[!DNL Salesforce Marketing Cloud] API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
