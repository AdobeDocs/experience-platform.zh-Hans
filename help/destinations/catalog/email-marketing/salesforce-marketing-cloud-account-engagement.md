---
title: SalesforceMarketing Cloud帐户参与
description: 了解如何使用SalesforceMarketing Cloud客户参与（以前称为Pardot）目标导出您的帐户数据，并在SalesforceMarketing Cloud客户参与中根据您的业务需求激活它。
last-substantial-update: 2023-04-14T00:00:00Z
source-git-commit: 65feb905bfa7d663d1d463d94af428a04dc55b01
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud Account Engagement] 连接

使用 [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(以前称为 [!DNL Pardot])* 目标以捕获、跟踪、评分和评分潜在客户。 您还可以通过电子邮件点击促销活动和商机管理，通过培养、评分和促销活动分段，为目标市场区段和客户群设计渠道所有阶段的商机跟踪。

与 [!DNL Salesforce Marketing Cloud Engagement] 更注重 **B2C** 营销， [!DNL Marketing Cloud Account Engagement] 非常适合 **B2B** 涉及多个部门和决策者的需要较长销售和决策周期的用例。 此外，您还可以与CRM保持更紧密的接近和集成，以做出适当的销售和营销决策。 *请注意，Experience Platform还具有 [!DNL Salesforce Marketing Cloud Engagement]，您可以在 [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) 和 [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) 页面。*

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) 端点，到 **添加或更新潜在客户** 在 [!DNL Marketing Cloud Account Engagement] 区段。

[!DNL Marketing Cloud Account Engagement] 使用带授权代码协议的OAuth 2对 [!DNL Account Engagement] API。 验证的说明 [!DNL Marketing Cloud Account Engagement] 实例位于下面的 [对目标进行身份验证](#authenticate) 中。

## 用例 {#use-cases}

为了帮助您更好地了解应如何以及何时应使用 [!DNL Marketing Cloud Account Engagement] 目标中，以下是Adobe Experience Platform客户可通过使用此目标解决的示例用例。

### 向营销活动的联系人发送电子邮件 {#use-case-send-emails}

在线平台的营销部门希望向策划的B2B潜在客户受众广播基于电子邮件的营销活动。 该平台的营销团队可以通过Adobe Experience Platform添加新的潜在客户或更新现有的潜在客户信息，根据他们自己的离线数据构建区段，并将这些区段发送到 [!DNL Marketing Cloud Account Engagement]，然后用于发送营销活动电子邮件。

## 先决条件 {#prerequisites}

有关您需要在Experience Platform和 [!DNL Salesforce] 以及您在使用 [!DNL Marketing Cloud Account Engagement] 目标。

### Experience Platform中的先决条件 {#prerequisites-in-experience-platform}

在将数据激活到 [!DNL Marketing Cloud Account Engagement] 目标，您必须具有 [模式](/help/xdm/schema/composition.md), a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)和 [区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 创建于 [!DNL Experience Platform].

### 先决条件 [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

请注意以下先决条件，以便将数据从Platform导出到 [!DNL Marketing Cloud Account Engagement] 帐户：

#### 你需要 [!DNL Marketing Cloud Account Engagement] 帐户 {#prerequisites-account}

A [!DNL Marketing Cloud Account Engagement] 具有订阅的帐户 [Marketing Cloud帐户参与度](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) 产品必须继续。

您的 [!DNL Salesforce] 帐户应具有 [!DNL Salesforce] `Account Engagement Administrator role`. 这是 [创建自定义潜在客户字段](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5).

最后，您的帐户还应能够访问 [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5).

联系 [[!DNL Salesforce] 支持](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) 或 [!DNL Salesforce] 帐户管理员（如果您没有帐户，或帐户缺失） [!DNL Marketing Cloud Account Engagement] 订阅或 [!DNL Account Engagement Administrator role].

#### 收集 [!DNL Marketing Cloud Account Engagement] 凭据 {#gather-credentials}

在验证到 [!DNL Marketing Cloud Account Engagement] 目标。

| 凭据 | 描述 |
| --- | --- |
| `Username` | 您的 [!DNL Marketing Cloud Account Engagement] 帐户用户名。 |
| `Password` | 您的 [!DNL Marketing Cloud Account Engagement] 帐户密码。 |
| `Account Engagement Business Unit ID` | 要查找帐户参与业务单位ID，请使用 [!DNL Salesforce]. 在设置中，输入 *业务单元设置* 中。 您的帐户参与业务单位ID以 `0Uv` 且长度为18个字符。 如果无法访问业务单元设置信息，请咨询 [!DNL Salesforce] 帐户管理员为您提供 `Account Engagement Business Unit ID`. 如果您需要任何其他指导，请参阅 [[!DNL Salesforce] 身份验证](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication) 准则页面。 |

{style="table-layout:auto"}

### 护栏 {#guardrails}

请参阅 [!DNL Marketing Cloud Account Engagement] [速率限制](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) 其中详细列出了您的计划所施加的限制，并且还适用于Experience Platform执行。

>[!IMPORTANT]
>
>如果 [!DNL Salesforce] 帐户管理员对受信任IP范围的访问权限受限，您需要联系他们以获取 [Experience PlatformIP](/help/destinations/catalog/streaming/ip-address-allow-list.md) 列入允许列表。 请参阅 [!DNL Salesforce] [限制对已连接应用程序的受信任IP范围的访问](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 文档。

## 支持的身份 {#supported-identities}

[!DNL Marketing Cloud Account Engagement] 支持激活下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 潜在客户电子邮件地址 | 必需 |

{style="table-layout:auto"}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | <ul><li>您正在导出区段的所有成员，以及所需的架构字段 *(例如：电子邮件地址、电话号码、姓氏)*，则会根据字段映射。</li><li> 对于Platform中的每个选定区段， [!DNL Salesforce Marketing Cloud Account Engagement] 区段状态会从平台中更新为其区段状态。</li></ul> |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

在 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**，搜索 [!DNL Salesforce Marketing Cloud Account Engagement]. 或者，您也可以在 **[!UICONTROL 电子邮件营销]** 类别。

### 对目标进行身份验证 {#authenticate}

要对目标进行身份验证，请选择 **[!UICONTROL 连接到目标]**. 您将导航到 [!DNL Salesforce] 登录页面。 输入 [!DNL Marketing Cloud Account Engagement] 帐户凭据并选择 [!DNL Log In].

![Platform UI屏幕截图，其中显示了如何验证Marketing Cloud帐户参与度。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

下一步，选择 [!UICONTROL 允许] ，以授予 **Adobe Experience Platform** 访问 [!DNL Salesforce Marketing Cloud Account Engagement] 帐户。 *您只需执行一次此操作*.

![Salesforce应用程序屏幕截图确认弹出窗口，用于授予Experience Platform应用程序访问Marketing Cloud帐户参与度的权限。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

如果提供的详细信息有效，UI会显示一条消息： *您已成功连接到SalesforceMarketing Cloud帐户参与帐户* 消息和 **[!UICONTROL 已连接]** 状态中显示绿色复选标记，则可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。 请参阅 [收集 [!DNL Marketing Cloud Account Engagement] 凭据](#gather-credentials) 部分。

![Platform UI屏幕截图，显示目标详细信息。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| 字段 | 描述 |
| --- | --- |
| **[!UICONTROL 名称]** | 将来用于识别此目标的名称。 |
| **[!UICONTROL 描述]** | 此描述将帮助您在将来确定此目标。 |
| **[!UICONTROL 帐户参与业务单元ID]** | 您的 [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
>
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活用户档案和区段以流式传输区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射注意事项和示例 {#mapping-considerations-example}

要将受众数据从Adobe Experience Platform正确发送到 [!DNL Marketing Cloud Account Engagement] 目标，您需要完成字段映射步骤。 映射包括在Platform帐户中的体验数据模型(XDM)架构字段与目标目标中相应的对等字段之间创建一个链接。

要将XDM字段正确映射到 [!DNL Marketing Cloud Account Engagement] 目标字段中，请按照以下步骤操作。

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您将在屏幕上看到一个新的映射行。
1. 在 **[!UICONTROL 选择源字段]** 窗口，选择 **[!UICONTROL 选择属性]** 类别，然后选择XDM属性或 **[!UICONTROL 选择身份命名空间]** 并选择一个身份。
1. 在 **[!UICONTROL 选择目标字段]** 窗口，选择 **[!UICONTROL 选择身份命名空间]** 选择身份或选择 **[!UICONTROL 选择自定义属性]** 类别和从 [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) 从可用架构中。

   * 重复这些步骤，在XDM配置文件架构和 [!DNL Marketing Cloud Account Engagement]: |源字段 |目标字段 |必填 | | — | — | — | |`IdentityMap: Email`|`Identity: email`|是 | |`xdm: MailingAddress.city`|`xdm: city`| | |`xdm: person.name.firstName`|`Attribute: firstName`| |

   * 下面显示了具有上述映射的示例：
      ![平台UI屏幕截图示例，其中显示了目标映射。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

完成为目标连接提供映射后，请选择 **[!UICONTROL 下一个]**.

## 验证数据导出 {#exported-data}

要验证您是否已正确设置目标，请执行以下步骤：

1. 导航到您选择的其中一个区段。 选择 **[!DNL Activation data]** 选项卡。的 **[!UICONTROL 映射ID]** 列显示在 [!DNL Marketing Cloud Account Engagement Prospects] 页面。
   ![Platform UI屏幕截图示例，显示选定区段的映射ID。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. 登录到 [[!DNL Salesforce]](https://login.salesforce.com/) 网站。 然后，导航到 **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** 页面，并检查区段中的潜在客户是否已添加/更新。 或者，您也可以访问 [[!DNL Salesforce Pardot]](https://pi.pardot.com/) 并访问 **[!DNL Prospects]** 页面。
   ![显示“潜在客户”页面的Salesforce UI屏幕截图。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. 要检查潜在客户是否已更新，请选择一个潜在客户，然后验证自定义潜在客户字段是否已更新为Experience Platform区段状态。
   ![Salesforce UI屏幕截图显示选定的潜在客户页面，自定义潜在客户字段将更新为区段状态。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API文档](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).