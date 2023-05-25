---
keywords: Experience Platform；主页；热门主题；客户属性连接器
solution: Experience Platform
title: 客户属性源连接器概述
description: 了解如何使用API或用户界面将客户属性连接到Adobe Experience Platform
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 10%

---

# 客户属性连接器

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) 通过Experience Cloud，您可以上传从客户关系管理(CRM)数据库中捕获的企业数据。 您可以将数据上传到 Experience Cloud 中的客户属性数据源，然后在 Adobe Analytics 和 Adobe Target 中使用这些数据。

Experience Platform提供摄取支持 [!DNL Customer Attributes] 将数据配置文件导入Adobe Experience Platform。

## 数据集和架构

此 [!DNL Customer Attributes] source会自动创建数据集以供数据登陆到。 此自动创建的数据集是固定的，无法手动选择。 源还会根据输入数据源自动为数据集创建架构。 此过程还包括自动创建架构和源数据之间的必要映射。

## 标识

数据集的主要标识包含在源数据的CSV文件的第一列中。 此 [!DNL Customer Attributes] 源假定身份始终映射到 [`CORE` 命名空间](../../../identity-service/namespaces.md)，系统生成的命名空间，受支持 [[!DNL Identity Service]](../../../identity-service/home.md).

使用时，无法为身份选择现有命名空间 [!DNL Customer Attributes] 源原因 [!DNL Customer Attributes] 假定架构的主要标识始终位于标识映射中。 [!DNL Customer Attributes] 然后，以自动方式创建源ID到身份映射UUID的映射。

对象 [!DNL Customer Attributes] 要与其他关联的数据 [!DNL Profile] 数据集、其数据和身份必须能够与Experience CloudID匹配。

您可以建立 `CORE` 命名空间，方法是使用为访客设置Experience CloudID [Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en)， [移动SDK](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity)，或 [Experience CloudID服务API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=en).

此 [!DNL Customer Attributes] 文件不会进一步填充任何其他身份关系。 例如，如果 [!DNL Customer Attributes] 源数据集包含 **电子邮件** 和 **忠诚度ID** 字段，则这些字段必须标记为架构中的标识字段，才能被处理到 [!DNL Identity Service].

请参阅上的教程 [创建 [!DNL Customer Attributes] UI中的源连接](../../tutorials/ui/create/adobe-applications/customer-attributes.md) 了解更多信息。
