---
keywords: Experience Platform；入门；归因ai；热门主题
feature: Attribution AI
title: 快速入门Attribution AI
topic-legacy: Getting started
description: 以下指南需要了解与使用Attribution AI有关的各种Adobe Experience Platform服务。 在开始教程之前，请查阅以下文档。
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: a14f857f87482e1468211152976530c718d56e38
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# Attribution AI入门

以下指南需要了解 [!DNL Adobe Experience Platform] 与使用Attribution AI相关的服务。 在开始教程之前，请查看以下文档：

- [Experience Data Model(XDM)系统概述](../../xdm/home.md):XDM是允许 [!DNL Adobe Experience Cloud]由Experience Platform提供支持，在适当的时间通过适当的渠道向适当的人员提供适当的信息。 构建Experience Platform的方法 — XDM系统，可操作Experience Data Model模式以供Platform服务使用。
- [架构组合的基础知识](../../xdm/schema/composition.md):本文档简要介绍Experience Data Model(XDM)架构，以及组合架构以在 [!DNL Adobe Experience Platform].
- [构建模式](../../xdm/tutorials/create-schema-ui.md):本教程介绍了在Experience Platform中使用架构编辑器创建架构的步骤。

Attribution AI需要数据集才能符合消费者体验事件(CEE)架构，该架构是一种 [体验数据模型(XDM)](../../xdm/home.md) 架构字段组。 要实施或更改此数据，请通过attributionai-support@adobe.com联系Adobe支持。 如果存在媒体支出数据，您可以进行进一步分析，如增加收入和ROI。 如果客户配置文件数据可用，您可以进一步将点数归因于客户配置文件级别。

## 术语

- **转化事件：** 客户为指示目标（如会议注册）的里程碑而进行的任何数字事件或数字交互。 其他示例包括付费转化、免费帐户注册或符合某个特征的条件。

- **接触点：** 客户在实现目标的过程中进行的任何数字事件或数字交互。 示例包括与购买前相关的营销工作、显示已查看的广告展示次数以及付费搜索点击。

## 下载Attribution AI分数

>[!NOTE]
>
>如果您不需要下载原始分数，则可以跳过此步骤并继续 [后续步骤](#next-steps).

下载Attribution AI得分可通过API调用的组合完成。 要调用Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程可为所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对Platform API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关Platform中沙箱的更多信息，请参阅 [沙盒概述文档](../../sandboxes/home.md).

### 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md) (位于Experience Platform疑难解答指南中)。

## 访问控制 {#access-control}

使用基于角色的访问控制时， **查看Attribution AI** 和 **管理Attribution AI** 权限授予对Attribution AI不同功能的访问权限。 的 **管理Attribution AI** 允许您 **创建**, **克隆**, **编辑**, **删除**, **启用**&#x200B;或 **禁用** 实例 **查看Attribution AI** 允许您 **读取** 或 **视图** 它。 的 **创建**, **编辑** 和 **删除** 操作由审核日志记录。

请参阅相关文档以了解 [为访问控制分配权限](../../../help/access-control/home.md) 或如何 [使用审核日志来监控访问和活动](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## 后续步骤 {#next-steps}

准备就绪并部署所有凭据和模式后，请首先按照 [Attribution AI用户界面指南](./user-guide.md). 本指南将指导您创建实例并提交该实例以进行培训和评分。
