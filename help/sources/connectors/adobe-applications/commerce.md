---
title: Adobe Commerce源连接器
description: 了解如何使用Adobe Commerce源将商业数据引入Experience Platform。
last-substantial-update: 2023-06-21T00:00:00Z
source-git-commit: 49098cd11249a44ad7780857e85d054ece864046
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 1%

---

# Adobe Commerce

Adobe Commerce是一个敏捷的B2B和B2C商业平台，使商家和品牌能够通过在线和实体空间中的以客户为中心的数字商业体验来加快收入增长。

Adobe Experience Platform源支持Adobe Commerce的集成，允许商家将店面和后台数据发送到Adobe Experience Edge，以便其他Adobe Experience Cloud产品(如Adobe Analytics和Adobe Target)可以使用 [!DNL Commerce] 数据。

* **店面活动**：捕获购物者交互，例如 `View Page`， `View Product`、和 `Add to Cart`. 对于B2B商家，店面活动还捕获 [申请列表](<https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html>).
* **后台活动**：捕获有关订单状态的信息，例如订单已下达、已取消、已退款、已发运或已完成。

>[!NOTE]
>
>Adobe Commerce中捕获的数据不包括个人身份信息(PII)。 所有用户标识符（如Cookie ID和IP地址）均严格进行匿名处理。

## 先决条件

要将Adobe Commerce连接到Experience Platform，您必须具备以下条件：

* Adobe Commerce 2.4.3或更高版本。
* 有效的Adobe ID和组织ID。
* 访问 [Adobe客户端数据层扩展](../../../tags/extensions/client/client-data-layer/overview.md). 此扩展是收集店面事件数据所必需的。
* 对其他AdobeDX产品的权利。

## 载入步骤

要全面载入您的Adobe Commerce源帐户，请按照下面列出的步骤及其相应文档进行操作。

* [安装Experience Platform连接器扩展](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/install.html) 适用于Adobe Commerce的。 可以从以下位置下载连接器扩展 [Adobe市场](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html).
* 成功安装Connector扩展后，请在Experience Cloud中登录到您的Adobe帐户并 [确认您的组织ID](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=en#concept_EA8AEE5B02CF46ACBDAD6A8508646255). 此ID与您配置的Experience Cloud公司关联。 其格式为24个字符的数字字母字符串，并包含一个必填项 `@AdobeOrg`.
* 接下来，使用特定于Commerce的字段组创建或更新您的Experience Data Model (XDM)架构。 有关如何将特定于Commerce的字段组添加到XDM架构的详细步骤，请阅读 [将字段组添加到XDM架构](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html).
* 配置架构后，您必须根据新架构创建数据集。 然后，此数据集将包含 [!DNL Commerce] 您发送的数据。 有关如何为创建数据集的 [!DNL Commerce] 数据，请阅读指南 [向Experience Platform发送数据](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=en#create-a-dataset).
* 接下来，创建一个数据流，并选择包含特定于商务的字段组的XDM架构。 有关数据流的详细信息，请参阅 [数据流概述](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html).
* 然后，您必须将Adobe Commerce实例连接到 [商务服务连接器](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html). 这允许将您的Commerce实例部署为SaaS（软件即服务）。
* 完成上述所有配置后，您现在可以使用配置Commerce Services Connector和Experience Platform连接器来连接到Experience Platform。 [!DNL Commerce Admin]. 有关此最后步骤的更多信息，请阅读以下指南： [将Commerce数据连接到Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/connect-data.html).