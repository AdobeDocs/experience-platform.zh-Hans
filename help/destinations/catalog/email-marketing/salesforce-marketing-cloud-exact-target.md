---
keywords: 电子邮件；电子邮件；电子邮件；电子邮件目标；Salesforce;API Salesforce Marketing Cloud目标
title: (API)SalesforceMarketing Cloud连接
description: SalesforceMarketing Cloud（以前称为ExactTarget）目标允许您导出帐户数据，并在SalesforceMarketing Cloud中激活它以满足您的业务需求。
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 017ccadc1689663059aa1214c5440549b509e81b
workflow-type: tm+mt
source-wordcount: '2619'
ht-degree: 1%

---

# [!DNL (API) Salesforce Marketing Cloud] 连接

## 概述 {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/overview/) (以前称为 [!DNL ExactTarget])是一款数字营销套装，它允许您构建和自定义访客和客户的历程，以个性化其体验。

>[!IMPORTANT]
>
>请注意此连接与 [[!DNL Salesforce Marketing Cloud] 连接](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) 电子邮件营销目录部分中存在的问题。 其他SalesforceMarketing Cloud连接允许您将文件导出到指定的存储位置，而这是基于API的流连接。

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [!DNL Salesforce Marketing Cloud] [更新联系人](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API，它允许您 **添加联系人和更新联系人数据** 在新的 [!DNL Salesforce Marketing Cloud] 区段。

[!DNL Salesforce Marketing Cloud] 使用带有客户端凭据的OAuth 2作为与 [!DNL Salesforce Marketing Cloud] API。 验证的说明 [!DNL Salesforce Marketing Cloud] 实例位于下面的 [对目标进行身份验证](#authenticate) 中。

## 用例 {#use-cases}

为了帮助您更好地了解应如何以及何时应使用 [!DNL (API) Salesforce Marketing Cloud] 目标中，以下是Adobe Experience Platform客户可通过使用此目标解决的示例用例。

### 向营销活动的联系人发送电子邮件 {#use-case-send-emails}

家庭租赁平台的销售部门希望向目标客户受众广播营销电子邮件。 平台的营销团队可以添加新联系人/更新现有联系人 *（及其电子邮件地址）* 通过Adobe Experience Platform，根据自己的离线数据构建区段，并将这些区段发送到 [!DNL Salesforce Marketing Cloud]，然后用于发送营销活动电子邮件。

## 先决条件 {#prerequisites}

### Experience Platform中的先决条件 {#prerequisites-in-experience-platform}

在将数据激活到 [!DNL (API) Salesforce Marketing Cloud] 目标，您必须具有 [模式](/help/xdm/schema/composition.md), a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)和 [区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 创建于 [!DNL Experience Platform].

### 先决条件 [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

请注意以下先决条件，以便将数据从Platform导出到 [!DNL Salesforce Marketing Cloud] 帐户：

#### 你需要 [!DNL Salesforce Marketing Cloud] 帐户 {#prerequisites-account}

A [!DNL Salesforce Marketing Cloud] 具有订阅的帐户 [Marketing Cloud帐户参与度](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) 产品必须继续。

联系 [[!DNL Salesforce] 支持](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) 如果您没有 [!DNL Salesforce Marketing Cloud] 帐户或帐户缺失 [!DNL Marketing Cloud Account Engagement] 产品订阅。

#### 在中创建属性 [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

将区段激活到 [!DNL (API) Salesforce Marketing Cloud] 目标，则必须在 **[!UICONTROL 映射ID]** 字段中 **[区段计划](#schedule-segment-export-example)** 中。

[!DNL Salesforce] 需要此值才能正确读取和解释来自Experience Platform的区段，并在 [!DNL Salesforce Marketing Cloud]. 请参阅Experience Platform文档，以了解 [区段成员资格详细信息架构字段组](/help/xdm/field-groups/profile/segmentation.md) 如果您需要有关区段状态的指导，请执行以下操作：

对于从Platform激活到 [!DNL Salesforce Marketing Cloud]，则需要创建类型的属性 `Text` within [!DNL Salesforce]. 使用 [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder] 创建属性。 属性字段名称用于 [!DNL (API) Salesforce Marketing Cloud] 目标字段，应在下创建 `[!DNL Email Demographics system attribute-set]`. 您可以根据业务要求定义最多4000个字符的字段字符。 请参阅 [!DNL Salesforce Marketing Cloud] [数据扩展数据类型](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) 文档页面，以了解有关属性类型的其他信息。

请参阅 [!DNL Salesforce Marketing Cloud] 文档 [创建属性](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) 如果您需要有关创建属性的指导，请参阅。

中数据设计器屏幕的示例 [!DNL Salesforce Marketing Cloud]，您将在其中添加属性如下所示：
![SalesforceMarketing CloudUI数据设计器。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

查看 [!DNL Salesforce Marketing Cloud] [!DNL Email Demographics] 属性集如下所示：
![SalesforceMarketing CloudUI电子邮件人口统计属性集。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demograhics-fields.png)

的 [!DNL (API) Salesforce Marketing Cloud] 目标使用 [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) 动态检索属性及其在 [!DNL Salesforce Marketing Cloud].

这些值显示在 **[!UICONTROL 目标字段]** 选择窗口 [映射](#mapping-considerations-example) （在工作流中） [将区段激活到目标](#activate). 请注意，仅映射 [!DNL Salesforce Marketing Cloud] `[!DNL Email Demographics]` 支持属性集。

>[!IMPORTANT]
>
>在 [!DNL Salesforce Marketing Cloud]，则必须使用 **[!UICONTROL 字段名称]** 与 **[!UICONTROL 映射ID]** 每个激活的平台区段。 例如，下面的屏幕截图显示了一个名为 `salesforce_mc_segment_1`. 在将区段激活到此目标时，添加 `salesforce_mc_segment_1` as **[!UICONTROL 映射ID]** 将Experience Platform中的区段受众填充到此属性中。

中属性创建的示例 [!DNL Salesforce Marketing Cloud]，如下所示：
![SalesforceMarketing CloudUI屏幕截图，显示属性。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
>* 创建属性时，请勿在字段名称中包含空格字符。 请改用下划线 `(_)` 字符。
>* 区分用于平台区段的属性和 [!DNL Salesforce Marketing Cloud]，则可以为用于Adobe区段的属性包含可识别的前缀或后缀。 例如， `test_segment`，使用 `Adobe_test_segment` 或 `test_segment_Adobe`.
>* 如果您已在中创建其他属性 [!DNL Salesforce Marketing Cloud]，则可以使用与平台区段相同的名称，以便在 [!DNL Salesforce Marketing Cloud].


#### 收集 [!DNL Salesforce Marketing Cloud] 凭据 {#gather-credentials}

在验证到 [!DNL (API) Salesforce Marketing Cloud] 目标。

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| Subdomain | 请参阅 [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) 了解如何从 [!DNL Salesforce Marketing Cloud] 界面。 | 如果 [!DNL Salesforce Marketing Cloud] 域<br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br>您需要提供 `mcq4jrssqdlyc4lph19nnqgzzs84` 作为值。 |
| 客户端ID | 请参阅 [!DNL Salesforce Marketing Cloud] [文档](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) 了解如何从 [!DNL Salesforce Marketing Cloud] 界面。 | r23kxxxxxxxx0z05xxxxxx |
| 客户端密钥 | 请参阅 [!DNL Salesforce Marketing Cloud] [文档](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) 了解如何从 [!DNL Salesforce Marketing Cloud] 界面。 | ipxxxxxxxxxxT4xxxxxxxxxx |

{style="table-layout:auto"}

### 护栏 {#guardrails}

* Salesforce强加了 [速率限制](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * 请参阅 [!DNL Salesforce Marketing Cloud] [文档](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) 以解决您在执行过程中可能遇到的任何可能限制并减少错误。
   * 请参阅 [[!DNL Salesforce Marketing Cloud] 参与度定价](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) 页面 *下载完整版比较图* 作为pdf，其中详细列出了您的计划所施加的限制。
   * 的 [API概述](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) 页面详细信息其他限制。
   * 请参阅 [此处](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) ，以查看可以整理这些详细信息的页面。
* 计数 *每个对象允许的自定义字段* 会因您的Salesforce版本而异。
   * 请参阅 [!DNL Salesforce] [文档](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) 以获取其他指导。
   * 如果您已达到 *每个对象允许的自定义字段* within [!DNL Salesforce Marketing Cloud] 您需要
      * 在中添加新属性之前，请删除旧属性 [!DNL Salesforce Marketing Cloud].
      * 更新或删除Platform目标中任何已激活的区段，这些区段会将这些旧属性名称用作 **[!UICONTROL 映射ID]** 在 [区段计划](#schedule-segment-export-example) 中。

## 支持的身份 {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] 支持激活下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] 联系密钥。 请参阅 [!DNL Salesforce Marketing Cloud] [文档](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) 如果您需要其他指导，请执行以下操作。 | 必需 |

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | <ul><li>您正在导出区段的所有成员，以及所需的架构字段 *(例如：电子邮件地址、电话号码、姓氏)*，则会根据字段映射。</li><li> 每个区段状态位于 [!DNL Salesforce Marketing Cloud] 会根据 **[!UICONTROL 映射ID]** 值 [区段计划](#schedule-segment-export-example) 中。</li></ul> |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

在 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**，搜索 [!DNL (API) Salesforce Marketing Cloud]. 或者，您也可以在 **[!UICONTROL 电子邮件营销]** 类别。

### 对目标进行身份验证 {#authenticate}

要对目标进行身份验证，请填写以下必填字段并选择 **[!UICONTROL 连接到目标]**. 请参阅 [收集 [!DNL Salesforce Marketing Cloud] 凭据](#gather-credentials) 部分。

| [!DNL (API) Salesforce Marketing Cloud] 目标 | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Subdomain]** | 您的 [!DNL Salesforce Marketing Cloud] 域前缀。 <br>例如，如果您的域为 <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br> 您需要提供 `mcq4jrssqdlyc4lph19nnqgzzs84` 作为值。 |
| **[!UICONTROL 客户端ID]** | 您的 [!DNL Salesforce Marketing Cloud] `Client ID`. |
| **[!UICONTROL 客户端密钥]** | 您的 [!DNL Salesforce Marketing Cloud] `Client Secret`. |

![Platform UI屏幕截图，其中显示了如何对SalesforceMarketing Cloud进行身份验证。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

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

要将受众数据从Adobe Experience Platform正确发送到 [!DNL (API) Salesforce Marketing Cloud] 目标，您需要完成字段映射步骤。 映射包括在Platform帐户中的体验数据模型(XDM)架构字段与目标目标中相应的对等字段之间创建一个链接。

要将XDM字段正确映射到 [!DNL (API) Salesforce Marketing Cloud] 目标字段中，请按照以下步骤操作。

>[!IMPORTANT]
>
>尽管属性名称与 [!DNL Salesforce Marketing Cloud] 帐户，这两个帐户的映射 `contactKey` 和 `personalEmail.address` 为必填项。 在映射属性时，仅映射Experience Platform中的属性 `Email Demographics` attribute-set应在target字段中使用。

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您将在屏幕上看到一个新的映射行。
   ![Platform UI中“添加新映射”的屏幕截图示例。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. 在 **[!UICONTROL 选择源字段]** 窗口，选择 **[!UICONTROL 选择属性]** 类别，然后选择XDM属性或 **[!UICONTROL 选择身份命名空间]** 并选择一个身份。
1. 在 **[!UICONTROL 选择目标字段]** 窗口，选择 **[!UICONTROL 选择身份命名空间]** 选择身份或选择 **[!UICONTROL 选择自定义属性]** 类别，然后从 `Email Demographics` 属性。 的 [!DNL (API) Salesforce Marketing Cloud] 目标使用 [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) 动态检索属性及其在 [!DNL Salesforce Marketing Cloud]. 这些值显示在 **[!UICONTROL 目标字段]** 弹出窗口 [映射](#mapping-considerations-example) 在 [将区段激活到工作流](#activate). 请注意，仅映射 [!DNL Salesforce Marketing Cloud] `[!DNL Email Demographics]` 支持属性集。

   * 重复这些步骤，在XDM配置文件架构和 [!DNL (API) Salesforce Marketing Cloud]: |源字段|目标字段|必填| |—|—|—| |`IdentityMap: contactKey`|`Identity: salesforceContactKey`| `Mandatory` |\
      |`xdm: person.name.firstName`|`Attribute: Email Demographics.First Name`| - |
|`xdm: personalEmail.address`|`Attribute: Email Addresses.Email Address`| - |

   * 使用这些映射的示例如下所示：
      ![平台UI屏幕截图示例，其中显示了目标映射。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

完成为目标连接提供映射后，请选择 **[!UICONTROL 下一个]**.

### 计划区段导出和示例 {#schedule-segment-export-example}

执行 [计划区段导出](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 步骤中，您必须手动将平台区段映射到 [属性](#prerequisites-attribute) in [!DNL Salesforce Marketing Cloud].

要实现此目的，请选择每个区段，然后输入 [!DNL Salesforce Marketing Cloud] 在 [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 映射ID]** 字段。 请参阅 [在中创建属性 [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) 部分，用于在 [!DNL Salesforce Marketing Cloud].

例如，如果 [!DNL Salesforce Marketing Cloud] 属性为 `salesforce_mc_segment_1`，请在 [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 映射ID]** 将Experience Platform中的区段受众填充到此属性中。

示例属性来自 [!DNL Salesforce Marketing Cloud] 如下所示：
![SalesforceMarketing CloudUI屏幕截图，显示属性。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

指示 [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 映射ID]** 如下所示：
![Platform UI屏幕截图示例显示了计划区段导出。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

如所示， [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 映射ID]** 应与 [!DNL Salesforce Marketing Cloud] **[!UICONTROL 字段名称]**.

对每个激活的平台区段重复此部分。

根据您的用例，所有激活的区段都可以映射到相同的 [!DNL Salesforce Marketing Cloud] **[!UICONTROL 字段名称]** 或 **[!UICONTROL 字段名称]** in [!DNL (API) Salesforce Marketing Cloud]. 基于上面所示图像的典型示例可能是。
| [!DNL (API) Salesforce Marketing Cloud] 区段名称 | [!DNL Salesforce Marketing Cloud] **[!UICONTROL 字段名称]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL 映射ID]** | | — | — | — | | salesforce mc区段1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` | | salesforce mc区段2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

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

* 检查数据流运行时，您可能会遇到以下错误消息： `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

   ![显示错误的平台UI屏幕截图。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * 要修复此错误，请验证 **[!UICONTROL 映射ID]** 激活工作流中提供的 [!DNL (API) Salesforce Marketing Cloud] 目标与您在中创建的属性的名称完全匹配 [!DNL Salesforce Marketing Cloud]. 请参阅 [在中创建属性 [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) 部分。

* 激活区段时，可能会收到一条错误消息： `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * 要修复此错误，请与 [!DNL Salesforce Marketing Cloud] 帐户管理员添加 [Experience PlatformIP地址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 至 [!DNL Salesforce Marketing Cloud] 帐户的受信任IP范围。 请参阅 [!DNL Salesforce Marketing Cloud] [要包含在中允许列表的IP地址Marketing Cloud](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) 文档。

## 其他资源 {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [文档](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) 说明如何使用指定属性组中的指定信息更新联系人。

### Changelog {#changelog}

本节将捕获对此目标连接器所做的功能和重要文档更新。

+++ 查看changelog

| 发布月份 | 更新类型 | 描述 |
|---|---|---|
| 2023 年 2 月 | 文档更新 | 我们更新了 [(API)SalesforceMarketing Cloud中的先决条件](#prerequisites-destination) 包含引用链接的部分，该引用链接调用 [!DNL Salesforce Marketing Cloud Account Engagement] 是使用此目标的强制订阅。 |
| 2023 年 2 月 | 功能更新 | 我们修复了目标中配置不正确导致将格式错误的JSON发送到Salesforce的问题。 这会导致某些用户在激活时看到大量身份失败。 (PLATIR-26299) |
| 2023 年 1 月 | 文档更新 | <ul><li>我们更新了 [先决条件 [!DNL Salesforce]](#prerequisites-destination) 调用需要在 [!DNL Salesforce] 侧。 此部分现在包含有关如何执行此操作的详细说明以及有关在 [!DNL Salesforce]. (PLATIR-25602)</li><li>我们为 [区段计划](#schedule-segment-export-example) 中。 (PLATIR-25602)</li></ul> |
| 2022 年 10 月 | 初始版本 | 初始目标版本和文档发布。 |

{style="table-layout:auto"}

+++