---
keywords: Experience Platform；主页；热门主题；沙盒；沙盒；测试；测试
solution: Experience Platform
title: 沙盒概述
description: 沙盒是单个Experience Platform实例中的虚拟分区，允许与数字体验应用程序的开发过程无缝集成。
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 0%

---

# 沙盒概述

Adobe Experience Platform旨在丰富全球范围内的数字体验应用程序。 公司通常并行运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署需要，同时确保运营法规遵从性。

为了满足此需求，Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的沙箱，以帮助开发和改进数字体验应用程序。

本文档提供了Experience Platform中沙盒的高级概述。

## 了解沙盒

沙盒是单个Experience Platform实例中的虚拟分区，允许与数字体验应用程序的开发过程无缝集成。 在沙盒内执行的所有内容和操作都仅限于该沙盒，不影响任何其他沙盒。 Experience Platform支持两种沙盒：

* **生产沙盒**：生产沙盒旨在与生产环境中的用户档案一起使用。 Platform允许您创建多个生产沙箱，以便在保持操作隔离的同时为数据提供适当的功能。 此功能允许您为不同的业务线、品牌、项目或区域指定特定的生产沙箱。 生产沙盒支持大量生产配置文件，直到您获得许可为止 [!DNL Profile] 承诺（在所有授权的生产沙箱中累计）。 您有权根据授权使用许可的平均用户档案 [!DNL Profile] （在所有授权的生产沙箱中累计）。
* **开发沙盒**：开发沙盒是一种沙盒，专门用于使用非生产用户档案进行开发和测试。 开发沙盒支持多达10%的许可的非生产用户档案 [!DNL Profile] 承诺（在所有授权的开发沙箱中累计）。 您有权享有：
   * 每个授权的非生产配置文件的平均非生产配置文件丰富度为75 KB（在所有授权的开发沙盒中累加测量）；
   * 每个开发沙盒每天进行一次批量分段作业；
   * 平均120个 [!DNL Profile] API调用，按 [!DNL Profile]，每年（在所有已授权的开发沙盒中累积测量）。

Experience Platform实例支持多个生产和开发沙盒，每个沙盒维护其自身独立的Platform资源库（包括架构、数据集、配置文件等）。 此外，生产和开发沙盒都有一个重置功能，该功能会从沙盒中删除所有客户创建的资源。 开发沙盒无法转换为生产沙盒。

默认Experience Platform许可证总共授予您5个沙盒，您可以将其分类为生产或开发。 您可以额外许可包含10个沙盒的包，最多总共75个沙盒。 这些额外的沙盒可用于创建生产和开发沙盒。 有关更多详细信息，请联系您的组织管理员或您的Adobe销售代表。

最后，默认的生产沙盒是在首次创建组织时创建的第一个生产沙盒。 默认的生产沙盒允许您从Platform摄取或使用数据，以及接受不包含沙盒名称或沙盒ID值的请求。

>[!NOTE]
>
>首次创建沙盒时，沙盒不包含任何数据。 由于每个沙盒都维护其自己的独立数据存储，因此它们还必须独立摄取其数据。

总之，沙盒具有以下优势：

* **应用程序生命周期管理**：创建单独的虚拟环境，以开发和改进数字体验应用程序。
* **项目和品牌管理**：允许多个项目在同一个组织中并行运行，同时提供隔离和访问控制。 未来版本将支持在多个区域部署。
* **灵活的发展生态系统**：以无缝、可扩展且经济高效的方式提供沙盒，用于探索、支持和演示目的。

## 沙盒的访问控制

默认情况下，组织的所有用户都有权访问生产沙盒。 非生产沙箱的访问权限必须由系统管理员、产品管理员或产品配置文件管理员通过 [Adobe Admin Console](https://adminconsole.adobe.com).

要查看、创建、更新或删除非生产沙盒，还必须向用户授予沙盒管理权限。

有关管理沙盒的角色和权限的更多信息，请参阅 [访问控制概述](../access-control/home.md).

## Experience PlatformUI中的沙盒

在 [Experience Platform用户界面](https://platform.adobe.com)，用户可以使用在自己有权访问的沙盒之间切换 **沙盒切换器** 控件。  具有沙盒管理权限的用户还可以访问 **[!UICONTROL 沙盒]** 选项卡，用户可以在其中查看和管理组织的沙箱。 有关如何在UI中使用沙盒的更多信息，请参阅 [沙盒用户指南](ui/overview.md).

## Experience PlatformAPI中的沙盒

调用Experience PlatformAPI时，必须在标头下提供沙盒名称 `x-sandbox-name`. 例如，在调用 [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) 要查看生产沙盒中的所有数据集，沙盒的名称(“prod”)作为API请求中的标头提供：

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

如果 `x-sandbox-name` API调用中未包含，系统将改用默认沙盒。 但是，最佳实践是始终在所有API调用中包含此标头，即使使用默认沙盒时也是如此。 因此，Experience Platform的API文档将 `x-sandbox-name` 作为必需标头。

### 沙盒API

沙盒API允许您使用RESTful API操作管理沙盒。 请参阅 [沙盒开发人员指南](api/overview.md) 有关如何使用API的详细信息，包括格式正确的请求和示例响应。

## 后续步骤

通过阅读本文档，您已了解有关Experience Platform中沙盒的基本概念。 有关如何管理沙箱的详细步骤，请参阅 [用户指南](ui/overview.md) 对于UI或 [开发人员指南](./api/getting-started.md) 用于API。

虽然沙盒是隔离开发团队平台环境的有用工具，但您也可以使用Adobe Admin Console管理更精细的访问控制。 请参阅 [访问控制概述](../access-control/home.md) 了解更多信息。
