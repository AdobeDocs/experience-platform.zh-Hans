---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: 实时机器学习概述
topic: Overview
translation-type: tm+mt
source-git-commit: 8f9454730e3bab451ac75070fcd1623698df9196
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 1%

---


# 实时机器学习概述(Alpha)

>[!IMPORTANT]
>尚未向所有用户提供实时机器学习。 此功能在alpha中，仍在测试中。 此文档可能会更改。

实时机器学习可以显着增强您的数字体验内容对最终用户的相关性。 通过在Experience Edge上利用实时参考和持续学习，可以实现这一点。

在集线器和边缘上的无缝计算相结合可显着减少过去在为超级个性化体验提供相关性和响应性方面所涉及的延迟。 因此，实时机器学习为同步决策提供了极低延迟的推理。 示例包括呈现个性化网页内容或呈现优惠或折扣，以减少客户流失并提高网店转化率。

## 实时机器学习架构 {#architecture}

下图提供了实时机器学习体系结构的概述。 目前，alpha具有更简化的版本。

![α拱](../images/rtml/alpha-arch.png)

![简化的概述](../images/rtml/end-to-end-arch.png)

## 实时机器学习工作流程

以下工作流概述了创建和利用实时机器学习模型时涉及的典型步骤和结果。

### 数据获取和准备

借助Adobe Experience Platform上的体验数据模型(XDM)，数据被摄取并转换。 此数据用于模型培训。 要进一步了解XDM，请访 [问XDM概述](../../xdm/home.md)。

### 创作

通过从头开始创作实时机器学习模型，或在Adobe Experience Platform Jupyter笔记本中将其作为经过预先培训的序列化ONNX模型引入，创建实时机器学习模型。

### 部署

将您的模型部署到Experience Edge以使用预测API端点在服务库中创建实时机器学习服务。

### 推理

使用Prediction REST API端点实时生成机器学习洞察。

### 投放

然后，营销人员可以定义将实时机器学习得分与使用Adobe目标的体验相对应的细分和规则。 这允许访客品牌网站实时显示相同或下一页的超个性化体验。

## 当前功能

实时机器学习目前采用alpha。 随着更多功能和节点的可用，以下概述的功能可能会发生更改。

>[!NOTE]
> Alpha限制：
> - 目前，仅支持基于ONNX的模型。
> - 节点中使用的函数无法序列化。 例如，在Pacnots节点中使用的lambda函数。
> - 手动完成Edge部署后有60秒的睡眠时间。
> - 要进行深入学习，您需要以一种方式发送数据，即 `df.values` 在调用数据时，它返回一个DL模型可以接受的阵列。 这是因为ONNX模型评分节点使用 `df.values` 并发送输出以对模型进行评分。



### 功能:

|  | Alpha（5月） |
| --- | --- |
| **功能** | -使用RTML笔记本模板，创作、测试和部署自定义机器学习模型。 <br> -支持导入预先培训的机器学习模型。 <br> -实时机器学习SDK。 <br> -创作节点的起始集。 <br> -已部署到Adobe Experience Platform Hub。 |
| **可用性** | 北美洲 |
| **创作节点** | - Apnotics <br> - ScikitLearn <br> - ONNXode <br> - Split <br> - ModelUpload <br> - OneHotEncoder |
| **评分运行时间** | ONNX |

## 后续步骤

您可以按照入门指 [南开始](./getting-started.md) 。 本指南将指导您设置创建实时机器学习模型所需的所有先决条件。

