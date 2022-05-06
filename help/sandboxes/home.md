---
keywords: Experience Platform；主页；热门主题；沙盒；沙盒；测试；测试
solution: Experience Platform
title: 沙箱概述
topic-legacy: overview
description: 沙盒是单个Experience Platform实例内的虚拟分区，它允许与数字体验应用程序的开发过程无缝集成。
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 0%

---

# 沙箱概述

Adobe Experience Platform旨在在全球范围内丰富数字体验应用程序。 公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署的需要，同时确保操作合规性。

为了满足这一需求，Experience Platform提供了将单个Platform实例分区为单独虚拟环境的沙盒，以帮助开发和改进数字体验应用程序。

本文档提供沙箱的高级概述Experience Platform。

## 了解沙箱

沙盒是单个Experience Platform实例内的虚拟分区，它允许与数字体验应用程序的开发过程无缝集成。 在沙盒内执行的所有内容和操作都仅限于该沙盒，不会影响任何其他沙盒。 Experience Platform支持两种沙箱：

* **生产沙盒**:生产沙盒用于与生产环境中的用户档案一起使用。 平台允许您创建多个生产沙箱，以便为数据提供正确的功能，同时保持操作隔离。 此功能允许您将特定的生产沙箱专用于不同的业务线、品牌、项目或地区。 生产沙箱可支持大量生产配置文件，具体取决于您获得许可的 [!DNL Profile] 承诺（在所有授权生产沙箱中累计测量）。 您有权按授权使用授权的平均配置文件 [!DNL Profile] （累计测量所有授权生产沙箱）。
* **开发沙盒**:开发沙盒是一个沙盒，专门用于使用非生产用户档案进行开发和测试。 开发沙箱支持大量非生产用户档案，这些用户档案最多占您获得许可的用户档案的10% [!DNL Profile] 承诺（在所有授权开发沙箱中累计测量）。 您最多有权：
   * 每个授权非生产配置文件的平均非生产配置文件丰富度为75 KB（累计测量所有授权开发沙箱）；
   * 每天按开发沙盒执行一次批量分段作业；
   * 平均120 [!DNL Profile] API调用，每个 [!DNL Profile]，每年（累计测量所有授权开发沙箱的数据）。

一个Experience Platform实例支持多个生产和开发沙箱，每个沙箱都维护自己独立的平台资源库（包括架构、数据集、用户档案等）。 此外，生产沙盒和开发沙盒都具有重置功能，可从沙盒中删除客户创建的所有资源。 开发沙箱无法转换为生产沙箱。

默认的Experience Platform许可证会授予您总共五个沙箱，您可以将其分类为生产或开发。 您可以额外授权包含10个沙箱，最多共授权75个沙箱。 这些附加沙箱可用于创建生产和开发沙箱。 有关更多详细信息，请联系您的IMS组织管理员或Adobe销售代表。

最后，默认的生产沙盒是首次创建IMS组织时创建的第一个生产沙盒。 默认的生产沙盒允许您从Platform中摄取或使用数据，并接受不包含沙盒名称或沙盒ID值的请求。

>[!NOTE]
>
>首次创建沙盒时，它不包含任何数据。 由于每个沙盒都维护其自身的独立数据存储，因此它们还必须独立摄取数据。

总之，沙箱具有以下优势：

* **应用程序生命周期管理**:创建单独的虚拟环境以开发和改进数字体验应用程序。
* **项目和品牌管理**:允许多个项目在同一IMS组织内并行运行，同时提供隔离和访问控制。 未来版本将支持在多个地区进行部署。
* **灵活发展生态系统**:以一种无缝、可扩展且经济高效的方式提供沙箱，以用于探索、启用和演示。

## 沙箱的访问控制

默认情况下，组织的所有用户都有权访问生产沙盒。 非生产沙箱的访问权限必须由系统管理员、产品管理员或产品配置文件管理员通过 [Adobe Admin Console](https://adminconsole.adobe.com).

要查看、创建、更新或删除非生产沙箱，还必须向用户授予“沙盒管理”权限。

有关管理沙箱角色和权限的更多信息，请参阅 [访问控制概述](../access-control/home.md).

## Experience PlatformUI中的沙箱

在 [Experience Platform用户界面](https://platform.adobe.com)，用户可以使用 **沙盒切换器** 控件。  具有沙盒管理权限的用户还有权访问 **[!UICONTROL 沙箱]** 选项卡，在该选项卡中，用户可以查看和管理组织的沙箱。 有关如何在UI中使用沙箱的更多信息，请参阅 [沙盒用户指南](ui/overview.md).

## Experience PlatformAPI中的沙箱

调用Experience PlatformAPI时，必须在标题下提供沙盒名称 `x-sandbox-name`. 例如，在对 [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) 要查看“生产”沙盒中的所有数据集，沙盒的名称(“prod”)将作为API请求中的标头提供：

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

如果 `x-sandbox-name` API调用中未包含，则系统将改用默认的沙箱。 但是，最佳实践是始终在所有API调用中包含此标头，即使使用默认沙盒也是如此。 因此，Experience Platform的API文档将提供 `x-sandbox-name` 作为必需标题。

### 沙盒API

沙盒API允许您使用RESTful API操作来管理沙箱。 请参阅 [沙盒开发人员指南](api/overview.md) 有关如何使用API的详细信息，包括格式正确的请求和示例响应。

## 后续步骤

通过阅读本文档，您了解了Experience Platform中沙箱的基本概念。 有关如何管理沙箱的详细步骤，请参阅 [用户指南](ui/overview.md) ，或 [开发人员指南](./api/getting-started.md) ，以用于API。

沙盒是为您的开发团队隔离平台环境的有用工具，但您也可以使用Adobe Admin Console管理更精细的访问控制。 请参阅 [访问控制概述](../access-control/home.md) 以了解更多信息。
