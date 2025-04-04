---
title: SugarCRM Source概述
description: 了解如何使用API或用户界面将SugarCRM连接到Adobe Experience Platform。
last-substantial-update: 2023-08-23T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# [!DNL SugarCRM]

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform支持从第三方CRM应用程序中摄取数据。 CRM提供商的支持包括[!DNL SugarCRM]。

[[!DNL SugarCRM]](https://www.sugarcrm.com/)是客户关系管理(CRM)系统。 [!DNL SugarCRM]的功能包括销售人员自动化、营销活动、客户支持、协作、Mobile CRM、Social CRM和报表。

[!DNL SugarCRM]源允许您从以下API端点摄取帐户、联系人和事件数据：

* [帐户](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [联系人](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [事件](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)

[!DNL SugarCRM]使用持有者令牌作为身份验证机制与[!DNL SugarCRM]帐户和联系人API以及[!DNL SugarCRM]事件API进行通信。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

## 先决条件

在创建[!DNL SugarCRM]源连接之前，必须首先确保您具备以下条件：

* [!DNL SugarMarket]帐户。 如果您还没有有效的[!DNL SugarMarket]帐户，则必须联系[!DNL SugarCRM]帐户管理员以获取该帐户。

* 与营销或销售流程关联的任何用户帐户分开的唯一API用户名和帐户。 此唯一的用户名和帐户组合必须具有API访问权限。 有关帐户设置过程的详细信息，请访问[[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro)文档。

## 将[!DNL SugarCRM Accounts & Contacts]连接到Experience Platform

* [创建源连接以使用API将 [!DNL SugarCRM Accounts & Contacts] 数据引入Experience Platform](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md)。
* [使用用户界面](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md)创建源连接以将 [!DNL SugarCRM Accounts & Contacts] 数据引入Experience Platform。
* [使用流服务API为CRM源创建数据流](../../tutorials/api/collect/crm.md)


## 将[!DNL SugarCRM Events]连接到Experience Platform

* [创建源连接以使用API将 [!DNL SugarCRM Events] 数据引入Experience Platform](../../tutorials/ui/create/crm/sugarcrm-events.md)。
* [使用用户界面](../../tutorials/ui/create/crm/sugarcrm-events.md)创建源连接以将 [!DNL SugarCRM Events] 数据引入Experience Platform。
* [在用户界面中为CRM源连接创建数据流](../../tutorials/ui/dataflow/crm.md)
