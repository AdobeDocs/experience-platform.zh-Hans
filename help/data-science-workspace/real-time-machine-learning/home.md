---
keywords: Experience Platform；开发人员指南；数据科学Workspace；热门主题；实时机器学习；
solution: Experience Platform
title: 实时机器学习概述
description: 实时机器学习可以显着增强数字体验内容与最终用户的相关性。 可通过在Experience Platform Edge Network中利用实时推断和持续学习来实现这一点。
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---

# 实时机器学习概述(Alpha)

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

>[!IMPORTANT]
>
>实时机器学习尚未对所有用户可用。 此功能处于Alpha状态，仍在测试中。 此文档可能会发生更改。

实时机器学习可以显着增强数字体验内容与最终用户的相关性。 这是通过在[!DNL Experience Platform Edge Network]上利用实时推断和连续学习实现的。

集线器和[!DNL Edge]上的无缝计算组合可显着减少传统上用于提供相关且响应式超个性化体验的延迟。 因此，实时机器学习为同步决策提供了延迟极短的推断。 例如，呈现个性化的网页内容或提供优惠或折扣，以减少流失并提高Web商店的转化率。

## 实时机器学习架构 {#architecture}

下图提供了实时机器学习架构的概述。 目前，Alpha的版本更加简化。

![阿尔法拱门](../images/rtml/alpha-arch.png)

![简化的概述](../images/rtml/end-to-end-arch.png)

## 实时机器学习工作流程

以下工作流程概述了创建和利用实时机器学习模型所涉及的典型步骤和结果。

### 数据引入和准备

在Adobe Experience Platform上使用[!DNL Experience Data Model] (XDM)引入并转换数据。 此数据用于模型训练。 要了解有关XDM的更多信息，请访问[XDM概述](../../xdm/home.md)。

### 创作

通过从头开始创作实时机器学习模型或在Adobe Experience Platform Jupyter Notebooks中将其作为预先训练的序列化ONNX模型引入来创建。

### 部署

将您的模型部署到[!DNL Edge Network]以使用预测API端点在[!UICONTROL Service Gallery]中创建实时机器学习服务。

### 推断

使用预测REST API端点实时生成机器学习见解。

### 投放

接下来，营销人员可以使用Adobe Target定义区段和规则，将实时机器学习得分映射到体验。 这允许实时向品牌网站的访客显示相同或下一页超个性化体验。

## 当前功能

实时机器学习目前采用阿尔法。 随着更多功能和节点的推出，下面概述的功能可能会发生更改。

>[!NOTE]
>
> Alpha限制：
>
> - 目前，仅支持基于ONNX的模型。
> - 无法序列化节点中使用的函数。 例如，在Pandas节点中使用的lambda函数。
> - 手动完成[!DNL Edge]部署后有20秒睡眠。
> - 对于深度学习，需要以这样一种方式发送数据：在调用`df.values`时，它会返回一个DL模型可以接受的数组。 这是因为ONNX模型评分节点使用`df.values`并发送输出以对该模型评分。


### 功能：

| | Alpha （5月） |
| --- | --- |
| **功能** |  — 使用RTML笔记本模板，创作、测试和部署自定义机器学习模型。 <br> — 支持导入预先训练的机器学习模型。 <br> — 实时机器学习SDK。 <br> — 创作节点的入门集合。 <br> — 部署到Adobe Experience Platform中心。 |
| **可用性** | 北美洲 |
| **创作节点** |  — 熊猫<br> - ScikitLearn <br> - ONNXNode <br> — 拆分<br> - ModelUpload <br> - OneHotEncoder |
| **评分运行时间** | ONX |

## 后续步骤

您可以按照[快速入门](./getting-started.md)指南开始操作。 本指南将指导您完成创建实时机器学习模型所需的所有先决条件的设置。
