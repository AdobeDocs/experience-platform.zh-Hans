---
keywords: Experience Platform；主页；热门主题；客户属性连接器
solution: Experience Platform
title: 客户属性来源连接器概述
topic-legacy: overview
description: 了解如何使用API或用户界面将客户属性连接到Adobe Experience Platform
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 541cc87f218a6ef3dcca37573f6d0f9cf560edfb
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 8%

---

# 客户属性连接器

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) 在Experience Cloud中，您可以上传从客户关系管理(CRM)数据库中捕获的企业数据。您可以将数据上传到 Experience Cloud 中的客户属性数据源，然后在 Adobe Analytics 和 Adobe Target 中使用这些数据。

Experience Platform支持将[!DNL Customer Attributes]配置文件数据摄取到Adobe Experience Platform。

## 数据集和架构

[!DNL Customer Attributes]源会自动创建数据集，以便数据登陆。 此自动创建的数据集已修复，无法手动选择。 该源还会根据输入数据源自动为数据集创建架构。 此过程还涉及自动创建架构与源数据之间的必需映射。

## 标识

数据集的主标识包含在源数据CSV文件的第一列中。 [!DNL Customer Attributes]源假定标识始终映射到[`CORE`命名空间](../../../identity-service/namespaces.md)，该命名空间是系统生成的命名空间，受[[!DNL Identity Service]](../../../identity-service/home.md)支持。

使用[!DNL Customer Attributes]源时，您无法为标识选择现有的命名空间，因为[!DNL Customer Attributes]假定架构的主标识始终位于标识映射中。 [!DNL Customer Attributes] 然后，以自动方式创建源ID到身份映射UUID的映射。

要使[!DNL Customer Attributes]数据与其他[!DNL Profile]数据集关联，其数据和身份必须能够与Experience CloudID匹配。

您可以使用[Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en)、[Mobile SDK](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity)或[Experience CloudID服务API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hans)为访客设置Experience CloudID，以建立`CORE`命名空间。

[!DNL Customer Attributes]文件不会进一步填充任何其他身份关系。 例如，如果[!DNL Customer Attributes]源数据集包含&#x200B;**Email**&#x200B;和&#x200B;**忠诚度ID**&#x200B;字段，则这些字段必须标记为架构中的标识字段，才能处理到[!DNL Identity Service]中。

有关更多信息，请参阅有关在UI](../../tutorials/ui/create/adobe-applications/customer-attributes.md)中创建 [!DNL Customer Attributes] 源连接的教程。[
