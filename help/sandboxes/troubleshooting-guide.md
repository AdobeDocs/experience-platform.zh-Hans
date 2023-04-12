---
keywords: Experience Platform；主页；热门主题；沙盒疑难解答
solution: Experience Platform
title: 沙箱疑难解答指南
description: 本文档提供了有关Adobe Experience Platform沙箱的常见问题解答。
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 6%

---

# 沙箱疑难解答指南

本文档提供了有关Adobe Experience Platform沙箱的常见问题解答。 有关其他平台服务的相关问题和疑难解答，请参阅 [Experience Platform疑难解答指南](../landing/troubleshooting.md).

沙盒将单个Platform实例分区为单独的虚拟环境，以帮助开发和改进数字体验应用程序。 请参阅 [沙箱概述](home.md) 以了解更多信息。

## 什么是沙盒？

沙箱是单个Experience Platform实例中的虚拟分区。 每个沙盒都维护着自己独立的Platform资源库（包括模式、数据集、用户档案等）。 在沙盒内执行的所有内容和操作都仅限于该沙盒，不会影响任何其他沙盒。 请参阅 [沙箱概述](home.md) 以了解更多信息。

## 有哪些类型的沙箱可用，它们之间有何区别？ {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="沙盒类型"
>abstract="沙盒类型指示这是生产沙盒还是开发沙盒。生产沙盒包括实时数据，开发沙盒用于测试和开发。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html#create" text="在 UI 中创建沙盒"

Experience Platform中提供了两种沙盒类型：

* **生产沙盒**:生产沙盒用于与生产环境中的用户档案一起使用。 平台允许您创建多个生产沙箱，以便为数据提供正确的功能，同时保持操作隔离。 此功能允许您将特定的生产沙箱专用于不同的业务线、品牌、项目或地区。 生产沙箱可支持大量生产配置文件，具体取决于您获得许可的 [!DNL Profile] 承诺（在所有授权生产沙箱中累计测量）。 您有权按授权使用授权的平均配置文件 [!DNL Profile] （累计测量所有授权生产沙箱）。
* **开发沙盒**:开发沙盒是一个沙盒，专门用于使用非生产用户档案进行开发和测试。 开发沙箱支持大量非生产用户档案，这些用户档案最多占您获得许可的用户档案的10% [!DNL Profile] 承诺（在所有授权开发沙箱中累计测量）。 您最多有权：
   * 每个授权非生产配置文件的平均非生产配置文件丰富度为75 KB（累计测量所有授权开发沙箱）；
   * 每天按开发沙盒执行一次批量分段作业；
   * 平均120 [!DNL Profile] API调用，每个 [!DNL Profile]，每年（累计测量所有授权开发沙箱的数据）。

请参阅 [沙箱概述](./home.md) 以了解更多信息。

## 我能否从多个沙盒访问资源？

沙盒是单个Platform实例的独立分区，每个沙盒都维护其自己的独立资源库。 无论沙盒类型（生产或非生产）如何，都无法从任何其他沙盒访问存在于一个沙盒中的资源。

## 默认的生产沙盒是什么？

默认的生产沙盒是在首次配置组织时创建的第一个生产沙盒。 默认的生产沙盒允许您从Platform中摄取或使用数据，并接受不包含沙盒名称或沙盒ID值的请求。 可以重置默认的生产沙盒，但不能删除。

## 我能有多少个生产沙箱？

一个Experience Platform实例支持多个生产和开发沙箱，每个沙箱都维护自己独立的Platform资源库（包括架构、数据集和配置文件）。

默认的Experience Platform许可证会授予您总共五个沙箱，您可以将其分类为生产或开发。 您可以额外授权包含10个沙箱，最多共授权75个沙箱。

生产沙箱可以重置或删除，但生产沙箱也由Adobe Analytics用于 [跨设备分析(CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) 功能，或者如果在其中托管的身份图表也由Adobe Audience Manager用于 [基于人员的目标(PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html) 功能。

您可以更新生产沙盒的标题。 但是，不能重命名生产沙盒。

>[!NOTE]
>
>沙盒名称用于API调用中的查找目的，而沙盒标题用作显示名称。

## 我可以拥有多少个开发沙箱？

Experience Platform当前允许在单个组织内最多75个沙箱（生产和开发）处于活动状态。

开发沙箱支持重置和删除功能。

## 我刚创建了一个沙盒。 如何为将使用此沙盒的用户设置权限？

Adobe Admin Console通过使用产品配置文件将用户链接到沙箱和权限。 创建新沙盒后，导航到 **权限** 选项卡，然后单击 **沙箱**. 在此，您可以以与其他权限相同的方式添加或删除对新沙盒的访问权限。

如果您希望向特定沙盒的用户添加唯一权限，则可能需要创建应用了相应沙盒和权限的新产品用户档案，并将这些用户分配给该用户档案。

请参阅 [访问控制用户指南](../access-control/ui/overview.md) 有关管理沙箱和Admin Console权限的更多信息。
