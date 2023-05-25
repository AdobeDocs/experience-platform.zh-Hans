---
title: SalesforceMarketing Cloud帐户参与度
description: 了解如何使用SalesforceMarketing Cloud帐户参与（以前称为Pardot）目标导出您的帐户数据，并在SalesforceMarketing Cloud帐户参与中激活该数据，以满足您的业务需求。
last-substantial-update: 2023-04-14T00:00:00Z
exl-id: fca9d4f4-8717-4bfa-9992-5164ba98bea4
source-git-commit: 86feee5981aaa81d4c1f97ff8aaf303b2aacd977
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud Account Engagement] 连接

使用 [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(以前称为 [!DNL Pardot])* 捕获、跟踪、评分和评级潜在客户的目标。 您还可以通过电子邮件滴答式营销活动，以及通过培养、评分和营销活动细分来为目标市场细分和客户组设计管道所有阶段的潜在客户跟踪。

比较对象 [!DNL Salesforce Marketing Cloud Engagement] 更加面向 **B2C** 营销， [!DNL Marketing Cloud Account Engagement] 非常适合 **B2B** 涉及多个部门和决策者的用例，这些部门和决策者需要更长的销售和决策周期。 此外，您还可以与CRM保持更紧密的联系和集成，以便做出适当的销售和营销决策。 *请注意，Experience Platform还具有以下连接： [!DNL Salesforce Marketing Cloud Engagement]，您可以在以下网址查看它们： [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) 和 [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) 页数。*

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) 端点，至 **添加或更新您的潜在客户** 在新的中激活它们之后 [!DNL Marketing Cloud Account Engagement] 区段。

[!DNL Marketing Cloud Account Engagement] 使用带有授权代码的OAuth 2协议来验证 [!DNL Account Engagement] API。 向您的验证的说明 [!DNL Marketing Cloud Account Engagement] 实例位于 [向目标进行身份验证](#authenticate) 部分。

## 用例 {#use-cases}

为了帮助您更好地了解应该如何以及何时使用 [!DNL Marketing Cloud Account Engagement] 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 向营销活动的联系人发送电子邮件 {#use-case-send-emails}

一家在线平台的营销部门希望向精选的B2B潜在客户观众广播基于电子邮件的营销活动。 该平台的营销团队可以通过Adobe Experience Platform添加新潜在客户或更新现有潜在客户信息，从自己的离线数据构建区段，并将这些区段发送到 [!DNL Marketing Cloud Account Engagement]，然后可以将其用于发送营销活动电子邮件。

## 先决条件 {#prerequisites}

请参阅以下部分，了解需要在Experience Platform中设置的任何先决条件，并且 [!DNL Salesforce] ，并获取在使用 [!DNL Marketing Cloud Account Engagement] 目标。

### Experience Platform中的先决条件 {#prerequisites-in-experience-platform}

将数据激活到之前 [!DNL Marketing Cloud Account Engagement] 目标，您必须拥有 [架构](/help/xdm/schema/composition.md)， a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)、和 [区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 创建于 [!DNL Experience Platform].

### 中的先决条件 [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

请注意以下先决条件，以便将数据从Platform导出到 [!DNL Marketing Cloud Account Engagement] 帐户：

#### 您需要拥有 [!DNL Marketing Cloud Account Engagement] 帐户 {#prerequisites-account}

A [!DNL Marketing Cloud Account Engagement] 订购 [Marketing Cloud客户参与](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) 必须提供产品才能继续。

您的 [!DNL Salesforce] 帐户应具有 [!DNL Salesforce] `Account Engagement Administrator role`. 此为必需项 [创建自定义目标客户字段](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5).

最后，您的帐户还应该能够访问 [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5).

联系至 [[!DNL Salesforce] 支持](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) 或 [!DNL Salesforce] 帐户管理员（如果您没有帐户，或者帐户缺少） [!DNL Marketing Cloud Account Engagement] 订阅或 [!DNL Account Engagement Administrator role].

#### 收集 [!DNL Marketing Cloud Account Engagement] 凭据 {#gather-credentials}

在对进行身份验证之前，请记下以下各项 [!DNL Marketing Cloud Account Engagement] 目标。

| 凭据 | 描述 |
| --- | --- |
| `Username` | 您的 [!DNL Marketing Cloud Account Engagement] 帐户用户名。 |
| `Password` | 您的 [!DNL Marketing Cloud Account Engagement] 帐户密码。 |
| `Account Engagement Business Unit ID` | 要查找Account Engagement Business Unit ID，请使用 [!DNL Salesforce]. 在设置中，输入 *业务部门设置* 在“快速查找”框中。 您的帐户参与业务单元ID的开头为 `0Uv` 长度为18个字符。 如果您无法访问业务部门设置信息，请咨询 [!DNL Salesforce] 帐户管理员为您提供 `Account Engagement Business Unit ID`. 如果您需要任何额外的指南，请参阅 [[!DNL Salesforce] 身份验证](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication) 准则页面。 |

{style="table-layout:auto"}

### 护栏 {#guardrails}

请参阅 [!DNL Marketing Cloud Account Engagement] [速率限制](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) 其中详细说明了您的计划所施加的限制，并且同样适用于Experience Platform执行。

>[!IMPORTANT]
>
>如果您的 [!DNL Salesforce] 帐户管理员限制了对受信任IP范围的访问，您需要联系他们以获取 [Experience PlatformIP的](/help/destinations/catalog/streaming/ip-address-allow-list.md) 已列入允许列表 请参阅 [!DNL Salesforce] [限制对连接应用程序的受信任IP范围的访问](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 文档（如果您需要其他指导）。

## 支持的身份 {#supported-identities}

[!DNL Marketing Cloud Account Engagement] 支持激活下表中描述的标识。 详细了解 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 目标客户电子邮件地址 | 必需 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | <ul><li>您正在导出区段的所有成员以及所需的架构字段 *（例如：电子邮件地址、电话号码、姓氏）*，根据您的字段映射。</li><li> 对于Platform中的每个选定区段，将 [!DNL Salesforce Marketing Cloud Account Engagement] 区段状态通过Platform中的区段状态进行更新。</li></ul> |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据区段评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

范围 **[!UICONTROL 目标]** > **[!UICONTROL 目录]**，搜索 [!DNL Salesforce Marketing Cloud Account Engagement]. 或者，您也可以在 **[!UICONTROL 电子邮件营销]** 类别。

### 向目标进行身份验证 {#authenticate}

要对目标进行身份验证，请选择 **[!UICONTROL 连接到目标]**. 您将导航到 [!DNL Salesforce] 登录页面。 输入您的 [!DNL Marketing Cloud Account Engagement] 帐户凭据并选择 [!DNL Log In].

![显示如何对Marketing Cloud帐户参与进行身份验证的平台UI屏幕快照。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

接下来，选择 [!UICONTROL 允许] 在后续窗口中将权限授予 **Adobe Experience Platform** 应用程序访问 [!DNL Salesforce Marketing Cloud Account Engagement] 帐户。 *您只需执行此操作一次*.

![Salesforce应用程序屏幕快照确认弹出窗口，用于授予Experience Platform应用程序访问Marketing Cloud帐户参与度的权限。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

如果提供的详细信息有效，则UI会显示一条消息： *您已成功连接到SalesforceMarketing Cloud帐户参与帐户* 消息和 **[!UICONTROL 已连接]** 状态，带有绿色复选标记，您可以继续下一步骤。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。 请参阅 [收集 [!DNL Marketing Cloud Account Engagement] 凭据](#gather-credentials) 部分获取任何指导。

![显示目标详细信息的Platform UI屏幕快照。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| 字段 | 描述 |
| --- | --- |
| **[!UICONTROL 名称]** | 将来用于识别此目标的名称。 |
| **[!UICONTROL 描述]** | 可帮助您将来标识此目标的描述。 |
| **[!UICONTROL 帐户参与业务单元ID]** | 您的 [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
>
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [将配置文件和区段激活到流式区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射注意事项和示例 {#mapping-considerations-example}

要正确地将受众数据从Adobe Experience Platform发送到 [!DNL Marketing Cloud Account Engagement] 目标，您需要完成字段映射步骤。 映射包括在Platform帐户中的Experience Data Model (XDM)架构字段与其与目标目标中的相应等效字段之间创建链接。

要将XDM字段正确映射到 [!DNL Marketing Cloud Account Engagement] 目标字段，请执行以下步骤。

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您将在屏幕上看到一个新映射行。
1. 在 **[!UICONTROL 选择源字段]** 窗口中，选择 **[!UICONTROL 选择属性]** 类别并选择XDM属性或选择 **[!UICONTROL 选择身份命名空间]** 并选择身份。
1. 在 **[!UICONTROL 选择目标字段]** 窗口中，选择 **[!UICONTROL 选择身份命名空间]** 并选择身份或选择 **[!UICONTROL 选择自定义属性]** 类别并从列表中指定 [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) 从可用架构中。

   * 重复这些步骤以在XDM配置文件架构和 [!DNL Marketing Cloud Account Engagement]： |源字段 |目标字段 |必需 | | — | — | — | |`IdentityMap: Email`|`Identity: email`|是 | |`xdm: MailingAddress.city`|`xdm: city`| | |`xdm: person.name.firstName`|`Attribute: firstName`| |

   * 下面显示了具有上述映射的示例：
      ![显示Target映射的平台UI屏幕快照示例。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

完成提供目标连接的映射后，选择 **[!UICONTROL 下一个]**.

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

1. 导航到您选择的区段之一。 选择 **[!DNL Activation data]** 选项卡。此 **[!UICONTROL 映射Id]** 列显示在中生成的自定义字段的名称 [!DNL Marketing Cloud Account Engagement Prospects] 页面。
   ![显示选定区段映射ID的平台UI屏幕截图示例。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. 登录到 [[!DNL Salesforce]](https://login.salesforce.com/) 网站。 然后导航到 **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** 页面，并检查区段中的潜在客户是否已添加/更新。 或者，您也可以访问 [[!DNL Salesforce Pardot]](https://pi.pardot.com/) 并访问 **[!DNL Prospects]** 页面。
   ![显示“潜在客户”页面的Salesforce UI屏幕快照。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. 要检查目标客户是否已更新，请选择目标客户并验证自定义目标客户字段是否已使用Experience Platform区段状态进行更新。
   ![Salesforce UI屏幕截图显示了所选的目标客户页面，自定义目标客户字段更新了区段状态。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关以下方面的详细信息： [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据治理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API文档](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).
