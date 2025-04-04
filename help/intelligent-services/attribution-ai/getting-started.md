---
keywords: Experience Platform；快速入门；归因人工智能；热门主题
feature: Attribution AI
title: Attribution AI入门
description: 以下指南需要了解与使用归因人工智能有关的各种Adobe Experience Platform服务。 在开始教程之前，请查看以下文档。
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 6%

---

# Attribution AI入门

以下指南需要了解与使用归因人工智能有关的各种[!DNL Adobe Experience Platform]服务。 在开始教程之前，请查看以下文档：

- [体验数据模型(XDM)系统概述](../../xdm/home.md)： XDM是一个基础框架，它允许[!DNL Adobe Experience Cloud]在正确的时间通过正确的渠道向正确的人员传递正确的消息，该框架由Experience Platform提供支持。 构建Experience Platform所基于的方法XDM系统可使Experience Data Model架构可操作以供Experience Platform服务使用。
- [架构组合的基础知识](../../xdm/schema/composition.md)：本文档介绍了体验数据模型(XDM)架构以及用于组合要在[!DNL Adobe Experience Platform]中使用的架构的构建块、原则和最佳实践。
- [构建架构](../../xdm/tutorials/create-schema-ui.md)：本教程介绍了在Experience Platform中使用“架构编辑器”创建架构的步骤。

归因人工智能要求数据集符合使用者体验事件(CEE)架构，它是[体验数据模型(XDM)](../../xdm/home.md)架构字段组。 请通过attributionai-support@adobe.com联系Adobe支持，以实施或更改此数据。 如果存在媒体支出数据，您可以执行进一步分析，如增加收入和ROI。 如果客户配置文件数据可用，则您可以将信用进一步归因于客户配置文件层。

## 术语

- **转化事件：**&#x200B;客户为指示目标的里程碑而执行的任何数字事件或数字交互，如会议注册。 其他示例包括付费转化、免费帐户注册或符合某个特征的条件。

- **接触点：**&#x200B;客户在实现目标的过程中进行的任何数字活动或数字交互。 例如，与购买前相关的营销工作、展示已查看的广告展示次数和付费搜索点击次数。

## 下载Attribution AI分数

>[!NOTE]
>
>如果您不需要下载原始得分，则可以跳过此步骤，继续执行[后续步骤](#next-steps)。

下载归因人工智能得分是通过API调用的组合完成的。 要调用Experience Platform API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

Experience Platform中的所有资源都被隔离到特定的虚拟沙盒中。 对Experience Platform API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关Experience Platform中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

### 正在读取示例 API 调用

本指南提供了示例 API 调用来演示如何格式化请求。这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md)的部分。

## 访问控制 {#access-control}

使用基于角色的访问控制时，**查看归因人工智能**&#x200B;和&#x200B;**管理归因人工智能**&#x200B;权限授予对归因人工智能不同功能的访问权限。 **管理归因人工智能**&#x200B;允许您&#x200B;**创建**、**克隆**、**编辑**、**删除**、**启用**&#x200B;或&#x200B;**禁用**&#x200B;实例，而&#x200B;**查看归因人工智能**&#x200B;允许您&#x200B;**读取**&#x200B;或&#x200B;**查看**&#x200B;实例。 审核日志记录了&#x200B;**创建**、**编辑**&#x200B;和&#x200B;**删除**&#x200B;操作。

请参阅文档以了解[为访问控制](../../../help/access-control/home.md)分配权限，或如何[使用审核日志来监视访问和活动](../../../help/landing/governance-privacy-security/audit-logs/overview.md)。

## 后续步骤 {#next-steps}

准备好并准备好所有凭据和架构后，请按照[归因人工智能用户界面指南](./user-guide.md)开始。 本指南将指导您如何创建实例并提交它以进行培训和评分。
