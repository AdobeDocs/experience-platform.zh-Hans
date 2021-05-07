---
keywords: Experience Platform；入门；归因ai；热门主题
solution: Experience Platform, Intelligent Services
title: Attribution AI入门
topic-legacy: Getting started
description: 以下指南需要了解与使用Attribution AI相关的各种Adobe Experience Platform服务。 在开始教程之前，请查看以下文档。
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Attribution AI入门

以下指南需要了解与使用Attribution AI相关的各种[!DNL Adobe Experience Platform]服务。 在开始教程之前，请查看以下文档:

- [体验数据模型(XDM)系统概述](../../xdm/home.md):XDM是基本框架，它允 [!DNL Adobe Experience Cloud]许在Experience Platform的支持下，在恰当的时间，在适当的渠道向适当的人提供适当的信息。构建Experience Platform的方法，即XDM系统，可操作由平台服务使用的体验数据模型模式。
- [模式合成的基础](../../xdm/schema/composition.md):本文档介绍了体验数据模型(XDM)模式，以及构建要在中使用的模式的构件、原则和最佳做法 [!DNL Adobe Experience Platform]。
- [构建模式](../../xdm/tutorials/create-schema-ui.md):本教程介绍了在Experience Platform中使用模式编辑器创建模式的步骤。

Attribution AI需要数据集才能符合“消费者体验事件”(CEE)模式，该是“体验数据模型”(XDM)](../../xdm/home.md)“模式”字段组。 [请通过attributionai-support@adobe.com与Adobe支持联系，以实施或更改此数据。 如果存在媒体支出数据，您可以进行进一步的分析，如增加收入和ROI。 如果客户用户档案数据可用，您可以进一步将积分归因到客户用户档案级别。

## 术语

- **转换事件:** 客户为指示目标（如会议注册）的里程碑而进行的任何数字事件或数字交互。其他示例包括付费转换、免费帐户注册或特征资格鉴定。

- **接触点：** 客户在实现目标的过程中进行的任何数字事件或数字互动。示例包括与购买前相关的营销工作、已查看的展示广告印象和付费搜索点击。

## 下载Attribution AI得分

>[!NOTE]
>
>如果您不需要下载原始分数，可以跳过此步骤并继续执行[后续步骤](#next-steps)。

下载Attribution AI分数可通过API调用的组合完成。 要调用平台API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

- 授权：承载`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

Experience Platform中的所有资源都隔离到特定的虚拟沙箱。 对平台API的所有请求都需要一个头，它指定操作将在中进行的沙箱的名称：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>有关平台中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

### 读取示例API调用

本指南提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关文档中用于示例API调用的约定的信息，请参阅Experience Platform疑难解答指南中关于如何读取示例API调用](../../landing/troubleshooting.md)的部分。[

## 后续步骤 {#next-steps}

在您准备就绪并准备好所有凭据和模式后，请按照[Attribution AI用户界面指南](./user-guide.md)进行开始。 本指南将指导您创建一个实例并提交它以进行培训和评分。
