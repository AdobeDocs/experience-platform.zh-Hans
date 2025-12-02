---
keywords: Experience Platform；主页；热门主题；客户属性连接器
solution: Experience Platform
title: 客户属性Source连接器概述
description: 了解如何使用API或用户界面将客户属性连接到Adobe Experience Platform
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 14%

---

# 客户属性连接器

Adobe Experience Platform 允许从外部源摄取数据，同时让您能够使用 Experience Platform 服务来构建、赋予标签和增强传入数据。您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Cloud中的[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=zh-Hans)允许您上传从客户关系管理(CRM)数据库中捕获的企业数据。 您可以将数据上传到 Experience Cloud 中的客户属性数据源，然后在 Adobe Analytics 和 Adobe Target 中使用这些数据。

Experience Platform支持将[!DNL Customer Attributes]配置文件数据摄取到Adobe Experience Platform。

## 数据集和架构

[!DNL Customer Attributes]源自动创建数据集以供数据登陆到。 此自动创建的数据集是固定的，无法手动选择。 源还会根据输入数据源自动为数据集创建架构。 此过程还涉及在架构和源数据之间自动创建必要的映射。

## 身份标识

数据集的主要标识包含在源数据的CSV文件的第一列中。 [!DNL Customer Attributes]源假定身份始终映射到[`CORE`命名空间](../../../identity-service/features/namespaces.md)，该命名空间是[[!DNL Identity Service]](../../../identity-service/home.md)支持的系统生成的命名空间。

在使用[!DNL Customer Attributes]源时，无法为标识选择现有命名空间，因为[!DNL Customer Attributes]假定架构的主要标识始终在标识映射中。 然后，[!DNL Customer Attributes]以自动方式创建源ID到身份映射UUID的映射。

若要将[!DNL Customer Attributes]数据绑定到其他[!DNL Profile]数据集，其数据和标识必须能够与Experience Cloud ID匹配。

您可以使用`CORE`Web SDK[、](/help/collection/use-cases/identity/id-overview.md)Mobile SDK[或](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/)Experience Cloud ID服务API[为访客设置Experience Cloud ID，以建立](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hans)命名空间。

[!DNL Customer Attributes]文件未进一步填充任何其他标识关系。 例如，如果[!DNL Customer Attributes]源数据集包含&#x200B;**电子邮件**&#x200B;和&#x200B;**忠诚度ID**&#x200B;字段，则这些字段必须在架构中标记为标识字段，才能处理到[!DNL Identity Service]中。

有关详细信息，请参阅有关[在UI [!DNL Customer Attributes] 中创建](../../tutorials/ui/create/adobe-applications/customer-attributes.md)源连接的教程。
