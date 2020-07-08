---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 沙箱概述
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---


# 沙箱概述

Adobe Experience Platform旨在在全球范围内丰富数字体验应用程序。 公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署的需要，同时确保操作合规性。

In order to address this need, Experience Platform provides **sandboxes** which partition a single Platform instance into separate virtual environments to help develop and evolve digital experience applications.

此文档提供Experience Platform中沙箱的高级概述。

## 了解沙箱

沙箱是单个Experience Platform实例中的虚拟分区，它允许与数字体验应用程序的开发过程无缝集成。 一个Experience Platform实例支持一个生产沙箱和多个非生产沙箱，每个沙箱都维护自己独立的平台资源库(包括模式、数据集、用户档案等)。  在沙箱内执行的所有内容和操作仅限于该沙箱，不会影响任何其他沙箱。

非生产沙箱允许您测试功能、运行实验并制作自定义配置，而不会影响您的生产沙箱。 此外，非生产沙箱还具有重置功能，可从沙箱中删除所有客户创建的资源。 非生产沙箱无法转换为生产沙箱。

>[!NOTE]
>
>首次创建沙箱时，它不包含任何数据。 由于每个沙箱都维护其自己的独立数据存储，因此它们还必须独立地摄取其数据。

总之，沙箱具有以下优点：

* **应用程序生命周期管理**: 创建单独的虚拟环境，开发和改进数字体验应用程序。
* **项目和品牌管理**: 允许在同一IMS组织内并行运行多个项目，同时提供隔离和访问控制。 未来版本将支持在多个地区进行部署。
* **灵活的开发生态系统**: 以无缝、可扩展且经济有效的方式提供沙箱，用于探索、支持和演示。

## 沙箱访问控制

默认情况下，组织的所有用户都有权访问生产沙箱。 对非生产沙箱的访问权限必须由系统管理员、产品管理员或产品用户档案管理员通过AdobeAdmin Console [授予](https://adminconsole.adobe.com)。

要视图、创建、更新或删除非生产沙箱，用户还必须获得“沙箱管理”权限。

有关管理沙箱角色和权限的更多信息，请参阅 [访问控制概述](../access-control/home.md)。

## Experience PlatformUI中的沙箱

在Experience Platform [用户界面中](https://platform.adobe.com)，用户可以使用屏幕左上角的沙箱切换器 **控件** ，在他们可以访问的沙箱之间切换。  具有“沙箱管理”权限的用户还可以访问左 **侧导航** 中的“沙箱”选项卡，在该选项卡中，他们可以视图和管理组织的沙箱。 有关如何在UI中使用沙箱的详细信息，请参阅沙 [箱用户指南](ui/overview.md)。

## Experience PlatformAPI中的沙箱

在调用Experience PlatformAPI时，必须在头下提供沙箱名称 `x-sandbox-name`。 例如，当调用Catalog Service API [来视图](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) “生产”沙箱内的所有数据集时，沙箱的名称(“prod”)将作为API请求中的头提供：

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

如 `x-sandbox-name` 果API调用中不包括，系统将改用默认沙箱。 但是，最佳实践是始终在所有API调用中包含此头，即使使用默认沙箱也是如此。 因此，Experience Platform的API文档将视为 `x-sandbox-name` 必需的标题。

### 沙箱API

沙箱API允许您使用RESTful API操作管理沙箱。 有关如何 [使用API(包括格式正确的请求和示例响应](api/getting-started.md) )的详细信息，请参阅沙箱开发人员指南。

## 后续步骤

通过阅读此文档，您了解了Experience Platform中沙箱的基本概念。 有关如何管理沙箱的详细步骤，请参 [阅UI](ui/overview.md) 用户指南或 [API开发人](./api/getting-started.md) 员指南。

沙箱是为开发团队隔离平台环境的宝贵工具，您还可以使用AdobeAdmin Console管理更精细的访问控制。 有关更多 [信息](../access-control/home.md) ，请参阅访问控制概述。