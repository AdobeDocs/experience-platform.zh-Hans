---
title: Real-time Customer Data Platform B2B版中的模式
description: 概述Adobe Real-time Customer Data Platform B2B Edition中体验数据模型(XDM)模式的角色。
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Real-time Customer Data Platform B2B版中的模式

Adobe Real-time Customer Data Platform B2B Edition提供多个标准 [体验数据模型(XDM)类](../../xdm/schema/composition.md#class) 可捕获关于基本B2B数据实体（如帐户、机会、营销活动等）的详细信息。 此外，Real-Time CDP B2B Edition还允许您定义这些架构之间的多对一关系，以便它们能够参与高级分段用例。

>[!IMPORTANT]
>
>您必须拥有Real-Time CDP B2B Edition的访问权限，才能使B2B模式参与 [实时客户资料](../../profile/home.md).

Real-Time CDP B2B Edition提供了以下标准类：

* [XDM业务帐户](../../xdm/classes/b2b/business-account.md)
* [XDM业务帐户人员关系](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign成员](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM业务机会](../../xdm/classes/b2b/business-opportunity.md)
* [XDM业务机会人员关系](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM业务营销列表](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM业务营销列表成员](../../xdm/classes/b2b/business-marketing-list-members.md)

要了解架构如何适合您的B2B工作流，请参阅 [端到端教程](../b2b-tutorial.md).

有关如何在两个模式之间创建多对一关系的步骤，请参阅 [定义B2B模式关系](../../xdm/tutorials/relationship-b2b.md).

如果您使用B2B源连接，则可以使用工具自动生成所需的架构及其之间的关系。 请参阅 [B2B命名空间](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) （详细信息）。
