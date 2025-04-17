---
keywords: Experience Platform；主页；热门主题；沙盒故障排除
solution: Experience Platform
title: 沙盒疑难解答指南
description: 本文档提供有关Adobe Experience Platform中沙盒的常见问题解答。
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 9%

---

# 沙盒疑难解答指南

本文档提供有关Adobe Experience Platform中沙盒的常见问题解答。 有关其他Experience Platform服务的问题和疑难解答，请参阅[Experience Platform疑难解答指南](../landing/troubleshooting.md)。

沙盒将单个Experience Platform实例划分为单独的虚拟环境，以帮助开发和改进数字体验应用程序。 有关更多信息，请参阅[沙盒概述](home.md)。

## 沙盒是什么？

沙盒是单个 Experience Platform 实例内的虚拟分区。每个沙盒都维护其自身的Experience Platform资源库（包括架构、数据集、配置文件等）。 在沙盒内执行的所有内容和操作仅受该沙盒限制，不会影响任何其他沙盒。 有关更多信息，请参阅[沙盒概述](home.md)。

## 提供了哪些类型的沙盒，它们之间有何差异？ {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="沙盒类型"
>abstract="沙盒类型指示这是生产沙盒还是开发沙盒。生产沙盒包括实时数据，开发沙盒用于测试和开发。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html#create" text="在 UI 中创建沙盒"

Experience Platform中有两种沙盒类型可用：

* **生产沙盒**：生产沙盒应该与生产环境中的用户档案一起使用。 Experience Platform允许您创建多个生产沙盒，以便在保持操作隔离的同时为数据提供适当的功能。 此功能允许您为不同的业务线、品牌、项目或区域指定特定的生产沙箱。 生产沙盒支持大量生产配置文件，最多不超过您的许可[!DNL Profile]承诺（在所有授权的生产沙盒中累积测量）。 您有权使用整个许可的总数据量（在所有授权的生产沙盒中累积测量）。

* **开发沙盒**：开发沙盒是一个沙盒，可专门用于开发和测试非生产配置文件。 开发沙盒支持大量非生产配置文件，最多占您许可的[!DNL Profile]承诺的10%（在所有授权的开发沙盒中累积测量）。 您有权获得以下权限：
   * 每个开发沙盒每天一个批量分段作业；
   * 每[!DNL Profile]年平均120次[!DNL Profile] API调用（在所有授权的开发沙盒中累积测量）。

有关更多信息，请参阅[沙盒概述](./home.md)。

## 我是否可以从多个沙盒访问资源？

沙盒是单个Experience Platform实例的独立分区，每个沙盒维护其自己的独立资源库。 无论沙盒类型（生产或非生产）如何，都无法从任何其他沙盒访问存在于一个沙盒中的资源。

## 默认的生产沙盒是什么？

默认的生产沙盒是在首次配置组织时创建的第一个生产沙盒。 默认的生产沙盒允许您从Experience Platform摄取或使用数据，以及接受不包含沙盒名称或沙盒ID值的请求。 默认的生产沙盒可以重置，但不能删除。

## 我可以拥有多少个生产沙盒？

Experience Platform实例支持多个生产和开发沙盒，每个沙盒维护其自身的Experience Platform资源（包括架构、数据集和配置文件）独立库。

默认的Experience Platform许可证总共授予您5个沙盒，您可以将其分类为生产或开发。 您可以额外许可包含10个沙盒的包，最多总共75个沙盒。

生产沙盒可以重置或删除，但Adobe Analytics也将其用于[Cross Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html)功能，或者其中托管的身份图形也被Adobe Audience Manager用于[基于人员的目标(PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html)功能除外。

您可以更新生产沙盒的标题。 但是，无法重命名生产沙盒。

>[!NOTE]
>
>沙盒名称用于在API调用中查找，而沙盒标题用作显示名称。

## 我可以拥有多少个开发沙盒？

目前，Experience Platform最多允许在一个组织内有75个沙盒（生产和开发）处于活动状态。

开发沙盒支持重置和删除功能。

## 我刚刚创建了一个沙盒。 如何为将使用此沙盒的用户设置权限？

Adobe Admin Console通过使用产品配置文件将用户链接到沙盒和权限。 创建新沙盒后，导航到要授予访问权限的产品配置文件的&#x200B;**权限**&#x200B;选项卡，然后单击&#x200B;**沙盒**。 在此，您可以按照与其他权限相同的方式添加新沙盒或删除对新沙盒的访问权限。

如果您希望向特定沙盒的用户添加唯一权限，您可能需要使用应用的相应沙盒和权限创建新的产品配置文件，并将这些用户分配给该配置文件。

有关在Admin Console中管理沙盒和权限的更多信息，请参阅[访问控制用户指南](../access-control/ui/overview.md)。
