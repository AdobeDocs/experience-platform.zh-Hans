---
title: SAP Commerce Source概述
description: 了解如何使用API或用户界面将SAP Commerce连接到Adobe Experience Platform。
last-substantial-update: 2023-07-26T00:00:00Z
badge: Beta 版
exl-id: d2ddfec3-a421-48a7-b765-86ce9162f26f
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 3%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>[!DNL SAP Commerce]源为测试版。 有关使用测试版标记源的更多信息，请参阅[源概述](../../home.md#terms-and-conditions)。

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html)，一种针对B2B和B2C企业的基于云的电子商务平台解决方案已作为SAP客户体验产品组合的一部分提供。 [[!DNL SAP] 订阅帐单](https://www.sap.com/products/financial-management/subscription-billing.html)是产品组合中的产品，通过标准化的集成，通过简化的销售和付款体验实现完整的订阅生命周期管理。

[!DNL SAP Commerce]源允许您从以下[[!DNL SAP] 订阅计费](https://www.sap.com/products/financial-management/subscription-billing.html)业务合作伙伴API端点将客户和联系人信息摄取到Experience Platform中：

* [客户](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [联系人](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

此外，如果运行[!DNL SAP Commerce]以检索客户数据，则还会调用[客户与联系人关系](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) API以检索客户的联系信息。

## IP地址允许列表 {#ip-allow-list}

在将源连接到Experience Platform之前，必须将特定于区域的IP地址添加到允许列表。 有关详细信息，请阅读有关[将IP地址列入允许列表到Experience Platform](../../ip-address-allow-list.md)的指南。

## 先决条件 {#prerequisites}

在将[!DNL SAP Commerce]数据带入Experience Platform之前，您必须首先确保您具备以下条件：

* [!DNL SAP Subscription Billing]帐户。 如果您还没有有效的帐单帐户，请联系您的[!DNL SAP]帐户经理。 有关其他详细信息，请参阅[[!DNL SAP] 平台配置](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf)文档。

* [!DNL SAP]服务密钥。 [!DNL SAP]服务密钥允许您通过Experience Platform访问[!DNL SAP Subscription Billing] API。 [!DNL SAP Commerce] 要求您满足以下条件：
   * 客户端 ID
   * 客户端密码
   * URL。 URL模式如下： `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`。 当您使用API `region`创建基本连接`tokenEndpoint`或通过Experience Platform UI [连接您的](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection)帐户[时，此值稍后将用于获取 [!DNL SAP Commerce] 和](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account)的值。

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

以下文档提供了有关如何使用API或用户界面将[!DNL SAP Commerce]连接到Experience Platform的信息：

* [创建源连接和数据流以使用API将 [!DNL SAP Commerce] 数据引入Experience Platform](../../tutorials/api/create/ecommerce/sap-commerce.md)。
* 使用UI [将您的 [!DNL SAP Commerce] 帐户连接到Experience Platform](../../tutorials/ui/create/ecommerce/sap-commerce.md)。
* [使用UI为源创建数据流](../../tutorials/ui/dataflow/ecommerce.md)
