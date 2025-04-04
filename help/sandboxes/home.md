---
keywords: Experience Platform；主页；热门主题；沙盒；沙盒；测试；测试
solution: Experience Platform
title: 沙盒概述
description: 沙盒是Experience Platform单个实例中的虚拟分区，允许与数字体验应用程序的开发过程无缝集成。
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 2%

---

# 沙盒概述

Adobe Experience Platform 旨在丰富全球范围内的数字体验应用。公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署需要，同时确保操作法规遵从性。

为了满足此需求，Experience Platform提供了可将单个Experience Platform实例划分为多个单独的虚拟环境的沙箱，以帮助开发和改进数字体验应用程序。

本文档全面概述了Experience Platform中的沙盒。

## 了解沙盒

沙盒是Experience Platform单个实例中的虚拟分区，允许与数字体验应用程序的开发过程无缝集成。 在沙盒内执行的所有内容和操作仅受该沙盒限制，不会影响任何其他沙盒。 Experience Platform支持两种沙盒：

* **生产沙盒**：生产沙盒应该与生产环境中的用户档案一起使用。 Experience Platform允许您创建多个生产沙盒，以便在保持操作隔离的同时为数据提供适当的功能。 此功能允许您为不同的业务线、品牌、项目或区域指定特定的生产沙箱。 生产沙盒支持大量生产配置文件，最多不超过您的许可[!DNL Profile]承诺（在所有授权的生产沙盒中累积测量）。 您有权使用整个许可的总数据量（在所有授权的生产沙盒中累积测量）。

* **开发沙盒**：开发沙盒是一个沙盒，可专门用于开发和测试非生产配置文件。 开发沙盒支持大量非生产配置文件，最多占您许可的[!DNL Profile]承诺的10%（在所有授权的开发沙盒中累积测量）。 您有权获得以下权限：
   * 每个开发沙盒每天一个批量分段作业；
   * 每[!DNL Profile]年平均120次[!DNL Profile] API调用（在所有授权的开发沙盒中累积测量）。

Experience Platform实例支持多个生产和开发沙盒，每个沙盒维护其自身的Experience Platform资源（包括架构、数据集、配置文件等）独立库。 此外，生产和开发沙盒都具有重置功能，可从沙盒中删除所有客户创建的资源。 无法将开发沙盒转换为生产沙盒。

默认的Experience Platform许可证总共授予您5个沙盒，您可以将其分类为生产或开发。 您可以额外许可包含10个沙盒的包，最多总共75个沙盒。 这些额外的沙盒可用于创建生产和开发沙盒。 有关更多详细信息，请联系您的组织管理员或Adobe销售代表。

最后，默认的生产沙盒是在首次创建组织时创建的第一个生产沙盒。 默认的生产沙盒允许您从Experience Platform摄取或使用数据，以及接受不包含沙盒名称或沙盒ID值的请求。

>[!NOTE]
>
>首次创建沙盒时，沙盒不包含任何数据。 由于每个沙盒都维护其自己的独立数据存储，因此它们还必须独立摄取其数据。

总之，沙盒具有以下优势：

* **应用程序生命周期管理**：创建单独的虚拟环境以开发和改进数字体验应用程序。
* **项目和品牌管理**：允许在同一组织内并行运行多个项目，同时提供隔离和访问控制。
* **灵活的开发生态系统**：以无缝、可扩展且经济实惠的方式提供沙盒，用于探索、启用和演示目的。

## 沙盒访问控制

默认情况下，组织的所有用户都有权访问生产沙盒。 非生产沙盒的访问必须由系统管理员、产品管理员或产品配置文件管理员通过[Adobe Admin Console](https://adminconsole.adobe.com)授予。

要查看、创建、更新或删除非生产沙盒，还必须向用户授予沙盒管理权限。

有关管理沙盒的角色和权限的详细信息，请参阅[访问控制概述](../access-control/home.md)。

## Experience Platform UI中的沙盒

在[Experience Platform用户界面](https://platform.adobe.com)中，用户可以使用屏幕左上角的&#x200B;**沙盒切换器**&#x200B;控件在它们有权访问的沙盒之间切换。  具有沙盒管理权限的用户还可以访问左侧导航中的&#x200B;**[!UICONTROL 沙盒]**&#x200B;选项卡，他们可以在其中查看和管理组织的沙盒。 有关如何在UI中使用沙盒的更多信息，请参阅[沙盒用户指南](ui/overview.md)。

## Experience Platform API中的沙盒

调用Experience Platform API时，必须在标头`x-sandbox-name`下提供沙盒名称。 例如，在调用[[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/)以查看生产沙盒内的所有数据集时，沙盒的名称(“prod”)作为API请求中的标头提供：

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

如果API调用中未包含`x-sandbox-name`，则系统将改用默认沙盒。 但是，最佳实践是在所有API调用中始终包含此标头，即使使用默认沙盒时也是如此。 因此，Experience Platform的API文档将`x-sandbox-name`视为必需的标头。

### 沙盒API

沙盒API允许您使用RESTful API操作管理沙盒。 有关如何使用API的详细信息（包括格式正确的请求和示例响应），请参阅[沙盒开发人员指南](api/overview.md)。

## 后续步骤

通过阅读本文档，您已了解有关Experience Platform中沙盒的基本概念。 有关如何管理沙盒的详细步骤，请参阅UI的[用户指南](ui/overview.md)或API的[开发人员指南](./api/getting-started.md)。

虽然沙盒是一种用于为开发团队隔离Experience Platform环境的有用工具，但您也可以使用Adobe Admin Console管理更精细的访问控制。 有关详细信息，请参阅[访问控制概述](../access-control/home.md)。
