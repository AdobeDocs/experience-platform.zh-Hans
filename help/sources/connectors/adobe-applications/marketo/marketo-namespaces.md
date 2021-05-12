---
keywords: Experience Platform；主页；热门主题；Marketo源连接器；命名空间;模式
solution: Experience Platform
title: Marketo命名空间
topic-legacy: overview
description: 本文档概述创建Marketo Engage源连接器时所需的自定义命名空间。
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
translation-type: tm+mt
source-git-commit: 8dd7b1724f3de12bf6a3a1b77ee8050fd1a9eaf3
workflow-type: tm+mt
source-wordcount: '1602'
ht-degree: 4%

---

# （测试版）[!DNL Marketo Engage]命名空间和模式

>[!IMPORTANT]
>
>[!DNL Marketo Engage]源当前处于测试状态。 功能和文档是主题更改。

本文档提供有关与[!DNL Marketo Engage]一起使用的B2B命名空间和模式（下称“[!DNL Marketo]”）的基础设置的信息。 本文档还提供了有关设置生成[!DNL Marketo] B2B命名空间和模式所需的邮递员自动化实用程序的详细信息。

## 设置[!DNL Marketo]命名空间和模式自动生成实用程序

使用[!DNL Marketo]命名空间和模式自动生成实用程序的第一步是设置您的平台开发人员控制台和[!DNL Postman]环境。

- 您可以从此[GitHub存储库](https://git.corp.adobe.com/marketo-engineering/namespace_schema_utility)下载命名空间和模式自动生成实用程序集合和环境。
- 有关使用平台API的信息，包括有关如何收集所需标头值和读取示例API调用的详细信息，请参阅[平台API入门指南](../../../../landing/api-guide.md)。
- 有关如何为平台API生成凭据的信息，请参阅教程[验证和访问Experience PlatformAPI](../../../../landing/api-authentication.md)。
- 有关如何为平台API设置[!DNL Postman]的信息，请参阅教程（位于[设置开发人员控制台和 [!DNL Postman]](../../../../landing/postman.md)）。

通过设置平台开发人员控制台和[!DNL Postman]，您现在可以开始将适当的环境值应用到您的[!DNL Postman]环境。

下表包含示例值以及有关填充[!DNL Postman]环境的其他信息：

| Variable | 描述 | 示例 |
| --- | --- | --- |
| `CLIENT_SECRET` | 用于生成`{ACCESS_TOKEN}`的唯一标识符。 有关如何检索`{CLIENT_SECRET}`的信息，请参阅教程中的[验证和访问Experience Platform API](../../../../landing/api-authentication.md)。 | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web令牌(JWT)是用于生成{ACCESS_TOKEN}的身份验证凭据。 有关如何生成`{JWT_TOKEN}`的信息，请参阅有关[验证和访问Experience Platform API](../../../../landing/api-authentication.md)的教程。 | `{JWT_TOKEN}` |
| `API_KEY` | 用于验证对Experience PlatformAPI的调用的唯一标识符。 有关如何检索`{API_KEY}`的信息，请参阅教程中的[验证和访问Experience Platform API](../../../../landing/api-authentication.md)。 | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | 完成对Experience Platform API的调用所需的授权令牌。 有关如何检索`{ACCESS_TOKEN}`的信息，请参阅教程中的[验证和访问Experience Platform API](../../../../landing/api-authentication.md)。 | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 对于[!DNL Marketo]，此值是固定的，并且始终设置为：`ent_dataservices_sdk`。 | `ent_dataservices_sdk` |
| `CONTAINER_ID` | `global`容器包含所有标准Adobe和Experience Platform合作伙伴提供的类、模式字段组、数据类型和模式。 对于[!DNL Marketo]，此值是固定的，始终设置为`global`。 | `global` |
| `PRIVATE_KEY` | 用于验证[!DNL Postman]实例以Experience PlatformAPI的凭据。 有关如何检索{PRIVATE_KEY}的说明，请参见有关设置开发人员控制台和[设置开发人员控制台和 [!DNL Postman]](../../../../landing/postman.md)的教程。 | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | 用于集成到Adobe I/O的凭据。 | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management系统(IMS)为Adobe服务提供身份验证框架。 对于[!DNL Marketo]，此值是固定的，始终设置为：`ims-na1.adobelogin.com`。 | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 拥有或许可产品和服务并允许访问其成员的企业实体。 有关如何检索`{IMS_ORG}`信息的说明，请参阅[设置开发人员控制台和 [!DNL Postman]](../../../../landing/postman.md)上的教程。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 您使用的虚拟沙箱分区的名称。 | `prod` |
| `TENANT_ID` | 一个ID，用于确保您创建的资源命名正确且包含在您的IMS组织中。 | `b2bcdpproductiontest` |
| `PLATFORM_URL` | 您对其进行API调用的URL端点。 此值是固定的，始终设置为：`http://platform.adobe.io/`。 | `http://platform.adobe.io/` |
| `munchkinId` | [!DNL Marketo]帐户的唯一ID。 有关如何检索`munchkinId`的信息，请参见[对您的 [!DNL Marketo] 实例](./marketo-auth.md)进行身份验证的教程。 | `123-ABC-456` |
| `sfdc_org_id` | [!DNL Salesforce]帐户的组织ID。 有关获取[!DNL Salesforce]组织ID的详细信息，请参阅以下[[!DNL Salesforce] 指南](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1)。 | `00D4W000000FgYJUA0` |
| `msd_org_id` | [!DNL Dynamics]帐户的组织ID。 有关获取[!DNL Dynamics]组织ID的详细信息，请参阅以下[[!DNL Microsoft Dynamics] 指南](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name)。 | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` |
| `has_abm` | 一个布尔值，指示您是否订阅[!DNL Marketo Account-Based Marketing]。 | `false` |
| `has_msi` | 一个布尔值，指示您是否被限定为[!DNL Marketo Sales Insight]。 | `false` |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] 命名空间

身份命名空间是[[!DNL Identity Service]](../../../../identity-service/home.md)的一个组件，用作身份相关上下文的指示器。

完全限定标识包括ID值和命名空间。 每个新[!DNL Marketo]实例和数据集组合都需要新的自定义命名空间。 例如，收录`programs`数据集的[!DNL Marketo]源连接器需要其自己的自定义命名空间，而收录同一数据集的另一个Marketo源连接器也需要其自己的新自定义命名空间。 有关详细信息，请参阅[命名空间概述](../../../../identity-service/namespaces.md)。

[!DNL Marketo]命名空间用于实体的主标识。

下表包含有关[!DNL Marketo]命名空间的基础设置的信息。

>[!NOTE]
>
>请向左/向右滚动以视图表的完整内容。

| 显示名称 | 身份符号 | 身份类型 | 颁发者类型 | 颁发者实体类型 | 蒙奇金ID示例 |
| --- | --- | --- | --- | --- | --- |
| `marketo_person_{MUNCHKIN_ID}` | 自动生成 | `CROSS_DEVICE` | [!DNL Marketo] | `person` | `123-ABC-789` |
| `marketo_company_{MUNCHKIN_ID}` | 自动生成 | `B2B_ACCOUNT` | [!DNL Marketo] | `company` | `123-ABC-789` |
| `marketo_opportunity_{MUNCHKIN_ID}` | 自动生成 | `B2B_OPPORTUNITY` | [!DNL Marketo] | `opportunity` | `123-ABC-789` |
| `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | 自动生成 | `B2B_OPPORTUNITY_PERSON` | [!DNL Marketo] | `opportunity contact role` | `123-ABC-789` |
| `marketo_program_{MUNCHKIN_ID}` | 自动生成 | `B2B_CAMPAIGN` | [!DNL Marketo] | `program` | `123-ABC-789` |
| `marketo_program_member_{MUNCHKIN_ID}` | 自动生成 | `B2B_CAMPAIGN_MEMBER` | [!DNL Marketo] | `program member` | `123-ABC-789` |
| `marketo_static_list_{MUNCHKIN_ID}` | 自动生成 | `B2B_MARKETING_LIST` | [!DNL Marketo] | `static list` | `123-ABC-789` |
| `marketo_static_list_member_{MUNCHKIN_ID}` | 自动生成 | `B2B_MARKETING_LIST_MEMBER` | [!DNL Marketo] | `static list member` | `123-ABC-789` |
| `marketo_named_account_{MUNCHKIN_ID}` | 自动生成 | `B2B_ACCOUNT` | [!DNL Marketo] | `named account` | `123-ABC-789` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Salesforce] 命名空间

如果您订阅了[!DNL Salesforce]集成，则[!DNL Salesforce]命名空间用于实体的次标识。

下表包含有关[!DNL Salesforce]命名空间的基础设置的信息。

>[!NOTE]
>
>请向左/向右滚动以视图表的完整内容。

| 显示名称 | 身份符号 | 身份类型 | 颁发者类型 | 颁发者实体类型 | [!DNL Salesforce] 订阅组织ID示例 |
| --- | --- | --- | --- | --- | --- |
| `salesforce_lead_{SALESFORCE_ORGANIZATION_ID}` | 自动生成 | `CROSS_DEVICE` | [!DNL Salesforce] | `lead` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | 自动生成 | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | 自动生成 | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | 自动生成 | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | 自动生成 | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | 自动生成 | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] 命名空间

如果您订阅了[!DNL Dynamics]集成，则[!DNL Dynamics]命名空间将用作实体的次标识。

下表包含有关[!DNL Dynamics]命名空间的基础设置的信息。

>[!NOTE]
>
>请向左/向右滚动以视图表的完整内容。

| 显示名称 | 身份符号 | 身份类型 | 颁发者类型 | 颁发者实体类型 | [!DNL Dynamics] 订阅组织ID示例 |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | 自动生成 | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | 自动生成 | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | 自动生成 | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | 自动生成 | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | 自动生成 | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | 自动生成 | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] 模式

Experience Platform 会使用架构，以便以可重用的一致方式描述数据结构。通过在整个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。

在将数据引入平台之前，必须构建一个模式来描述数据的结构，并对每个字段中可以包含的数据类型提供约束。 模式由基类和零个或多个模式字段组组成。

有关模式合成模型的详细信息（包括设计原则和最佳实践），请参阅[模式合成基础知识](../../../../xdm/schema/composition.md)。

下表包含有关[!DNL Marketo]模式的基础设置的信息。

>[!NOTE]
>
>请向左/向右滚动以视图表的完整内容。

| 模式名称 | 基类 | 字段组 | [!DNL Profile] 模式 | 主要身份 | 主要身份命名空间 | 次身份 | 辅助身份命名空间 | 关系 | 注释 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `[!DNL Marketo] Company {MUNCHKIN_ID}` | XDM业务帐户 | XDM业务帐户详细信息 | 已启用 | `accountID` 在基类中 | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基类中 | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` XDM业务帐户详细信息字段组</li><li>类型：一对一</li><li>参考模式:`[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>命名空间: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| `[!DNL Marketo] Person {MUNCHKIN_ID}` | XDM个人用户档案 | <ul><li>XDM业务人员详细信息</li><li>XDM业务人员组件</li><li>IdentityMap</li></ul> | 已启用 | `personID` 在基类中 | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` XDM业务人员详细信息字段组</li><li>`workEmail.address` XDM业务人员详细信息字段组</li><li>`identityMap` 身份映射字段组</ol></li> | <ol><li>`salesforce_lead_{SALESFORCE_ORGANIZATION_ID}`</li><li>电子邮件</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` XDM业务人员组件字段组</li><li>类型：多对一</li><li>参考模式:`[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>命名空间: `marketo_company_{MUNCHKIN_ID}`</li><li>目标属性：`accountID`</li><li>当前模式中的关系名称：帐户</li><li>引用模式中的关系名称：人物</li></ul> |
| `[!DNL Marketo] Opportunity {MUNCHKIN_ID}` | XDM业务机会 | XDM业务机会详细信息 | 已启用 | `opportunityID` 在基类中 | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基类中 | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` 在基类中</li><li>类型：多对一</li><li>参考模式:`[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>命名空间: `marketo_company_{MUNCHKIN_ID}`</li><li>目标属性：`accountID`</li><li>当前模式中的关系名称：帐户</li><li>引用模式中的关系名称：机会</li></ul> |
| `[!DNL Marketo] Opportunity Contact Role {MUNCHKIN_ID}` | XDM业务机会人关系 | None | 已启用 | `opportunityPersonID` 在基类中 | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基类中 | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | 第一种关系<ul><li>`personID` 在基类中</li><li>类型：多对一</li><li>参考模式:`[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>命名空间: `marketo_person_{MUNCHKIN_ID}`</li><li>目标属性：`personID`</li><li>当前模式中的关系名称：人</li><li>引用模式中的关系名称：机会</li></ul>第二种关系<ul><li>`opportunityID` 在基类中</li><li>类型：多对一</li><li>参考模式:`[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>命名空间: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>目标属性：`opportunityID`</li><li>当前模式中的关系名称：机会</li><li>引用模式中的关系名称：人物</li></ul> |
| `[!DNL Marketo] Program {MUNCHKIN_ID}` | XDM业务活动 | XDM业务活动详细信息 | 已启用 | `campaignID` 在基类中 | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基类中 | `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` |
| `[!DNL Marketo] Program Member {MUNCHKIN_ID}` | XDM业务活动会员 | XDM业务活动会员详细信息 | 已启用 | `campaignMemberID` 在基类中 | `marketo_program_member_{MUNCHKIN_ID}` | 无 | 无 | 第一种关系<ul><li>`personID` 在基类中</li><li>类型：多对一</li><li>参考模式:Marketo人{MUNCHKIN_ID}</li><li>命名空间: `marketo_person_{MUNCHKIN_ID}`</li><li>目标属性：`personID`</li><li>当前模式中的关系名称：人</li><li>引用模式中的关系名称：项目</li></ul>第二种关系<ul><li>`campaignID` 在基类中</li><li>类型：多对一</li><li>参考模式:`[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>命名空间: `marketo_program_{MUNCHKIN_ID}`</li><li>目标属性：`campaignID`</li><li>当前模式中的关系名称：项目</li><li>引用模式中的关系名称：人物</li></ul> |
| `[!DNL Marketo] Static List {MUNCHKIN_ID}` | XDM业务营销列表 | 无 | 已启用 | `marketingListID` 在基类中 | `marketo_static_list_{MUNCHKIN_ID}` | 无 | 无 | 无 | 静态列表未从[!DNL Salesforce]同步，因此没有辅助标识。 |
| `[!DNL Marketo] Static List Member {MUNCHKIN_ID}` | XDM业务营销列表会员 | 无 | 已启用 | `marketingListMemberID` 在基类中 | `marketo_static_list_member_{MUNCHKIN_ID}` | 无 | 无 | 第一种关系<ul><li>`personID` 在基类中</li><li>类型：多对一</li><li>参考模式:`[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>命名空间: `marketo_person_{MUNCHKIN_ID}`</li><li>目标属性：`personID`</li><li>当前模式中的关系名称：人</li><li>引用模式中的关系名称：列表</li></ul>第二种关系<ul><li>`marketingListID` 在基类中</li><li>类型：多对一</li><li>参考模式:`[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>命名空间: `marketo_static_list_{MUNCHKIN_ID}`</li><li>目标属性：`marketingListID`</li><li>当前模式中的关系名称：列表</li><li>引用模式中的关系名称：人物</li></ul> | 静态列表成员未从[!DNL Salesforce]同步，因此没有辅助标识。 |
| `[!DNL Marketo] Named Account {MUNCHKIN_ID}` | XDM业务帐户 | XDM业务帐户详细信息 | 已启用 | `accountID` 在基类中 | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基类中 | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` XDM业务帐户详细信息字段组</li><li>类型：一对一</li><li>参考模式:`[!DNL Marketo] Named Account {MUNCHKIN_ID}`</li><li>命名空间: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] 活动 `{MUNCHKIN ID}` | XDM ExperienceEvent | <ul><li>访问网页</li><li>新建潜在客户</li><li>转换潜在客户</li><li>添加到列表</li><li>从列表</li><li>添加到业务机会</li><li>从业务机会中删除</li><li>填写的表单</li><li>链接点击</li><li>电子邮件已送达</li><li>电子邮件已打开</li><li>已点击电子邮件</li><li>电子邮件退回</li><li>电子邮件退回软</li><li>取消订阅电子邮件</li><li>分数已更改</li><li>已更新业务机会</li><li>活动进展状态已更改</li><li>人员标识符</li><li>Marketo Web URL | 已启用 | `personID` 人员标识符字段组 | `marketo_person_{MUNCHKIN_ID}` | 无 | 无 | 第一种关系<ul><li>`listOperations.listID` 字段</li><li>类型：一对一</li><li>参考模式:`[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>命名空间: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>第二种关系<ul><li>`opportunityEvent.opportunityID` 字段</li><li>类型：一对一</li><li>参考模式:`[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>命名空间: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>第三种关系<ul><li>`leadOperation.campaignProgression.campaignID` 字段</li><li>类型：一对一</li><li>参考模式:`[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>命名空间: `marketo_program_{MUNCHKIN_ID}`</li></ul> | `[!DNL Marketo] Activity {MUNCHKIN_ID}`模式的主标识为`personID`，与`[!DNL Marketo] Person {MUNCHKIN_ID}`模式的主标识相同。 |

{style=&quot;table-layout:auto&quot;}

## 后续步骤

要了解如何将[!DNL Marketo]数据连接到平台，请参阅有关在UI](../../../tutorials/ui/create/adobe-applications/marketo.md)中创建Marketo源连接器的教程。[
