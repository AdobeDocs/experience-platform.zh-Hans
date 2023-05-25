---
keywords: Experience Platform；快速入门；归因人工智能；热门主题
feature: Attribution AI
title: Attribution AI快速入门
description: 以下指南要求您了解与使用Attribution AI有关的各种Adobe Experience Platform服务。 在开始教程之前，请查看以下文档。
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# Attribution AI快速入门

以下指南需要了解各种 [!DNL Adobe Experience Platform] 与使用Attribution AI有关的服务。 在开始教程之前，请查看以下文档：

- [Experience Data Model (XDM)系统概述](../../xdm/home.md)：XDM是允许使用以下项操作的基础框架： [!DNL Adobe Experience Cloud](由Experience Platform提供支持)在正确的时间通过正确的渠道向正确的人员传递正确的信息。 构建Experience Platform所基于的方法XDM System可使Experience Data Model架构可操作以供Platform服务使用。
- [模式组合基础](../../xdm/schema/composition.md)：本文档介绍了Experience Data Model (XDM)架构，以及构成要使用的架构的构建基块、原则和最佳实践。 [!DNL Adobe Experience Platform].
- [构建架构](../../xdm/tutorials/create-schema-ui.md)：本教程介绍了在Experience Platform中使用架构编辑器创建架构的步骤。

Attribution AI要求数据集符合使用者体验事件(CEE)架构，该架构是 [体验数据模型(XDM)](../../xdm/home.md) 架构字段组。 请通过attributionai-support@adobe.com联系Adobe支持，以实施或更改此数据。 如果存在媒体支出数据，您可以执行进一步分析，如增量收入和ROI。 如果客户配置文件数据可用，您可以进一步将信用归因于客户配置文件层。

## 术语

- **转化事件：** 客户为指示目标的里程碑而执行的任何数字事件或数字交互，例如会议注册。 其他示例包括付费转化、免费帐户注册或符合某个特征的条件。

- **接触点：** 客户在通往目标的道路上进行的任何数字事件或数字交互。 示例包括与购买前相关的营销工作、显示的已查看广告展示次数和付费搜索点击次数。

## 下载Attribution AI分数

>[!NOTE]
>
>如果您不需要下载原始分数，则可以跳过此步骤并转到 [后续步骤](#next-steps).

下载Attribution AI分数是通过API调用的组合完成的。 要调用Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有Experience PlatformAPI调用中的每个所需标头提供值，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Experience Platform中的所有资源都与特定的虚拟沙盒隔离。 对Platform API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关Platform中沙盒的更多信息，请参阅 [沙盒概述文档](../../sandboxes/home.md).

### 正在读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md) 在Experience Platform疑难解答指南中。

## 访问控制 {#access-control}

使用基于角色的访问控制时， **查看Attribution AI** 和 **管理Attribution AI** 权限授予对Attribution AI各种功能的访问权限。 此 **管理Attribution AI** 允许您 **创建**， **克隆**， **编辑**， **delete**， **启用**，或 **disable** 实例，但 **查看Attribution AI** 允许您 **读取** 或 **视图** 它。 此 **创建**， **编辑** 和 **delete** 操作由审核日志记录。

请参阅文档以了解详情 [为访问控制分配权限](../../../help/access-control/home.md) 或如何 [使用审核日志监控访问和活动](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## 后续步骤 {#next-steps}

准备就绪并准备好所有凭据和架构后，请按照以下步骤开始 [Attribution AI用户界面指南](./user-guide.md). 本指南将指导您完成创建实例并提交实例以进行培训和评分。
