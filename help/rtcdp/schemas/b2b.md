---
title: Real-Time Customer Data Platform B2B edition中的架构
description: Experience Data Model (XDM)架构在Adobe Real-Time Customer Data Platform B2B edition中的角色概述。
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 09f671af0d04251ab7b0a71528cb4b9745594b1c
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 12%

---

# Real-Time Customer Data Platform B2B edition中的架构

Adobe Real-Time Customer Data Platform B2B edition提供了多个标准的[体验数据模型(XDM)类](../../xdm/schema/composition.md#class)，这些类捕获有关基本B2B数据实体的详细信息，如帐户、机会、营销活动等。 此外，Real-Time CDP B2B edition允许您定义这些架构之间的多对一关系，以便它们可以参与高级分段用例。

>[!IMPORTANT]
>
>B2B架构可在Experience Platform应用程序中使用(例如，在[Customer Journey Analytics B2B edition](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition)中)。 <br/>但是，您必须拥有Real-Time CDP B2B edition的访问权限，才能使B2B架构（中的配置文件）参与[实时客户配置文件](../../profile/home.md)。

Real-Time CDP B2B edition中提供了以下标准类：

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
