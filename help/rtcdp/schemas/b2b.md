---
title: Real-time Customer Data Platform B2B版本中的架构
description: Experience Data Model (XDM)架构在Adobe Real-time Customer Data Platform B2B版本中的角色概述。
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B版本" type="Informative" url="https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 13%

---

# Real-time Customer Data Platform B2B版本中的架构

Adobe Real-time Customer Data Platform B2B版本提供了多个标准的[体验数据模型(XDM)类](../../xdm/schema/composition.md#class)，这些类捕获有关基本B2B数据实体的详细信息，如帐户、机会、营销活动等。 此外，Real-Time CDP B2B Edition允许您定义这些架构之间的多对一关系，以便它们可以参与高级分段用例。

>[!IMPORTANT]
>
>您必须有权访问Real-Time CDP B2B版本，B2B架构才能参与[实时客户个人资料](../../profile/home.md)。

Real-Time CDP B2B版本中提供了以下标准类：

* [XDM 业务帐户](../../xdm/classes/b2b/business-account.md)
* [XDM 业务帐户人员关系](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM 商业营销活动](../../xdm/classes/b2b/business-campaign.md)
* [XDM 商业营销活动成员](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM 商业机会](../../xdm/classes/b2b/business-opportunity.md)
* [XDM 业务机会人员关系](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM 商业营销列表](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM 商业营销列表成员](../../xdm/classes/b2b/business-marketing-list-members.md)

要了解架构如何适合您的B2B工作流，请参阅[端到端教程](../b2b-tutorial.md)。

有关如何创建两个架构之间的多对一关系的步骤，请参阅有关[定义B2B架构关系](../../xdm/tutorials/relationship-b2b.md)的教程。

如果您使用B2B源连接，则可以使用工具自动生成所需的架构以及架构之间的关系。 有关详细信息，请参阅源文档中有关[B2B命名空间](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)的指南。
