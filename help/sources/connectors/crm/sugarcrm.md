---
title: SugarCRM源概述
description: 了解如何使用API或用户界面将SugarCRM连接到Adobe Experience Platform。
badge: Beta
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# （测试版） [!DNL SugarCRM]

>[!NOTE]
>
>的 [!DNL SugarCRM] 来源为测试版。 请参阅 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

Experience Platform支持从第三方CRM应用程序摄取数据。 对CRM提供商的支持包括 [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) 是客户关系管理(CRM)系统。 [!DNL SugarCRM]的功能包括销售人员自动化、营销活动、客户支持、协作、移动CRM、Social CRM和报表。

的 [!DNL SugarCRM] 源允许您从以下API端点摄取帐户、联系人和事件数据：

* [帐户](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [联系人](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [事件](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)


[!DNL SugarCRM] 使用承载令牌作为与通信的验证机制 [!DNL SugarCRM] 帐户和联系API以及 [!DNL SugarCRM] 事件API。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表。 无法将特定于区域的IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面以了解更多信息。

## 先决条件

在创建 [!DNL SugarCRM] 源连接时，必须首先确保您具有以下内容：

* A [!DNL SugarMarket] 帐户。 您必须联系 [!DNL SugarCRM] 客户经理以获取有效 [!DNL SugarMarket] 帐户。

* 与营销或销售流程关联的任何用户帐户分开的唯一API用户名和帐户。 此唯一的用户名和帐户组合必须具有API访问权限。 有关设置帐户的流程的更多信息，请访问 [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro) 文档。

## 连接 [!DNL SugarCRM Accounts & Contacts] 到平台

* [创建源连接以引入 [!DNL SugarCRM Accounts & Contacts] 使用API将数据传输到平台](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [创建源连接以引入 [!DNL SugarCRM Accounts & Contacts] 使用用户界面将数据发送到平台](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [使用流服务API为CRM源创建数据流](../../tutorials/api/collect/crm.md)


## 连接 [!DNL SugarCRM Events] 到平台

* [创建源连接以引入 [!DNL SugarCRM Events] 使用API将数据传输到平台](../../tutorials/api/create/crm/sugarcrm-events.md).
* [创建源连接以引入 [!DNL SugarCRM Events] 使用用户界面将数据发送到平台](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [在UI中为CRM源连接创建数据流](../../tutorials/ui/dataflow/crm.md)
