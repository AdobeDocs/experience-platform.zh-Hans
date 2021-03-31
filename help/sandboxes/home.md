---
keywords: Experience Platform；主页；热门主题；沙箱；沙箱；测试；测试
solution: Experience Platform
title: 沙箱概述
topic: 概述
description: 沙箱是Experience Platform单个实例中的虚拟分区，它允许与数字体验应用程序的开发过程无缝集成。
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 0%

---


# 沙箱概述

Adobe Experience Platform旨在在全球范围内丰富数字体验应用程序。 公司经常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署的需要，同时确保操作合规性。

为了满足这一需求，Experience Platform提供了沙箱，可将单个平台实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

此文档提供Experience Platform中沙箱的高级概述。

## 了解沙箱

>[!NOTE]
>
>“多个制作沙箱”功能是测试版。

沙箱是Experience Platform单个实例中的虚拟分区，它允许与数字体验应用程序的开发过程无缝集成。 Experience Platform实例支持多个生产和非生产沙箱，每个沙箱都维护自己的独立平台资源库(包括模式、数据集、用户档案等)。 在沙箱内执行的所有内容和操作仅限于该沙箱，不影响任何其他沙箱。

非生产沙箱允许您测试功能、运行实验和制作自定义配置，而不会影响您的生产沙箱。 此外，生产沙箱和非生产沙箱都具有重置功能，可从沙箱中删除所有客户创建的资源。 无法将非生产沙箱转换为生产沙箱。 默认Experience Platform许可证授予您五个沙箱（一个生产箱和四个非生产箱）。 您最多可以添加10个沙箱包，最多共添加75个沙箱。 这些附加沙箱可用于创建生产沙箱和非生产沙箱。 有关详细信息，请与IMS组织管理员或Adobe销售代表联系。

>[!NOTE]
>
>首次创建沙箱时，它不包含任何数据。 由于每个沙箱都维护其自己的独立数据存储，因此它们还必须独立收集其数据。

总而言之，沙箱具有以下优点：

* **应用程序生命周期管理**:创建单独的虚拟环境，开发和发展数字体验应用程序。
* **项目和品牌管理**:允许多个项目在同一IMS组织内并行运行，同时提供隔离和访问控制。未来版本将支持在多个地区进行部署。
* **灵活的开发生态系统**:以无缝、可扩展且经济有效的方式提供沙箱，以用于探索、支持和演示。

## 访问控制沙箱

默认情况下，组织的所有用户都可以访问生产沙箱。 对非生产沙箱的访问权限必须由系统管理员、产品管理员或产品用户档案管理员通过[Adobe Admin Console](https://adminconsole.adobe.com)授予。

要视图、创建、更新或删除生产沙箱和非生产沙箱，用户还必须获得沙箱管理权限。

有关管理沙箱的角色和权限的详细信息，请参阅[访问控制概述](../access-control/home.md)。

## Experience PlatformUI中的沙箱

在[Experience Platform用户界面](https://platform.adobe.com)中，用户可以使用屏幕左上角的&#x200B;**沙箱切换器**&#x200B;控件在他们可以访问的沙箱之间切换。  具有“沙箱管理”权限的用户还可以访问左侧导航中的&#x200B;**[!UICONTROL Sandboxes]**&#x200B;选项卡，在该选项卡中，他们可以视图和管理组织的沙箱。 有关如何在UI中使用沙箱的详细信息，请参阅[沙箱用户指南](ui/overview.md)。

## Experience PlatformAPI中的沙箱

在调用Experience Platform API时，必须在标头`x-sandbox-name`下提供沙箱名称。 例如，当调用[[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)以视图生产沙箱内的所有数据集时，沙箱的名称(&quot;prod&quot;)将作为API请求中的标头提供：

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

如果API调用中未包含`x-sandbox-name`，则系统将改用默认沙箱。 但是，最佳实践是始终在所有API调用中包含此标头，即使使用默认沙箱也是如此。 因此，Experience Platform的API文档将`x-sandbox-name`视为必需标头。

### 沙箱API

沙箱API允许您使用RESTful API操作管理沙箱。 请参见[沙箱开发人员指南](api/getting-started.md)，了解有关如何使用API的详细信息，包括格式正确的请求和示例响应。

## 后续步骤

通过阅读此文档，您了解了关于沙箱在Experience Platform中的基本概念。 有关如何管理沙箱的详细步骤，请参阅UI的[用户指南](ui/overview.md)或API的[开发人员指南](./api/getting-started.md)。

沙箱是为您的开发团队隔离平台环境的有用工具，您还可以使用Adobe Admin Console管理更精细的访问控制。 有关详细信息，请参阅[访问控制概述](../access-control/home.md)。