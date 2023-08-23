---
title: SugarCRM源概述
description: 了解如何使用API或用户界面将SugarCRM连接到Adobe Experience Platform。
last-substantial-update: 2023-08-23T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# [!DNL SugarCRM]

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从第三方CRM应用程序引入数据。 对CRM提供商的支持包括 [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) 是一个客户关系管理(CRM)系统。 [!DNL SugarCRM]的功能包括销售人员自动化、营销活动、客户支持、协作、Mobile CRM、Social CRM和报表。

此 [!DNL SugarCRM] 源允许您从以下API端点摄取帐户、联系人和事件数据：

* [帐户](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [联系人](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [事件](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)

[!DNL SugarCRM] 使用持有者令牌作为身份验证机制与 [!DNL SugarCRM] Account和Contact API以及 [!DNL SugarCRM] 事件API。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面以了解更多信息。

## 先决条件

在创建之前 [!DNL SugarCRM] 源连接时，您必须首先确保具备以下条件：

* A [!DNL SugarMarket] 帐户。 您必须联系 [!DNL SugarCRM] 客户经理以获取有效的 [!DNL SugarMarket] 帐户（如果没有）。

* 与营销或销售流程关联的任何用户帐户分开的唯一API用户名和帐户。 此唯一的用户名和帐户组合必须具有API访问权限。 欲知建立账户的详细流程，请访问 [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro) 文档。

## 连接 [!DNL SugarCRM Accounts & Contacts] 目标平台

* [创建源连接以引入 [!DNL SugarCRM Accounts & Contacts] 使用API将数据发送到平台](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [创建源连接以引入 [!DNL SugarCRM Accounts & Contacts] 使用用户界面将数据发送到Platform](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [使用流服务API为CRM源创建数据流](../../tutorials/api/collect/crm.md)


## 连接 [!DNL SugarCRM Events] 目标平台

* [创建源连接以引入 [!DNL SugarCRM Events] 使用API将数据发送到平台](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [创建源连接以引入 [!DNL SugarCRM Events] 使用用户界面将数据发送到Platform](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [在用户界面中为CRM源连接创建数据流](../../tutorials/ui/dataflow/crm.md)
