---
title: 实时客户数据平台B2B版中的模式
description: 概述Experience Data Model(XDM)模式在实时客户数据平台B2B版中的角色。
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# 实时客户数据平台B2B版（测试版）中的架构

>[!IMPORTANT]
>
>实时客户数据平台B2B版目前处于测试阶段。 文档和功能可能会发生更改。

实时客户数据平台B2B版提供了多个标准[体验数据模型(XDM)类](../../xdm/schema/composition.md#class)，可捕获有关基本B2B数据实体（如帐户、机会、营销活动等）的详细信息。 此外，实时CDP B2B Edition还允许您定义这些模式之间的多对一关系，以便它们能够参与高级分段用例。

Real-time CDP B2B Edition中提供了以下标准类：

* [XDM业务帐户](../../xdm/classes/b2b/business-account.md)
* [XDM业务帐户人员关系](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [XDM Business Campaign成员](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM业务机会](../../xdm/classes/b2b/business-opportunity.md)
* [XDM业务机会人员关系](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM业务营销列表](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM业务营销列表成员](../../xdm/classes/b2b/business-marketing-list-members.md)

有关如何在两个架构之间创建多对一关系的步骤，请参阅[定义B2B架构关系](../../xdm/tutorials/relationship-b2b.md)的教程。

如果您使用B2B源连接，则可以使用工具自动生成所需的架构及其之间的关系。 有关更多信息，请参阅源文档中[B2B命名空间](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)的指南。
