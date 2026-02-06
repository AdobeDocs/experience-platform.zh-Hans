---
title: Real-Time Customer Data Platform B2B edition中的架构
description: Experience Data Model (XDM)架构在Adobe Real-Time Customer Data Platform B2B edition中的角色概述。
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=zh-Hans#rtcdp-editions" newtab=true
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 8%

---

# Real-Time Customer Data Platform B2B edition中的架构

Adobe Real-Time Customer Data Platform B2B edition提供了多个标准的[体验数据模型(XDM)类](../../xdm/schema/composition.md#class)，这些类捕获有关基本B2B数据实体的详细信息，如帐户、机会、营销活动等。 此外，Real-Time CDP B2B edition允许您定义这些架构之间的多对一关系，以便它们可以参与高级分段用例。

>[!IMPORTANT]
>
>B2B架构可在Experience Platform应用程序中使用(例如，在[Customer Journey Analytics B2B edition](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition)中)。 <br/>但是，您必须拥有Real-Time CDP B2B edition的访问权限，才能使B2B架构（中的配置文件）参与[实时客户配置文件](../../profile/home.md)。

Real-Time CDP B2B edition中提供了以下标准类：

* [XDM业务帐户](../../xdm/classes/b2b/business-account.md)
* [XDM业务帐户人员关系](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM商业营销活动](../../xdm/classes/b2b/business-campaign.md)
* [XDM商业营销活动成员](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM商业机会](../../xdm/classes/b2b/business-opportunity.md)
* [XDM业务机会人员关系](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM业务营销列表](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM商业营销列表成员](../../xdm/classes/b2b/business-marketing-list-members.md)

要了解架构如何适合您的B2B工作流，请参阅[端到端教程](../b2b-tutorial.md)。

有关如何创建两个架构之间的多对一关系的步骤，请参阅有关[定义B2B架构关系](../../xdm/tutorials/relationship-b2b.md)的教程。

如果您使用B2B源连接，则可以使用工具自动生成所需的架构以及架构之间的关系。 有关详细信息，请参阅源文档中有关[B2B命名空间](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)的指南。


下表包含有关B2B架构的基础设置的信息。

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| 架构名称 | 基类 | 字段组 | 架构中的[!DNL Profile] | 主要身份标识 | 主要身份标识命名空间 | 辅助标识 | 辅助身份命名空间 | 关系 | 注释 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B 帐户 | [XDM业务帐户](../../xdm/classes/b2b/business-account.md) | XDM业务帐户详细信息 | 已启用 | 基类中的`accountKey.sourceKey` | B2B 帐户 | 基类中的`extSourceSystemAudit.externalKey.sourceKey` | B2B 帐户 | <ul><li>XDM业务帐户详细信息字段组中的`accountParentKey.sourceKey`</li><li>目标属性： `/accountKey/sourceKey`</li><li>类型：一对一</li><li>引用架构：B2B帐户</li><li>命名空间： B2B帐户</li></ul> |  |
| B2B人员 | [XDM 轮廓](../../xdm/classes/individual-profile.md) | <ul><li>XDM业务人员详细信息</li><li>XDM业务人员组件</li><li>Identitymap</li><li>同意和偏好设置详细信息</li></ul> | 已启用 | XDM业务人员详细信息字段组中的`b2b.personKey.sourceKey` | B2B人员 | <ol><li>XDM业务人员详细信息字段组的`extSourceSystemAudit.externalKey.sourceKey`</li><li>XDM业务人员详细信息字段组的`workEmail.address`</ol></li> | <ol><li>B2B人员</li><li>电子邮件</li></ol> | <ul><li>XDM业务人员组件字段组的`personComponents.sourceAccountKey.sourceKey`</li><li>类型：多对一</li><li>引用架构：B2B帐户</li><li>命名空间： B2B帐户</li><li>目标属性： accountKey.sourceKey</li><li>来自当前架构的关系名称：帐户</li><li>引用架构中的关系名称：人员</li></ul> |  |
| B2B 机会 | [XDM业务机会](../../xdm/classes/b2b/business-opportunity.md) | XDM业务机会详细信息 | 已启用 | 基类中的`opportunityKey.sourceKey` | B2B 机会 | 基类中的`extSourceSystemAudit.externalKey.sourceKey` | B2B 机会 | <ul><li>基类中的`accountKey.sourceKey`</li><li>类型：多对一</li><li>引用架构：B2B帐户</li><li>命名空间： B2B帐户</li><li>目标属性： `accountKey.sourceKey`</li><li>来自当前架构的关系名称：帐户</li><li>引用架构中的关系名称：机会</li></ul> |  |
| B2B机会人员关系 | [XDM业务机会人员关系](../../xdm/classes/b2b/business-opportunity-person-relation.md) | None | 已启用 | 基类中的`opportunityPersonKey.sourceKey` | B2B机会人员关系 | | | **第一个关系**<ul><li>基类中的`personKey.sourceKey`</li><li>类型：多对一</li><li>引用架构：B2B人员</li><li>命名空间： B2B人员</li><li>目标属性： b2b.personKey.sourceKey</li><li>来自当前架构的关系名称：人员</li><li>引用架构中的关系名称：机会</li></ul>**第二个关系**<ul><li>基类中的`opportunityKey.sourceKey`</li><li>类型：多对一</li><li>引用架构：B2B机会 </li><li>命名空间： B2B机会 </li><li>目标属性： `opportunityKey.sourceKey`</li><li>来自当前架构的关系名称：机会</li><li>引用架构中的关系名称：人员</li></ul> |  |
| B2B 营销活动 | [XDM商业营销活动](../../xdm/classes/b2b/business-campaign.md) | XDM商业营销活动详细信息 | 已启用 | 基类中的`campaignKey.sourceKey` | B2B 营销活动 | | | | |
| B2B 营销活动成员 | [XDM商业营销活动成员](../../xdm/classes/b2b/business-campaign-members.md) | XDM商业营销活动成员详细信息 | 已启用 | 基类中的`ccampaignMemberKey.sourceKey` | B2B 营销活动成员 | | | **第一个关系**<ul><li>基类中的`personKey.sourceKey`</li><li>类型：多对一</li><li>引用架构：B2B人员</li><li>命名空间： B2B人员</li><li>目标属性： `b2b.personKey.sourceKey`</li><li>来自当前架构的关系名称：人员</li><li>引用架构中的关系名称：营销活动</li></ul>**第二个关系**<ul><li>基类中的`campaignKey.sourceKey`</li><li>类型：多对一</li><li>引用架构：B2B营销活动</li><li>命名空间： B2B营销活动</li><li>目标属性： `campaignKey.sourceKey`</li><li>来自当前架构的关系名称：营销活动</li><li>引用架构中的关系名称：人员</li></ul> |  |
| B2B 营销列表 | [XDM商业营销列表](../../xdm/classes/b2b/business-marketing-list.md) | None | 已启用 | 基类中的`marketingListKey.sourceKey` | B2B 营销列表 | None | None | None | 静态列表未从[!DNL Salesforce]同步，因此没有辅助标识。 |
| B2B 营销列表成员 | [XDM商业营销列表成员](../../xdm/classes/b2b/business-marketing-list-members.md) | None | 已启用 | 基类中的`marketingListMemberKey.sourceKey` | B2B 营销列表成员 | None | None | **第一个关系**<ul><li>基类中的`PersonKey.sourceKey`</li><li>类型：多对一</li><li>引用架构：B2B人员</li><li>命名空间： B2B人员</li><li>目标属性： `b2b.personKey.sourceKey`</li><li>来自当前架构的关系名称：人员</li><li>引用架构中的关系名称：营销列表</li></ul>**第二个关系**<ul><li>基类中的`marketingListKey.sourceKey`</li><li>类型：多对一</li><li>引用架构：B2B营销列表</li><li>命名空间： B2B营销列表</li><li>目标属性： `marketingListKey.sourceKey`</li><li>来自当前架构的关系名称：营销列表</li><li>引用架构中的关系名称：人员</li></ul> | 静态列表成员未从[!DNL Salesforce]同步，因此没有辅助标识。 |
| B2B帐户人员关系 | [XDM业务帐户人员关系](../../xdm/classes/b2b/business-account-person-relation.md) | 身份标识映射 | 已启用 | 基类中的`accountPersonKey.sourceKey` | B2B帐户人员关系 | None | None | **第一个关系**<ul><li>基类中的`personKey.sourceKey`</li><li>类型：多对一</li><li>引用架构：B2B人员</li><li>命名空间： B2B人员</li><li>目标属性： `b2b.personKey.SourceKey`</li><li>来自当前架构的关系名称：人员</li><li>引用架构中的关系名称：帐户</li></ul>**第二个关系**<ul><li>基类中的`accountKey.sourceKey`</li><li>类型：多对一</li><li>引用架构：B2B帐户</li><li>命名空间： B2B帐户</li><li>目标属性： `accountKey.sourceKey`</li><li>来自当前架构的关系名称：帐户</li><li>引用架构中的关系名称：人员</li></ul> |  |

{style="table-layout:auto"}

