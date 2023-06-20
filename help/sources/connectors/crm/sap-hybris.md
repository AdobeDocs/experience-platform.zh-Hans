---
title: SAP Hybris源概述
description: 了解如何使用API或用户界面将SAP Hybris连接到Adobe Experience Platform。
badge: 测试版
hide: true
hidefromtoc: true
source-git-commit: 32e2c13dcdbf2f13b4025354dfc50f5ccaf5f664
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---

# [!DNL SAP Hybris]

>[!NOTE]
>
>此 [!DNL SAP Hybris] 源为测试版。 请参阅 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记源的更多信息。

[[!DNL SAP Hybris]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html)，SAP客户体验产品组合中提供了适用于B2B和B2C企业的基于云的电子商务平台解决方案。 [[!DNL SAP] 订阅帐单](https://www.sap.com/products/financial-management/subscription-billing.html) 是产品组合中的一个产品，它通过标准化的集成，通过简化的销售和支付体验实现了完整的订阅生命周期管理。

此 [!DNL SAP Hybris] 源允许您将客户和联系人信息从 [[!DNL SAP] 订阅帐单](https://www.sap.com/products/financial-management/subscription-billing.html) 以下业务合作伙伴API端点：

* [客户](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [联系人](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

此外，如果 [!DNL SAP Hybris] 运行以检索客户数据， [客户 — 联系人关系](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) 还调用API以检索客户的联系信息。

## IP地址允许列表 {#ip-allow-list}

在使用源连接器之前，可能需要将IP地址列表添加到允许列表。 未能将特定于地区的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 请参阅 [IP地址允许列表](../../ip-address-allow-list.md) 页面，以了解更多信息。

## 先决条件 {#prerequisites}

在您带上 [!DNL SAP Hybris] 要Experience Platform的数据，您必须首先确保具有以下各项：

* A [!DNL SAP Subscription Billing] 帐户。 如果您还没有有效的计费帐户，请联系贵机构的 [!DNL SAP] 客户经理。 请参阅 [[!DNL SAP] 平台配置](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) 文档，以了解更多详细信息。

* [!DNL SAP] 服务密钥。 此 [!DNL SAP] 服务密钥允许您访问 [!DNL SAP Subscription Billing] 通过Experience Platform的API。 [!DNL SAP Hybris] 要求您满足以下条件：
   * 客户端ID
   * 客户端密码
   * URL. URL模式如下： `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. 此值稍后将用于获取 `region` 和 `tokenEndpoint` 当您 [创建基本连接](../../tutorials/api/create/crm/sap-hybris.md#base-connection) 使用API或当您 [连接您的 [!DNL SAP Hybris] 帐户](../../tutorials/ui/create/crm/sap-hybris.md#connect-account) 通过Platform UI。

+++选择以查看服务键的示例

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

## 后续步骤

以下文档提供了有关如何连接的信息 [!DNL SAP Hybris] 至使用API或用户界面的Platform：

* [创建源连接和数据流以引入 [!DNL SAP Hybris] 使用API将数据发送到平台](../../tutorials/api/create/crm/sap-hybris.md).
* [连接您的 [!DNL SAP Hybris] 要使用UIExperience Platform的帐户](../../tutorials/ui/create/crm/sap-hybris.md).
* [使用UI为CRM源创建数据流](../../tutorials/ui/dataflow/crm.md)
