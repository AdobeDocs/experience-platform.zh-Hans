---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: 归因AI快速入门
topic: Getting started
translation-type: tm+mt
source-git-commit: 14d47f99f1edd7734245b25b7c39f3a71e7aac50

---


# 归因AI快速入门

以下指南需要了解使用归因AI时涉及的各种Adobe Experience Platform服务。 在开始教程之前，请查看以下文档:

- [体验数据模型(XDM)系统概述](../../xdm/home.md):XDM是基本框架，它允许Adobe Experience Cloud以Experience Platform为后盾，在正确的渠道、恰当的时机向正确的人员提供正确的信息。 构建Experience Platform的方法(XDM System)可操作Experience Data Model模式，供Platform服务使用。
- [模式合成的基础知识](../../xdm/schema/composition.md):本文档介绍了Experience Data Model(XDM)模式，以及构成要在Adobe Experience Platform中使用的模式的构件块、原则和最佳做法。
- [建筑模式](../../xdm/tutorials/create-schema-ui.md):本教程介绍了在Experience Platform中使用模式编辑器创建模式的步骤。

归因AI要求数据集符合消费者体验事件(CEE)模式，该是体验数据模型 [](../../xdm/home.md) (XDM)中的一个混合体。 要实施或更改此数据，请通过attributionai-support@adobe.com与Adobe支持部门联系。 如果存在媒体支出数据，您可以进一步分析，如增加收入和ROI。 如果客户用户档案数据可用，您可以进一步将积分归因到客户用户档案级别。

## 术语

- **转化事件:** 客户为指示目标（如会议注册）的里程碑而进行的任何数字事件或数字交互。 其他示例包括付费转换、免费帐户注册或特征资格鉴定。

- **触点：** 客户在实现目标的过程中进行的任何数字事件或数字交互。 示例包括与购买前相关的营销工作、已查看的展示广告印象和付费搜索点击。

## 访问和查询得分

>[!NOTE] 如果您不需要查询或访问原始分数，可以跳过此步骤并继续阅读用 [户界面指南](./user-guide.md)。

访问和查询归因AI的得分是通过Snowflake完成的。 目前，您需要通过电子邮件将Adobe支持部门发送到attributionai-support@adobe.com，以设置并接收Snowflake的Reader帐户凭据或批量导出原始数据。

在Adobe支持部门处理您的请求后，您将获得Snowflake的Reader帐户URL以及下面的相应凭据：

- 雪花URL
- 用户名
- 密码

## 后续步骤

准备好并准备好所有凭据和模式后，请遵循归因AI用户界面指 [南进行开始](./user-guide.md)。 本指南将指导您逐步创建实例，并提交该实例进行培训和评分。