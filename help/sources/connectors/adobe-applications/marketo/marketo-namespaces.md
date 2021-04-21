---
keywords: Experience Platform；主页；热门主题；Marketo源连接器；命名空间;模式
solution: Experience Platform
title: 'Marketo命名空间 '
topic: 概述
description: 本文档概述创建Marketo Engage源连接器时所需的自定义命名空间。
translation-type: tm+mt
source-git-commit: 2563b413ec35cb4c5f05a54bce6f7271917e51f3
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 5%

---


# （测试版）[!DNL Marketo Engage]命名空间和模式

>[!IMPORTANT]
>
>[!DNL Marketo Engage]源当前处于测试状态。 功能和文档是主题更改。

本文档提供有关与[!DNL Marketo Engage]一起使用的B2B命名空间和模式（下称“[!DNL Marketo]”）的基础设置的信息。 本文档还提供了有关设置生成[!DNL Marketo] B2B命名空间和模式所需的邮递员自动化实用程序的详细信息。

## 先决条件

在生成B2B命名空间和模式之前，必须先设置平台开发者控制台和[!DNL Postman]环境。 有关详细信息，请参阅教程中的[设置开发人员控制台和 [!DNL Postman]](../../../../landing/postman.md)。

通过平台开发人员控制台和[!DNL Postman]设置，将以下变量应用于您的[!DNL Marketo]环境:

| 环境变量 | 示例值 | 注释 |
| --- | --- | --- |
| `PRIVATE_KEY` | `{PRIVATE_KEY}` |
| `SANDBOX_NAME` | `prod` |
| `TENANT_ID` | `b2bcdpproductiontest` |
| `munchkinId` | `123-ABC-456 ` | 有关详细信息，请参阅教程[验证 [!DNL Marketo] 实例](./marketo-auth.md)。 |
| `sfdc_org_id` | `00D4W000000FgYJUA0` | 有关获取组织ID的详细信息，请参阅以下[[!DNL Salesforce] 指南](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1)。 |
| `msd_org_id` | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` | 有关获取组织ID的详细信息，请参阅以下[[!DNL Microsoft Dynamics] 指南](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name)。 |
| `has_abm` | `false` | 如果您订阅了基于帐户的营销，则此值设置为`true`。 |
| `has_msi` | `false` | 如果您订阅[!DNL Marketo Sales Insight]，则此值设置为`true`。 |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] 命名空间

身份命名空间是[[!DNL Identity Service]](../../../../identity-service/home.md)的一个组件，用作身份相关上下文的指示器。

完全限定标识包括ID值和命名空间。 每个新[!DNL Marketo]实例和数据集组合都需要新的自定义命名空间。 例如，收录`programs`数据集的[!DNL Marketo]源连接器需要其自己的自定义命名空间，而收录同一数据集的另一个Marketo源连接器也需要其自己的新自定义命名空间。 有关详细信息，请参阅[命名空间概述](../../../../identity-service/namespaces.md)。

[!DNL Marketo]命名空间用于实体的主标识。

下表包含有关[!DNL Marketo]命名空间的基础设置的信息。

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

| 显示名称 | 身份符号 | 身份类型 | 颁发者类型 | 颁发者实体类型 | [!DNL Salesforce] 订阅组织ID示例 |
| --- | --- | --- | --- | --- | --- |
| `salesforce_person_{SALESFORCE_ORGANIZATION_ID}` | 自动生成 | `CROSS_DEVICE` | [!DNL Salesforce] | `person` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | 自动生成 | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | 自动生成 | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | 自动生成 | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | 自动生成 | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | 自动生成 | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] 命名空间

如果您订阅了[!DNL Dynamics]集成，则[!DNL Dynamics]命名空间将用作实体的次标识。

下表包含有关[!DNL Dynamics]命名空间的基础设置的信息。

| 显示名称 | 身份符号 | 身份类型 | 颁发者类型 | 颁发者实体类型 | [!DNL Salesforce] 订阅组织ID示例 |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | 自动生成 | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | 自动生成 | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | 自动生成 | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | 自动生成 | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | 自动生成 | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | 自动生成 | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

## [!DNL Marketo] 模式

Experience Platform 会使用架构，以便以可重用的一致方式描述数据结构。通过在整个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。

在将数据引入平台之前，必须构建一个模式来描述数据的结构，并对每个字段中可以包含的数据类型提供约束。 模式由基类和零个或多个混合组成。

有关模式合成模型的详细信息（包括设计原则和最佳实践），请参阅[模式合成基础知识](../../../../xdm/schema/composition.md)。

下表包含有关[!DNL Marketo]模式的基础设置的信息。

>[!NOTE]
>
>请向左/向右滚动以视图表的完整内容。

| 模式名称 | 基类 | Mixins | 主要身份 | 主要身份命名空间 | 次身份 | 辅助身份命名空间 | 关系 | 注释 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [!DNL Marketo] 公司{MUNCHKIN_ID} | XDM业务帐户 | XDM业务帐户详细信息 | `accountID` 在基类中 | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基类中 | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` XDM业务帐户详细信息混合</li><li>类型：一对一</li><li>参考模式:Marketo公司{MUNCHKIN_ID}</li><li>命名空间: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| [!DNL Marketo] 人物{MUNCHKIN_ID} | XDM个人用户档案 | <ul><li>XDM业务人员详细信息</li><li>XDM业务人员组件</li></ul> | `personID` 在基类中 | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` XDM企业人员详细信息混合</li><li>`workEmail.address` XDM企业人员详细信息混合</li><li>`identityMap` 身份映射混音</ol></li> | <ol><li>`salesforce_person_{SALESFORCE_ORGANIZATION_ID}`</li><li>电子邮件</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` XDM企业人员组件混合</li><li>类型：多对一</li><li>参考模式:Marketo公司{MUNCHKIN_ID}</li><li>命名空间: `marketo_company_{MUNCHKIN_ID}`</li><li>目标属性：`accountID`</li><li>当前模式中的关系名称：帐户</li><li>引用模式中的关系名称：人物</li></ul> |
| [!DNL Marketo] 机会{MUNCHKIN_ID} | XDM业务机会 | XDM业务机会详细信息 | `opportunityID` 在基类中 | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基类中 | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` 在基类中</li><li>类型：多对一</li><li>参考模式:Marketo公司{MUNCHKIN_ID}</li><li>命名空间: `marketo_company_{MUNCHKIN_ID}`</li><li>目标属性：`accountID`</li><li>当前模式中的关系名称：帐户</li><li>引用模式中的关系名称：机会</li></ul> |
| [!DNL Marketo] 机会联系角色{MUNCHKIN_ID} | XDM业务机会人关系 | None | `opportunityPersonID` 在基类中 | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基类中 | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | 第一种关系<ul><li>`personID` 在基类中</li><li>类型：多对一</li><li>参考模式:Marketo人{MUNCHKIN_ID}</li><li>命名空间: `marketo_person_{MUNCHKIN_ID}`</li><li>目标属性：`personID`</li><li>当前模式中的关系名称：人</li><li>引用模式中的关系名称：机会</li></ul>第二种关系<ul><li>`opportunityID` 在基类中</li><li>类型：多对一</li><li>参考模式:Marketo机会{MUNCHKIN_ID}</li><li>命名空间: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>目标属性：`opportunityID`</li><li>当前模式中的关系名称：机会</li><li>引用模式中的关系名称：人物</li></ul> |
| [!DNL Marketo] 项目{MUNCHKIN_ID} | XDM业务活动 | XDM业务活动详细信息 | `campaignID` 在基类中 | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基类中 | `salesforce_campaign_SALESFORCE_ORGANIZATION_ID}` |
| [!DNL Marketo] 项目成员{MUNCHKIN_ID} | XDM业务活动会员 | XDM业务活动会员详细信息 | `campaignMemberID` 在基类中 | `marketo_program_member_{MUNCHKIN_ID}` | 无 | 无 | 第一种关系<ul><li>`personID` 在基类中</li><li>类型：多对一</li><li>参考模式:Marketo人{MUNCHKIN_ID}</li><li>命名空间: `marketo_person_{MUNCHKIN_ID}`</li><li>目标属性：`personID`</li><li>当前模式中的关系名称：人</li><li>引用模式中的关系名称：项目</li></ul>第二种关系<ul><li>`campaignID` 在基类中</li><li>类型：多对一</li><li>参考模式:Marketo项目{MUNCHKIN_ID}</li><li>命名空间: `marketo_program_{MUNCHKIN_ID}`</li><li>目标属性：campaignID</li><li>当前模式中的关系名称：项目</li><li>引用模式中的关系名称：人物</li></ul> |
| [!DNL Marketo] 静态列表{MUNCHKIN_ID} | XDM业务营销列表 | 无 | `marketingListID` 在基类中 | `marketo_static_list_{MUNCHKIN_ID}` | 无 | 无 | 无 | 静态列表未从[!DNL Salesforce]同步，因此没有辅助标识 |
| [!DNL Marketo] 静态列表成员{MUNCHKIN_ID} | XDM业务营销列表会员 | 无 | `marketingListMemberID` 在基类中 | `marketo_static_list_member_{MUNCHKIN_ID}` | 无 | 无 | 第一种关系<ul><li>`personID` 在基类中</li><li>类型：多对一</li><li>参考模式:Marketo人{MUNCHKIN_ID}</li><li>命名空间: `marketo_person_{MUNCHKIN_ID}`</li><li>目标属性：`personID`</li><li>当前模式中的关系名称：人</li><li>引用模式中的关系名称：列表</li></ul>第二种关系<ul><li>`marketingListID` 在基类中</li><li>类型：多对一</li><li>参考模式:Marketo静态列表{MUNCHKIN_ID}</li><li>命名空间: `marketo_static_list_{MUNCHKIN_ID}`</li><li>目标属性：`marketingListID`</li><li>当前模式中的关系名称：列表</li><li>引用模式中的关系名称：人物</li></ul> |
| [!DNL Marketo] 命名帐户{MUNCHKIN_ID} | XDM业务帐户 | XDM业务帐户详细信息 | `accountID` 在基类中 | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` 在基类中 | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` XDM业务帐户详细信息混合</li><li>类型：一对一</li><li>参考模式:Marketo指定帐户{MUNCHKIN_ID}</li><li>命名空间: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] 活动{MUNCHKIN ID} | XDM体验事件 | <ul><li>访问网页</li><li>新建潜在客户</li><li>转换潜在客户</li><li>添加到列表</li><li>从列表</li><li>添加到业务机会</li><li>从业务机会中删除</li><li>填写的表单</li><li>链接点击</li><li>电子邮件已送达</li><li>电子邮件已打开</li><li>已点击电子邮件</li><li>电子邮件退回</li><li>电子邮件退回软</li><li>取消订阅电子邮件</li><li>分数已更改</li><li>已更新业务机会</li><li>活动进展状态已更改</li><li>人员标识符</li><li>Marketo Web URL | `personID` 人物标识符混合 | marketo_person_{MUNCHKIN_ID} | 无 | 无 | 第一种关系<ul><li>`listOperations.listID` 字段</li><li>类型：一对一</li><li>参考模式:Marketo静态列表{MUNCHKIN_ID}</li><li>命名空间: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>第二种关系<ul><li>`opportunityEvent.opportunityID` 字段</li><li>类型：一对一</li><li>参考模式:Marketo机会{MUNCHKIN_ID}</li><li>命名空间: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>第三种关系<ul><li>`leadOperation.campaignProgression.campaignID` 字段</li><li>类型：一对一</li><li>参考模式:Marketo项目{MUNCHKIN_ID}</li><li>命名空间: `marketo_program_{MUNCHKIN_ID}`</li></ul> |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>[!DNL Real-time Customer Profile]启用所有模式

## 后续步骤

要了解如何将[!DNL Marketo]数据连接到平台，请参阅有关在UI](../../../tutorials/ui/create/adobe-applications/marketo.md)中创建Marketo源连接器的教程。[