---
title: Adobe Commerce Source Connector
description: 了解如何使用Adobe Commerce源将您的商业数据引入到Experience Platform。
last-substantial-update: 2023-12-13T00:00:00Z
exl-id: 8313e3d5-5c3d-448c-883c-b9386dbbb2f5
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Adobe Commerce

Adobe Commerce是一个敏捷的B2B和B2C商务平台，使商家和品牌能够通过在线和物理空间提供的以客户为中心的数字商务体验来加快收入增长。

Adobe Experience Platform源支持集成Adobe Commerce，以允许商家将店面和后台数据发送到Experience Platform Edge Network，以便其他Adobe Experience Cloud产品(如Adobe Analytics和Adobe Target)可以使用[!DNL Commerce]数据。

* **店面事件**：捕获购物者交互，如`View Page`、`View Product`和`Add to Cart`。 对于B2B商家，店面活动还捕获[申请列表](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html?lang=zh-Hans)。
* **后台事件**：捕获有关订单状态的信息，例如订单是否已下达、取消、退款、已发运或已完成。

>[!NOTE]
>
>Adobe Commerce中捕获的数据不包括个人身份信息(PII)。 所有用户标识符（如Cookie ID和IP地址）都经过严格匿名处理。

## 先决条件

要将Adobe Commerce连接到Experience Platform，您必须具备以下条件：

* Adobe Commerce 2.4.3或更高版本。
* 有效的Adobe ID和组织ID。
* 访问[Adobe客户端数据层扩展](../../../tags/extensions/client/client-data-layer/overview.md)。 此扩展是收集店面事件数据所必需的。
* 对其他Adobe DX产品的权限。

## 载入步骤

要全面载入您的Adobe Commerce源帐户，请按照下面列出的步骤及其相应文档进行操作。

* [安装Adobe Commerce的 [!DNL Data Connection] 扩展](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html?lang=zh-Hans)。 您可以从[Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html)下载连接器扩展。
* 成功安装连接器扩展后，请在Experience Cloud中登录到您的Adobe帐户并[确认您的组织ID](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=zh-Hans#concept_EA8AEE5B02CF46ACBDAD6A8508646255)。 此ID与您的预配Experience Cloud公司关联。 其格式为24个字符的数字字母字符串，并包含必需的`@AdobeOrg`。
* 接下来，使用特定于Commerce的字段组创建或更新您的体验数据模型(XDM)架构。 有关如何将特定于Commerce的字段组添加到XDM架构的详细步骤，请阅读有关[将字段组添加到XDM架构](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html?lang=zh-Hans)的指南。
* 配置架构后，您必须根据新架构创建数据集。 然后，此数据集将包含您发送的[!DNL Commerce]数据。 有关如何为[!DNL Commerce]数据创建数据集的详细步骤，请阅读有关[将数据发送到Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=zh-Hans#create-a-dataset)的指南。
* 接下来，创建一个数据流并选择包含您的Commerce特定字段组的XDM架构。 有关数据流的详细信息，请阅读[数据流概述](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=zh-Hans)。
* 然后，您必须将Adobe Commerce实例连接到[Commerce服务连接器](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html?lang=zh-Hans)。 这允许将您的Commerce实例部署为SaaS（软件即服务）。
* 完成上述所有配置后，您现在可以通过使用[!DNL Data Connection]配置Experience Platform服务连接器和[!DNL Commerce Admin]扩展来连接到Commerce。 有关此最终步骤的更多信息，请阅读有关[将Commerce数据连接到Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html?lang=zh-Hans)的指南。
