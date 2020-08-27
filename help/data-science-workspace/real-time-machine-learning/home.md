---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: 实时机器学习概述
topic: Overview
description: 实时机器学习可以显着增强您的数字体验内容对最终用户的相关性。 通过在Experience Edge上利用实时参考和持续学习，可以实现这一点。
translation-type: tm+mt
source-git-commit: 9ba229195892245d29fb4f17b9f2e5cd6c6ea567
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---


# 实时机器学习概述(Alpha)

>[!IMPORTANT]
>
>尚未向所有用户提供实时机器学习。 此功能在alpha中，仍在测试中。 此文档可能会更改。

实时机器学习可以显着增强您的数字体验内容对最终用户的相关性。 通过利用实时参考和对Adobe的持续学习，可以实现这一点 [!DNL Experience Edge]。

在集线器和集线器上进行无缝计算的组合 [!DNL Edge] 可显着减少通常用于为超级个性化体验提供相关性和响应性的延迟。 因此，实时机器学习为同步决策提供了极低延迟的推理。 示例包括呈现个性化网页内容或呈现优惠或折扣，以减少客户流失并提高网店转化率。

## 实时机器学习架构 {#architecture}

下图提供了实时机器学习体系结构的概述。 目前，alpha具有更简化的版本。

![α拱](../images/rtml/alpha-arch.png)

![简化的概述](../images/rtml/end-to-end-arch.png)

## 实时机器学习工作流程

以下工作流概述了创建和利用实时机器学习模型时涉及的典型步骤和结果。

### 数据获取和准备

在Adobe Experience Platform，数据被摄取并 [!DNL Experience Data Model] 与(XDM)一起转换。 此数据用于模型培训。 要进一步了解XDM，请访 [问XDM概述](../../xdm/home.md)。

### 创作

通过从头开始创作或作为Adobe Experience PlatformJupyter笔记本中经过预先培训的序列化ONNX模型引入，创建实时机器学习模型。

### 部署

部署您的模 [!DNL Experience Edge] 型，以使用预测API端点在服 [!UICONTROL 务库中] 创建实时机器学习服务。

### 推理

使用Prediction REST API端点实时生成机器学习洞察。

### 投放

然后，营销人员可以定义细分和规则，将实时机器学习得分与使用Adobe Target的体验相对应。 这允许访客品牌网站实时显示相同或下一页的超个性化体验。

## 当前功能

实时机器学习目前采用alpha。 随着更多功能和节点的可用，以下概述的功能可能会发生更改。

>[!NOTE]
>
> Alpha限制：
> - 目前，仅支持基于ONNX的模型。
> - 节点中使用的函数无法序列化。 例如，在Pacnots节点中使用的lambda函数。
> - 手动完成部署后有20 [!DNL Edge] 秒的睡眠时间。
> - 要进行深入学习，您需要以一种方式发送数据，即 `df.values` 在调用数据时，它返回一个DL模型可以接受的阵列。 这是因为ONNX模型评分节点使用 `df.values` 并发送输出以对模型进行评分。



### 功能:

|  | Alpha（5月） |
| --- | --- |
| **功能** | -使用RTML笔记本模板，创作、测试和部署自定义机器学习模型。 <br> -支持导入预先培训的机器学习模型。 <br> -实时机器学习SDK。 <br> -创作节点的起始集。 <br> -部署到Adobe Experience Platform枢纽。 |
| **可用性** | 北美洲 |
| **创作节点** | - Apnotics <br> - ScikitLearn <br> - ONNXode <br> - Split <br> - ModelUpload <br> - OneHotEncoder |
| **评分运行时间** | ONNX |

## 后续步骤

您可以按照入门指 [南开始](./getting-started.md) 。 本指南将指导您设置创建实时机器学习模型所需的所有先决条件。

