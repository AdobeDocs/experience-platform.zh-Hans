---
title: (V2) Salesforce Marketing Cloud客户参与
description: 了解如何使用(V2) Salesforce Marketing Cloud Account Engagement（以前称为Pardot）目标导出您的配置文件数据，并通过批处理在Salesforce Marketing Cloud Account Engagement中激活这些数据，以满足您的业务需求。
badge: label="Alpha" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 21ca268d3ade99cf46b6c511360084297e8163d3
workflow-type: tm+mt
source-wordcount: '1809'
ht-degree: 3%

---

# [!DNL (V2) Salesforce Marketing Cloud Account Engagement]连接

[[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) （以前称为[!DNL Pardot]）目标允许您将您的Adobe Experience Platform配置文件数据导出到Salesforce的B2B营销自动化平台。

此集成支持在Adobe Experience Platform中的客户配置文件与[!DNL Salesforce Marketing Cloud Account Engagement]中的营销活动之间无缝同步数据。

此目标使用[[!DNL Salesforce Import API v5]](https://developer.salesforce.com/docs/marketing/pardot/guide/import-v5.html)高效地处理批处理数据导出。


>[!IMPORTANT]
> 
> 这是[Salesforce Marketing Cloud帐户参与](help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)目标的V2版本。 此版本取代了以前的目标，当前位于Alpha版本中。
> > <br>
> > 如果您当前使用的是[Salesforce Marketing Cloud帐户参与](help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)目标的早期版本，则必须在&#x200B;**2026年1月**&#x200B;之前迁移到此V2版本。 2026年1月后，Adobe将停用以前的版本，并且不再可用。


## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用[!DNL (V2) Marketing Cloud Account Engagement]目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### B2B潜在客户管理 {#use-case-lead-management}

将潜在客户数据从Adobe Experience Platform同步到[!DNL Salesforce Marketing Cloud Account Engagement]，以便全面培育和评估潜在客户。 您的营销团队可以在Experience Platform中构建丰富的受众配置文件，并将其导出到[!DNL Salesforce Marketing Cloud Account Engagement]以进行自动B2B营销活动。

### Campaign 自动化 {#use-case-campaign-automation}

您可以使用在Adobe Experience Platform中定义的受众在[!DNL Salesforce Marketing Cloud Account Engagement]中触发营销活动。 在将目标受众导出到[!DNL Salesforce]后，您可以使用这些受众来运行电子邮件营销活动，并通过培养、评分和营销活动分段来管理潜在客户。

### 轮廓扩充 {#use-case-profile-enrichment}

使用Adobe Experience Platform提供的丰富客户数据增强您的[!DNL Salesforce Marketing Cloud Account Engagement]潜在客户配置文件。 导出全面的配置文件属性，以便在[!DNL Salesforce Marketing Cloud Account Engagement]中创建更详细的目标客户记录，从而改进定位和个性化。

## 先决条件 {#prerequisites}

请参阅以下部分，了解需要在Experience Platform和[!DNL Salesforce]中设置的任何先决条件，以及在使用[!DNL (V2) Marketing Cloud Account Engagement]目标之前需要收集的信息。

### Experience Platform先决条件 {#prerequisites-in-experience-platform}

在将数据激活到[!DNL (V2) Marketing Cloud Account Engagement]目标之前，您必须在[中创建一个](/help/xdm/schema/composition.md)架构[、](../../../catalog/datasets/overview.md)数据集[和](../../../segmentation/types/overview.md)受众[!DNL Experience Platform]。

### [!DNL Salesforce Marketing Cloud Account Engagement]先决条件 {#prerequisites-destination}

请注意以下先决条件，以便将数据从Experience Platform导出到您的[!DNL Marketing Cloud Account Engagement]帐户：

#### 您需要拥有[!DNL Marketing Cloud Account Engagement]帐户 {#prerequisites-account}

必须提供订阅[!DNL Marketing Cloud Account Engagement]Marketing Cloud帐户参与[产品的](https://www.salesforce.com/products/marketing-cloud/marketing-automation/)帐户才能继续。

#### 收集[!DNL Marketing Cloud Account Engagement]凭据 {#gather-credentials}

在对[!DNL (V2) Marketing Cloud Account Engagement]目标进行身份验证之前，请记下以下项目。

| 凭据 | 描述 |
| --- | --- |
| **[!UICONTROL 帐户参与业务部门ID]** | 您的[!DNL Salesforce]帐户参与业务部门ID。 请参阅Salesforce [文档](https://help.salesforce.com/s/articleView?id=000381973&type=1)以了解如何查找该ID。 |

{style="table-layout:auto"}

## 支持的身份 {#supported-identities}

[!DNL (V2) Marketing Cloud Account Engagement]支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

如果使用其中一个标识符找到匹配项，则将使用Adobe Experience Platform中的数据更新现有的帐户参与潜在客户记录。 如果未找到匹配项，则将在“客户参与”中创建一个新的目标客户记录。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| `matchId` | 帐户参与中的目标客户ID | 这三种身份中至少需要一种 |
| `matchSalesforceId` | 潜在客户的Salesforce潜在客户/联系人ID | 这三种身份中至少需要一种 |
| `matchEmail` | 潜在客户的电子邮件地址 | 这三种身份中至少需要一种 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | <ul><li>您正在导出受众的所有成员，以及所需的架构字段&#x200B;*（例如：电子邮件地址、电话号码、姓氏）*（根据字段映射）。</li><li>此目标支持使用Salesforce Import API v5批量导出配置文件数据。</li></ul> |
| 导出频率 | **[!UICONTROL 批次]** | <ul><li>**初始导出**：映射后立即完全导出</li><li>**后续导出**：每3小时增量导出一次</li><li>此计划是固定的，无法在Alpha中自定义</li></ul> |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证到目标，请选择&#x200B;**[!UICONTROL 连接到目标]**。

![Salesforce Marketing Cloud帐户参与V2目标连接工作流](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/connect-to-destination.png "Salesforce Marketing Cloud帐户参与V2目标连接工作流")

您将被重定向到[!DNL Salesforce]登录页面。 输入您的[!DNL Marketing Cloud Account Engagement]帐户凭据并选择&#x200B;**[!UICONTROL 登录]**。

![Salesforce登录页面](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/salesforce-auth.png "Salesforce登录页面。")

接下来，选择&#x200B;**[!UICONTROL 允许]**&#x200B;授予&#x200B;**Adobe Experience Platform**&#x200B;应用访问您的[!DNL Salesforce Marketing Cloud Account Engagement]帐户的权限。 *您只需执行此操作一次*。

![Salesforce App屏幕快照确认弹出窗口，用于授予Experience Platform App访问Marketing Cloud Account Engagement的权限。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/allow-app.png)

如果提供的详细信息有效，则UI会显示一条消息： *您已成功连接到(V2) Salesforce Marketing Cloud帐户参与帐户*&#x200B;以及带有绿色复选标记的&#x200B;**[!UICONTROL 已连接]**&#x200B;状态。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 帐户参与业务部门ID]**：您的[!DNL Salesforce] `Account Engagement Business Unit ID`。
* **[!UICONTROL 帐户参与API]**：选择您要使用帐户参与API的生产端点(`https://pi.pardot.com`)还是演示端点(`https://pi.demo.pardot.com`)。
* **[!UICONTROL 帐户参与促销活动ID]**：每个[!DNL Account Engagement]潜在客户都必须与某个促销活动关联。 如果您未设置促销活动ID，那么当您的Salesforce帐户中存在默认帐户时，帐户参与度将尝试自动分配一个ID。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将受众数据激活到批处理配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md)。

### 映射注意事项和示例 {#mapping-considerations-example}

要将受众数据从Adobe Experience Platform发送到[!DNL (V2) Marketing Cloud Account Engagement]目标，您必须将体验数据模型(XDM)架构字段映射到目标中的相应字段。

有关支持的字段的完整列表，请参阅[Salesforce Prospect API v5文档](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html)。 请注意，Alpha版本中不支持[自定义字段](https://developer.salesforce.com/docs/marketing/pardot/guide/custom-field-v5.html)。

#### 支持的属性 {#supported-attributes}

Salesforce Marketing Cloud帐户参与目标支持下表中描述的目标属性。

| 属性 | 类型 | 描述 |
|---------|----------|----------|
| `salesforceId` | 字符串 | 目标客户的Salesforce ID |
| `salesforceOwnerId` | 整数 | 目标客户所有者的Salesforce用户ID |
| `salutation` | 字符串 | 潜在客户的称呼（例如，“先生”、“女士”、“博士”） |
| `score` | 整数 | 潜在客户在客户参与度中的得分 |
| `source` | 字符串 | 目标客户记录的源 |
| `state` | 字符串 | 潜在客户的省/市/自治区 |
| `territory` | 字符串 | 分配给目标客户的区域 |
| `userId` | 整数 | 与潜在客户关联的用户ID |
| `website` | 字符串 | 潜在客户的网站URL |
| `yearsInBusiness` | 字符串 | 展望已开展业务的年数 |
| `zip` | 字符串 | 潜在客户的邮政编码 |

#### 必需的映射 {#required-mappings}

在开始映射数据之前，请查看以下必需的字段映射。

| 目标字段 | 类型 | 必需 | 何时使用 |
|---|---|---|---|
| `email` | 属性 | 始终必需 | 潜在客户的电子邮件地址。 当您没有`matchId`或`matchSalesforceId`时，这是用于查找和匹配客户参与中的目标客户记录的主要标识符。<br> **注意：**&#x200B;如果帐户参与具有“允许多个潜在客户使用同一电子邮件地址”功能，则仅依赖电子邮件可能会导致模棱两可，因为同一电子邮件存在多个潜在客户。 在这种情况下，客户参与通常默认为使用最近的活动更新潜在客户。 |
| `matchId` | 身份标识 | 这三种身份中至少需要一种 | 由帐户参与为每个目标客户记录生成的唯一标识符。 当您已经拥有客户参与潜在客户ID并且希望确保将更新应用于正确的目标客户时，尤其是当多个潜在客户共享同一电子邮件地址时，请使用此选项。 |
| `matchSalesforceId` | 身份标识 | 这三种身份中至少需要一种 | Salesforce中商机或联系人的Salesforce ID。 在潜在客户已与Salesforce同步的情况下使用此项，以保持Account Engagement和Salesforce之间的数据一致性。 |
| `matchEmail` | 身份标识 | 这三种身份中至少需要一种 | 用于匹配的目标客户的电子邮件地址。 当您没有特定的帐户参与潜在客户ID或Salesforce ID时，可将此标识用作替代标识符。 注意：如果多个潜在客户共享同一电子邮件地址，则客户参与通常默认为使用最新活动更新潜在客户。 |

请按照以下步骤映射正确的字段。

1. 在&#x200B;**[!UICONTROL 映射]**&#x200B;步骤中，选择&#x200B;**[!UICONTROL 添加新映射]**。 您将在屏幕上看到一个新映射行。
1. 在&#x200B;**[!UICONTROL 选择源字段]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL 选择属性]**&#x200B;类别并选择XDM属性，或选择&#x200B;**[!UICONTROL 选择身份命名空间]**&#x200B;并选择身份。
1. 在&#x200B;**[!UICONTROL 选择目标字段]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL 选择身份命名空间]**&#x200B;并选择身份，或者选择&#x200B;**[!UICONTROL 选择自定义属性]**&#x200B;类别并从标准Account Engagement目标客户字段列表中指定。

![将XDM字段和标识映射到Salesforce Marketing Cloud帐户参与V2字段](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/mapping.png "将XDM字段和标识映射到Salesforce Marketing Cloud帐户参与V2字段的示例")

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

1. 导航到您选择的受众之一。 选择 **[!DNL Activation data]** 选项卡。**[!UICONTROL 映射ID]**&#x200B;列显示在[!DNL Marketing Cloud Account Engagement Prospects]页面中生成的自定义字段的名称。
   ![显示选定区段映射ID的Experience Platform UI屏幕快照示例。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/selected-segment-mapping-id.png)

1. 登录到[[!DNL Salesforce]](https://login.salesforce.com/)网站。 然后导航到&#x200B;**[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]**&#x200B;页面，并检查受众中的潜在客户是否已添加/更新。 或者，您也可以访问[[!DNL Account Engagement]](https://pi.pardot.com/)并访问&#x200B;**[!DNL Prospects]**页面。
   ![显示“潜在客户”页面的Salesforce UI屏幕截图。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/prospects.png)

1. 要检查潜在客户是否已更新，请选择一个潜在客户，并验证自定义潜在客户字段是否已使用Experience Platform受众状态进行更新。
   ![Salesforce UI屏幕截图显示所选目标客户页面，自定义目标客户字段已更新为受众状态。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/prospect.png)

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](/help/data-governance/home.md)。

## 其他资源 {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API文档](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html)
* [Salesforce导入API v5文档](https://developer.salesforce.com/docs/marketing/pardot/guide/import-v5.html)
* [Salesforce Prospect API v5文档](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html)