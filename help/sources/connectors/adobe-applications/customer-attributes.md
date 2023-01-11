---
keywords: Experience Platform；主页；热门主题；客户属性连接器
solution: Experience Platform
title: 客户属性来源连接器概述
description: 了解如何使用API或用户界面将客户属性连接到Adobe Experience Platform
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 8%

---

# 客户属性连接器

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) 在Experience Cloud中，您可以上传从客户关系管理(CRM)数据库中捕获的企业数据。 您可以将数据上传到 Experience Cloud 中的客户属性数据源，然后在 Adobe Analytics 和 Adobe Target 中使用这些数据。

Experience Platform支持摄取 [!DNL Customer Attributes] 将用户档案数据导入Adobe Experience Platform。

## 数据集和架构

的 [!DNL Customer Attributes] 源会自动创建数据集以登陆到。 此自动创建的数据集已修复，无法手动选择。 该源还会根据输入数据源自动为数据集创建架构。 此过程还涉及自动创建架构与源数据之间的必需映射。

## 标识

数据集的主标识包含在源数据CSV文件的第一列中。 的 [!DNL Customer Attributes] 源假定标识始终映射到 [`CORE` 命名空间](../../../identity-service/namespaces.md)，系统生成的命名空间，受支持 [[!DNL Identity Service]](../../../identity-service/home.md).

使用 [!DNL Customer Attributes] 源 [!DNL Customer Attributes] 假定架构的主标识始终位于标识映射中。 [!DNL Customer Attributes] 然后，以自动方式创建源ID到身份映射UUID的映射。

对于 [!DNL Customer Attributes] 与其他数据关联 [!DNL Profile] 数据集、其数据和身份必须能够与Experience CloudID匹配。

您可以将 `CORE` 命名空间，方法是使用 [Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en), [Mobile SDK](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity)，或 [Experience CloudID服务API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=en).

的 [!DNL Customer Attributes] 文件不会进一步填充任何其他身份关系。 例如，如果 [!DNL Customer Attributes] 源数据集包含 **电子邮件** 和 **忠诚度ID** 字段，则这些字段必须标记为架构中的标识字段，才能处理到 [!DNL Identity Service].

请参阅 [创建 [!DNL Customer Attributes] UI中的源连接](../../tutorials/ui/create/adobe-applications/customer-attributes.md) 以了解更多信息。
