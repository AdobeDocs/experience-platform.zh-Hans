---
title: Salesforce Marketing Cloud帐户参与度
description: 了解如何使用Salesforce Marketing Cloud Account Engagement（以前称为Pardot）目标导出您的帐户数据，并在Salesforce Marketing Cloud Account Engagement中激活这些数据，以满足您的业务需求。
last-substantial-update: 2023-04-14T00:00:00Z
exl-id: fca9d4f4-8717-4bfa-9992-5164ba98bea4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 2%

---

# [!DNL Salesforce Marketing Cloud Account Engagement]连接

使用[[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *（以前称为[!DNL Pardot]）*&#x200B;目标捕获、跟踪、得分和评级潜在客户。 您还可以通过电子邮件滴答营销活动，为针对性市场受众和客户组的管道的所有阶段设计潜在客户跟踪，并通过培养、评分和营销活动分段进行潜在客户管理。

与更面向&#x200B;**B2C**&#x200B;营销的[!DNL Salesforce Marketing Cloud Engagement]相比，[!DNL Marketing Cloud Account Engagement]非常适合于涉及多个部门和决策者、需要较长的销售和决策周期的&#x200B;**B2B**&#x200B;用例。 此外，您还可以与CRM保持更紧密的联系和集成，从而做出适当的销售和营销决策。 *请注意，Experience Platform也具有[!DNL Salesforce Marketing Cloud Engagement]的连接，您可以在[[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md)和[[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md)页面上查看它们。*

此[!DNL Adobe Experience Platform] [目标](/help/destinations/home.md)利用[[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email)终结点，在新[!DNL Marketing Cloud Account Engagement]区段中激活潜在客户后&#x200B;**添加或更新潜在客户**。

[!DNL Marketing Cloud Account Engagement]使用带有授权代码的OAuth 2协议来验证[!DNL Account Engagement] API。 下面的[向目标身份验证](#authenticate)部分中进一步提供了向您的[!DNL Marketing Cloud Account Engagement]实例进行身份验证的说明。

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用[!DNL Marketing Cloud Account Engagement]目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 向营销活动的联系人发送电子邮件 {#use-case-send-emails}

在线平台的营销部门希望向精选的B2B商机受众广播基于电子邮件的营销活动。 该平台的营销团队可以通过Adobe Experience Platform添加新潜在客户或更新现有潜在客户信息，根据受众自己的离线数据构建受众，并将这些受众发送到[!DNL Marketing Cloud Account Engagement]，然后可以使用这些受众发送营销活动电子邮件。

## 先决条件 {#prerequisites}

请参阅以下部分，了解需要在Experience Platform和[!DNL Salesforce]中设置的任何先决条件，以及在使用[!DNL Marketing Cloud Account Engagement]目标之前需要收集的信息。

### Experience Platform中的先决条件 {#prerequisites-in-experience-platform}

在将数据激活到[!DNL Marketing Cloud Account Engagement]目标之前，您必须在[!DNL Experience Platform]中创建一个[架构](/help/xdm/schema/composition.md)、[数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=zh-Hans)和[区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=zh-Hans)。

### [!DNL Marketing Cloud Account Engagement]中的先决条件 {#prerequisites-destination}

请注意以下先决条件，以便将数据从Experience Platform导出到您的[!DNL Marketing Cloud Account Engagement]帐户：

#### 您需要拥有[!DNL Marketing Cloud Account Engagement]帐户 {#prerequisites-account}

必须提供订阅[Marketing Cloud帐户参与](https://www.salesforce.com/products/marketing-cloud/marketing-automation/)产品的[!DNL Marketing Cloud Account Engagement]帐户才能继续。

您的[!DNL Salesforce]帐户应具有[!DNL Salesforce] `Account Engagement Administrator role`。 这是[创建自定义目标客户字段](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5)所必需的。

最后，您的帐户还应能够访问[[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5)。

如果您没有帐户，或帐户缺少[!DNL Marketing Cloud Account Engagement]订阅或[!DNL Account Engagement Administrator role]，请联系[[!DNL Salesforce] 支持](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10)或您的[!DNL Salesforce]帐户管理员。

#### 收集[!DNL Marketing Cloud Account Engagement]凭据 {#gather-credentials}

在对[!DNL Marketing Cloud Account Engagement]目标进行身份验证之前，请记下以下项目。

| 凭据 | 描述 |
| --- | --- |
| `Username` | 您的[!DNL Marketing Cloud Account Engagement]帐户用户名。 |
| `Password` | 您的[!DNL Marketing Cloud Account Engagement]帐户密码。 |
| `Account Engagement Business Unit ID` | 若要查找帐户参与业务部门ID，请使用[!DNL Salesforce]中的设置。 在“设置”的“快速查找”框中输入&#x200B;*业务部门设置*。 您的帐户参与业务单元ID以`0Uv`开头，长度为18个字符。 如果您无法访问业务部门设置信息，请让您的[!DNL Salesforce]帐户管理员为您提供`Account Engagement Business Unit ID`。 如果您需要其他指导，请参阅[[!DNL Salesforce] 身份验证](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication)指南页面。 |

{style="table-layout:auto"}

### 护栏 {#guardrails}

请参阅[!DNL Marketing Cloud Account Engagement] [速率限制](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits)，其中详细说明了您的计划所施加的限制，并且同样适用于Experience Platform执行。

>[!IMPORTANT]
>
>如果[!DNL Salesforce]帐户管理员限制了对受信任IP范围的访问，则需要联系他们以获取[Experience Platform 列入允许列表 IP的](/help/destinations/catalog/streaming/ip-address-allow-list.md)访问权限。 如果您需要其他指导，请参阅[!DNL Salesforce] [限制对连接应用程序的受信任IP范围的访问](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5)文档。

## 支持的身份 {#supported-identities}

[!DNL Marketing Cloud Account Engagement]支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 目标客户电子邮件地址 | 必需 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | <ul><li>您正在根据字段映射导出区段的所有成员，以及所需的架构字段&#x200B;*（例如：电子邮件地址、电话号码、姓氏）*。</li><li> 对于Experience Platform中的每个选定受众，相应的[!DNL Salesforce Marketing Cloud Account Engagement]区段状态将从Experience Platform中更新为其受众状态。</li></ul> |
| 导出频率 | **[!UICONTROL 正在流式传输]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

在&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**&#x200B;中，搜索[!DNL Salesforce Marketing Cloud Account Engagement]。 或者，您可以在&#x200B;**[!UICONTROL 电子邮件营销]**&#x200B;类别下找到它。

### 验证目标 {#authenticate}

要验证到目标，请选择&#x200B;**[!UICONTROL 连接到目标]**。 您将导航到[!DNL Salesforce]登录页面。 输入您的[!DNL Marketing Cloud Account Engagement]帐户凭据并选择[!DNL Log In]。

![Experience Platform UI屏幕截图，显示如何对Marketing Cloud帐户参与进行身份验证。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

接下来，在后续窗口中选择[!UICONTROL 允许]，以授予&#x200B;**Adobe Experience Platform**&#x200B;应用访问您的[!DNL Salesforce Marketing Cloud Account Engagement]帐户的权限。 *您只需执行此操作一次*。

![Salesforce App屏幕快照确认弹出窗口，用于授予Experience Platform App访问Marketing Cloud Account Engagement的权限。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

如果提供的详细信息有效，则UI会显示消息： *您已成功连接到Salesforce Marketing Cloud帐户参与帐户*&#x200B;消息以及带有绿色复选标记的&#x200B;**[!UICONTROL 已连接]**&#x200B;状态，之后您可以继续下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。 有关任何指导，请参阅[收集 [!DNL Marketing Cloud Account Engagement] 凭据](#gather-credentials)部分。

![Experience Platform UI屏幕截图显示目标详细信息。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| 字段 | 描述 |
| --- | --- |
| **[!UICONTROL 名称]** | 将来用于识别此目标的名称。 |
| **[!UICONTROL 描述]** | 可帮助您以后识别此目标的描述。 |
| **[!UICONTROL 帐户参与业务部门ID]** | 您的[!DNL Salesforce] `Account Engagement Business Unit ID`。 |

{style="table-layout:auto"}

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 映射注意事项和示例 {#mapping-considerations-example}

要将受众数据从Adobe Experience Platform正确发送到[!DNL Marketing Cloud Account Engagement]目标，您需要完成字段映射步骤。 映射包括在Experience Platform帐户中的Experience Data Model (XDM)架构字段与其与目标中的相应等效字段之间创建链接。

要将XDM字段正确映射到[!DNL Marketing Cloud Account Engagement]目标字段，请执行以下步骤。

1. 在&#x200B;**[!UICONTROL 映射]**&#x200B;步骤中，选择&#x200B;**[!UICONTROL 添加新映射]**。 您将在屏幕上看到一个新映射行。
1. 在&#x200B;**[!UICONTROL 选择源字段]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL 选择属性]**&#x200B;类别并选择XDM属性，或选择&#x200B;**[!UICONTROL 选择身份命名空间]**&#x200B;并选择身份。
1. 在&#x200B;**[!UICONTROL 选择目标字段]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL 选择标识命名空间]**&#x200B;并选择标识，或选择&#x200B;**[!UICONTROL 选择自定义属性]**&#x200B;类别并从可用架构的[[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields)列表中指定。

   * 重复这些步骤以在XDM配置文件架构和[!DNL Marketing Cloud Account Engagement]之间添加任何映射：

     | 源字段 | 目标字段 | 必需 |
     | --- | --- | --- |
     | `IdentityMap: Email` | `Identity: email` | 是 |
     | `xdm: MailingAddress.city` | `xdm: city` | |
     | `xdm: person.name.firstName` | `Attribute: firstName` | |

   * 下面显示了具有上述映射的示例：

     ![显示Target映射的Experience Platform UI屏幕快照示例。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

完成提供目标连接的映射后，请选择&#x200B;**[!UICONTROL 下一步]**。

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

1. 导航到您选择的受众之一。 选择 **[!DNL Activation data]** 选项卡。**[!UICONTROL 映射ID]**&#x200B;列显示在[!DNL Marketing Cloud Account Engagement Prospects]页面中生成的自定义字段的名称。
   ![显示选定区段映射ID的Experience Platform UI屏幕快照示例。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. 登录到[[!DNL Salesforce]](https://login.salesforce.com/)网站。 然后导航到&#x200B;**[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]**&#x200B;页面，并检查受众中的潜在客户是否已添加/更新。 或者，您也可以访问[[!DNL Salesforce Pardot]](https://pi.pardot.com/)并访问&#x200B;**[!DNL Prospects]**&#x200B;页面。
   ![显示“潜在客户”页面的Salesforce UI屏幕截图。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. 要检查潜在客户是否已更新，请选择一个潜在客户，并验证自定义潜在客户字段是否已使用Experience Platform受众状态进行更新。
   ![Salesforce UI屏幕截图显示所选目标客户页面，自定义目标客户字段已更新为受众状态。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](/help/data-governance/home.md)。

## 其他资源 {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API文档](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html)。
