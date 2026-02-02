---
title: Oracle Eloqua (V2) Source概述
description: 了解如何将Oracle Eloqua连接到Adobe Experience Platform。
last-substantial-update: 2025-02-02T00:00:00Z
source-git-commit: 4d47eae91711596677335b03568add9f6fbade74
workflow-type: tm+mt
source-wordcount: '1824'
ht-degree: 2%

---

# [!DNL Oracle Eloqua] (V2)源概述

>[!IMPORTANT]
>
>原始[[!DNL Oracle Eloqua] (V1)](oracle-eloqua.md)源自2026年1月起已被弃用。 此已弃用的源没有迁移可用，您必须使用新的[!DNL Oracle Eloqua] (V2)源重新实施数据。

[!DNL Oracle Eloqua]是一个功能强大的企业级营销自动化平台，旨在帮助主要在B2B领域的组织自动化并个性化管理潜在客户和编排买家历程的复杂流程。 它充当一个中心枢纽，营销团队可以在其中定义、部署和衡量多个数字渠道中的复杂促销活动，确保潜在客户在最参与的确切时刻获得正确的内容。 支持通过[!DNL Eloqua]进行摄取的对象是&#x200B;**联系人**、**帐户**、**营销活动**&#x200B;和&#x200B;**活动**。 完成初始摄取后，将使用计划的增量过程导入任何更改的数据。

您可以使用[!DNL Eloqua]源将您的[!DNL Eloqua]帐户连接到Adobe Experience Platform。 请阅读以下文档以了解如何入门。

## 用例示例 {#use-case-examples}

下表概述了[!DNL Eloqua] (V2)与Adobe Experience Platform集成支持的营销对象。 对于每个对象，您将找到描述以及示例用例，以说明将[!DNL Eloqua]数据与Real-Time CDP集成如何可以提高营销效率和活动结果。

| 对象 | 描述 | 用例示例 |
| --- | --- | --- |
| 联系人 | 将联系人数据（如姓名、电子邮件、电话号码、职务）摄取到Real-Time CDP以创建详细的统一客户档案，整合与每个联系人的所有交互和参与。 | **营销活动优化：**&#x200B;通过集成来自[!DNL Eloqua]的联系数据，您的营销团队可以根据电子邮件打开、表单提交和事件注册等近期活动识别高优先级的潜在客户。 Real-Time CDP可全方位查看每个联系人在电子邮件、网站和其他营销接触点中的行为，允许营销团队定制活动并优化消息传送，以提高参与度和转化率。 |
| 帐户 | 摄取帐户级别的数据（如公司名称、行业、公司规模、收入、位置）以在Real-Time CDP中构建基于帐户的营销(ABM)策略，并使您的团队能够通过相关消息传送来定位和接触适当的组织。 | **ABM营销活动：**&#x200B;集成来自[!DNL Eloqua]的帐户数据有助于生成针对性的ABM营销活动。 例如，一家软件公司可以利用客户数据对金融行业公司的决策者进行细分并向他们发送定制电子邮件促销活动，以推广针对其行业的新解决方案。 |
| 营销活动 | 将促销活动数据（如促销活动名称、类型、目标、打开率等性能量度、CTR）摄取到Real-Time CDP中以跨多个渠道跟踪和优化促销活动性能。 使用此数据衡量ROI并完善您的策略。 | **跨渠道归因：**&#x200B;如果[!DNL Eloqua]将促销活动数据发送到Real-Time CDP，则营销团队可以查看跨各种渠道（电子邮件、社交媒体、广告等）的促销活动效果，将转化归因于正确的接触点，并根据该insight优化未来策略。 |
| 活动 | 摄取活动数据（例如电子邮件打开、点击、网站访问、表单提交、网络研讨会出席情况）以跟踪不同渠道的实时行为和联系人，从而创造实时个性化参与的机会。 | **实时培养：**&#x200B;通过集成来自[!DNL Eloqua]的活动数据，当联系人参与内容（如下载白皮书或单击电子邮件链接）时，Real-Time CDP可以触发发送给销售团队的个性化电子邮件或通知，以便及时跟进和改善转化机会。 |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

请阅读以下各节，了解在将源连接到Experience Platform之前必须完成的先决条件设置。

### 设置应用程序以进行身份验证

请按照以下步骤了解如何设置[!DNL Eloqua]帐户并使用基本身份验证连接到Experience Platform。

若要开始，请以管理员（或有权创建用户、安全组和应用的用户）身份登录到您的[!DNL Eloqua]实例。

![我的Eloqua仪表板。](../../images/tutorials/create/eloqua/admin.png)

导航到&#x200B;**设置** > **平台扩展** > **应用程序云开发人员** > **创建应用程序**。 提供应用程序的详细信息，包括其名称、描述、图标和OAuth回调URL。 完成后选择&#x200B;**保存**。

![Eloqua仪表板中的“应用程序开发人员”面板和“创建应用程序”按钮。](../../images/tutorials/create/eloqua/create-app.png)

| 属性 | 描述 |
| --- | --- |
| 名称 | 应用程序的名称。 |
| 描述 | 应用程序的简短说明。 |
| 图标 | 图标的URL。 |
| OAuth回调URL | 安装应用程序并使用[!DNL Eloqua]进行身份验证后应重定向到的URL。 |

![Eloqua中的“创建应用程序”窗口。](../../images/tutorials/create/eloqua/new-app.png)

创建应用程序后，导航到[!DNL Authentication to Eloqua]并从新创建的应用程序中检索&#x200B;**客户端ID**&#x200B;和&#x200B;**客户端密钥**。 这些值将在稍后连接到Experience Platform时使用。

![Eloqua中的客户端ID和客户端密钥。](../../images/tutorials/create/eloqua/credentials.png)

通过安全组，管理员可以控制用户对资源、功能、界面等的访问级别。 要创建安全组，请导航到&#x200B;**设置** > **用户**。 然后，选择左侧面板上的&#x200B;**组**&#x200B;选项卡，然后选择&#x200B;**新建安全组**。

![Eloqua中的用户管理仪表板。](../../images/tutorials/create/eloqua/user-management.png)

使用&#x200B;**[!DNL Security Group Overview]**&#x200B;窗口提供安全组的名称和缩写。 创建后，导航到[!DNL Action Permissions]并从列表中添加[!DNL Consume] API权限，然后选择&#x200B;**保存**。

![Eloqua中的安全组概述窗口。](../../images/tutorials/create/eloqua/security-group-overview.png)

![使用API的选择窗口](../../images/tutorials/create/eloqua/consume-api.png)

>[!NOTE]
>
>[!DNL Consume] API是所需的权限，但您可以根据该应用程序的使用情况添加更多权限。

要摄取营销活动数据，请导航到&#x200B;**编辑用户**&#x200B;界面，并将[!DNL Guided Campaigns]添加到您选定的安全组。

![添加了具有引导式营销活动的安全组。](../../images/tutorials/create/eloqua/add-guided-campaigns.png)

您可以选择创建其他用户，并将该用户添加到安全组。 有关详细步骤，请阅读有关[!DNL Eloqua]创建用户[和](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/UserManagement/Tasks/CreatingIndividualUsers.htm)将用户分配给安全组[的](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityGroups/Tasks/AddingUsersToSecurityGroups.htm)文档。

### 收集所需的凭据

必须提供以下凭据的值才能将[!DNL Eloqua]连接到Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| 客户端 ID | 授权Experience Platform时，[!DNL Eloqua]用于识别您的帐户的公开标识符。 |
| 客户端密码 | 只有客户端应用程序和授权服务器才知道的机密密钥。 要验证您的帐户，此密钥与客户端ID一起必需。 |
| 用户名 | 与您的[!DNL Eloqua]帐户关联的用户名。 用于验证和授权您的访问权限。 用户名遵循`CompanyName\Username`格式。 |
| 密码 | 与您的[!DNL Eloqua]帐户关联的密码。 除了您的用户名之外，它还授予对您的Eloqua环境的访问权限。 |
| 基本端点 | [!DNL Eloqua]的身份验证基本URI的前缀。 进行身份验证时，基终结点不应包含`http://`或`https://`。 |

## [!DNL Eloqua]映射指南

>[!NOTE]
>
>以下是内部用于增量数据加载的增量字段：
>
>- **联系人：** `C_DateModified`
>- **帐户：** `M_DateModified`
>- **活动：** `CreatedAt`
>- **自定义对象：** `UpdatedAt`
>- **营销活动：** `updatedAt`

下表提供了Experience Platform中[!DNL Eloqua]源字段及其对应的Experience Data Model (XDM)目标字段之间的详细映射。 每一行都概述了转换逻辑（无论字段是否不可变），并提供了额外的注释来帮助您了解如何在Experience Platform中摄取和构建[!DNL Eloqua]数据。

### 帐户

| Eloqua Source列 | XDM目标路径 | 注释 |
| --- | --- | --- |
| `"Eloqua"` | accountKey.sourceType | 此字段始终设置为固定值“Eloqua”。 |
| `"${SOURCE_INSTANCE_ID}"` | accountKey.sourceInstanceID | `SOURCE_INSTANCE_ID`将自动被连接器替换。 |
| `Id` | accountKey.sourceID | |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | accountKey.sourceKey | `SOURCE_INSTANCE_ID`将自动被连接器替换。 |
| `M_CompanyName` | 帐户名称 | |
| `M_Country` | accountPhysicalAddress.country | |
| `M_Address1` | accountPhysicalAddress.street1 | |
| `M_City` | accountPhysicalAddress.city | |
| `M_State_Prov` | accountPhysicalAddress.stateProvince | |
| `M_Zip_Postal` | accountPhysicalAddress.postalCode | |
| `M_BusPhone` | accountPhone.number | |
| `M_Fax1` | accountFax.number | |
| `M_Account_Engagement_Score` | accountScore | |
| `M_Account_Type1` | 帐户类型 | |
| `M_Wesbsite1` | accountOrganization.website | |
| `M_Employees1` | accountOrganization.numberOfEmployees | |
| `to_decimal(M_Annual_Revenue1)` | accountOrganization.annualRevenue.amount | |
| `M_DateModified` | extSourceSystemAudit.lastUpdatedDate | |
| `M_DateCreated` | extSourceSystemAudit.createdDate | |
| `M_Industry1` | accountOrganization.industry | |
| `iif(M_SFDCAccountID != null && M_SFDCAccountID != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_SFDCAccountID, "sourceKey", concat(M_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(M_MSCRMAccountID != null && M_MSCRMAccountID != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_MSCRMAccountID, "sourceKey", concat(M_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | 连接器无法自动检测您的CRM实例ID。 您必须手动将`${CRM_INSTANCE_ID}`替换为您的实际CRM实例ID，即您的Salesforce或Dynamics实例ID。 在引入期间，如果存在`M_SFDCAccountID`，连接器将使用该值生成外部密钥并附加`\@CRM_INSTANCE_ID.Salesforce`。 如果该字段为空，则连接器将使用`M_MSCRMAccountID`并改为附加`\@CRM_INSTANCE_ID.Dynamics`。 如果两个字段都为空，此字段将设置为null。 |

{style="table-layout:auto"}

### 活动

| Eloqua Source列 | XDM目标路径 | 注释 |
| --- | --- | --- |
| `"Eloqua"` | personKey.sourceType | 此字段始终设置为固定值“Eloqua”。 |
| `"${SOURCE_INSTANCE_ID}"` | personKey.sourceInstanceID | `SOURCE_INSTANCE_ID`将自动被连接器替换。 |
| `ContactId` | personKey.sourceID |  |
| `concat(ContactId, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | personKey.sourceKey | `SOURCE_INSTANCE_ID`将自动被连接器替换。 |
| `ExternalId` | _id |  |
| `iif(ActivityType!=null && ActivityType!="", iif(ActivityType=="EmailSend", "directMarketing.emailSent", iif(ActivityType=="EmailOpen", "directMarketing.emailOpened", iif(ActivityType=="EmailClickthrough", "directMarketing.emailClicked", iif(ActivityType=="Unsubscribe", "directMarketing.emailUnsubscribed", iif(ActivityType=="Bounceback", "directMarketing.emailBounced", iif(ActivityType=="FormSubmit", "web.formFilledOut", iif(ActivityType=="PageView", "web.webpagedetails.pageViews", ActivityType))))))), null)` | 事件类型 | 根据ActivityType，将填充相应的Experience Platform eventType值。 对于ExternalActivities，Experience Platform中没有eventType。 您可以修改此映射以处理更多类型。 |
| `ActivityDate` | 时间戳 | |
| `iif(AssetType == "Email", AssetName, null)` | directMarketing.mailingName | |
| `iif(AssetType == "Email", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | directMarketing.mailingKey | `SOURCE_INSTANCE_ID`将自动被连接器替换。 |
| `iif(AssetType == "Email", EmailAddress, null)` | directMarketing.email | |
| `iif(ActivityType == "Bounceback", SmtpStatusCode, null)` | directMarketing.emailBouncedCode | |
| `iif(AssetType == "Email", SmtpMessage, null)` | directMarketing.emailBouncedDetails | |
| `iif(AssetType == "Email", EmailWebLink, null)` | directMarketing.linkURL | |
| `iif(ActivityType == "FormSubmit", AssetName, null)` | web.fillOutForm.webFormName | |
| `iif(ActivityType == "FormSubmit", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.fillOutForm.webFormKey | `SOURCE_INSTANCE_ID`将自动被连接器替换。 |
| `iif(ActivityType == "PageView", AssetName, null)` | web.webPageDetails.name | |
| `iif(ActivityType == "PageView", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.webPageDetails.webPageKey | `SOURCE_INSTANCE_ID`将自动被连接器替换。 |
| `iif(ActivityType == "PageView", Url, null)` | web.webPageDetails.URL | |

{style="table-layout:auto"}

### 营销活动

| Eloqua Source列 | XDM目标路径 | 注释 |
| --- | --- | --- |
| `"Eloqua"` | campaignKey.sourceType | 此字段始终设置为固定值“Eloqua”。 |
| `"${SOURCE_INSTANCE_ID}"` | campaignKey.sourceInstanceID | `SOURCE_INSTANCE_ID`将自动被连接器替换。 |
| `id` | campaignKey.sourceID | |
| `concat(id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | campaignKey.sourceKey | `SOURCE_INSTANCE_ID`将自动被连接器替换。 |
| `name` | campaignName | |
| `endAt` | campaignEndDate | |
| `startAt` | campaignStartDate | |
| `actualCost` | actualCost.amount | |
| `budgetedCost` | budgetedCost.amount | |
| `description` | campaignDescription | |
| `currentStatus` | campaignstatus | |
| `campaignType` | campaignType | |
| `createdAt` | extSourceSystemAudit.createdDate | |
| `updatedAt` | extSourceSystemAudit.lastUpdatedDate | |

{style="table-layout:auto"}

### 联系人

| Eloqua Source列 | XDM目标路径 | 注释 |
| --- | --- | --- |
| `"Eloqua"` | b2b.personKey.sourceType | 此字段始终设置为固定值“Eloqua”。 |
| `"${SOURCE_INSTANCE_ID}"` | b2b.personKey.sourceInstanceID | `SOURCE_INSTANCE_ID`将自动被连接器替换。 |
| `Id` | b2b.personKey.sourceID |  |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua"` | b2b.personKey.sourceKey | `SOURCE_INSTANCE_ID`将自动被连接器替换。 |
| `C_Company` | b2b.companyName |  |
| `C_Website1` | b2b.companyWebsite |  |
| `C_Job_Title1` | extendedWorkDetails.jobTitle |  |
| `C_Fax` | faxPhone.number |  |
| `C_MobilePhone` | mobilePhone.number |  |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))` | personComponents.sourceExternalKey | 如果[!DNL Eloqua]实例已与Salesforce同步，则保留此映射。 否则，请将其删除。 连接器无法确定CRM_INSTANCE_ID，因此您必须将${CRM_INSTANCE_ID}替换为您同步的Salesforce实例ID。 此映射同样适用于personComponents和extSourceSystemAudit，因此请保留两者。 |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))"` | personComponents.sourceExternalKey | 如果[!DNL Eloqua]实例已与Dynamics同步，则保留此映射。 否则，请将其删除。 连接器无法确定CRM_INSTANCE_ID，因此您必须将${CRM_INSTANCE_ID}替换为您同步的Dynamics实例ID。 此映射同样适用于personComponents和extSourceSystemAudit，因此请保留两者。 |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))"` | extSourceSystemAudit.externalKey | 如果[!DNL Eloqua]实例已与Salesforce同步，则保留此映射。 否则，请将其删除。 连接器无法确定CRM_INSTANCE_ID，因此您必须将${CRM_INSTANCE_ID}替换为您同步的Salesforce实例ID。 此映射同样适用于personComponents和extSourceSystemAudit，因此请保留两者。 |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | 如果[!DNL Eloqua]实例已与Dynamics同步，则保留此映射。 否则，请将其删除。 连接器无法确定CRM_INSTANCE_ID，因此您必须将${CRM_INSTANCE_ID}替换为您同步的Dynamics实例ID。 此映射同样适用于personComponents和extSourceSystemAudit，因此请保留两者。 |
| `C_DateCreated` | extSourceSystemAudit.createdDate |  |
| `C_DateModified` | extSourceSystemAudit.lastUpdatedDate |  |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | b2b.accountKey | 连接器无法确定CRM_INSTANCE_ID，因此您必须将${CRM_INSTANCE_ID}替换为您同步的CRM实例ID，即Salesforce实例ID或Dynamics实例ID。 此相同的映射同时适用于b2b.accountKey和personComponents.sourceAccountKey，因此请保留两者。 |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | personComponents.sourceAccountKey | 连接器无法确定CRM_INSTANCE_ID，因此您必须将${CRM_INSTANCE_ID}替换为您同步的CRM实例ID，即Salesforce实例ID或Dynamics实例ID。 此相同的映射同时适用于b2b.accountKey和personComponents.sourceAccountKey，因此请保留两者。 |
| `C_Lead_Source___Original1` | b2b.personSource | |
| `C_Lead_Source___Original1` | personComponents.personSource | |
| `C_Lead_Status1` | b2b.personStatus | |
| `C_Lead_Status1` | personComponents.personStatus | |
| `C_FirstName` | person.name.firstName | |
| `C_LastName` | person.name.lastName | |
| `C_Middle_Name1` | person.name.middleName | |
| `C_Salutation` | person.name.courtesyTitle | |
| `C_City` | workAddress.city | |
| `C_Country` | workAddress.country | |
| `C_Zip_Postal` | workAddress.postalCode | |
| `C_State_Prov` | workAddress.state | |

{style="table-layout:auto"}

### 活动类型映射引用

| Eloqua ActivityType | XDM eventType |
| -------------------- | --------------- |
| `EmailSend` | directMarketing.emailSent |
| `EmailOpen` | directMarketing.emailOpened |
| `EmailClickthrough` | directMarketing.emailClicked |
| `Unsubscribe` | directMarketing.emailUnsubscribed |
| `Bounceback` | directMarketing.emailBounced |
| `FormSubmit` | web.formFilledOut |
| `PageView` | web.webpagedetails.pageViews |
| `Other` | 按原样传递 |

{style="table-layout:auto"}

### 变量占位符

映射模板使用以下变量占位符，这些占位符在数据流运行后被替换：

| 占位符 | 描述 | 使用情况 |
| ----------- | ----------- | ----- |
| `${SOURCE_INSTANCE_ID}` | Eloqua源实例的唯一ID | 在源键中使用 |
| `${CRM_INSTANCE_ID}` | CRM系统的唯一ID (Salesforce/Dynamics) | 在外部键中使用 |

## 将[!DNL Eloqua]连接到Experience Platform

继续在Experience Platform中配置[!DNL Eloqua]源连接。 有关通过UI设置连接的分步指南，请参阅此处的[教程](../../tutorials/ui/create/marketing-automation/eloqua.md)。 阅读本教程以了解如何连接[!DNL Eloqua]帐户、选择数据、映射字段、计划摄取和监视数据流。

