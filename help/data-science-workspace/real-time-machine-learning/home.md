---
keywords: Experience Platform；开发人员指南；数据科学工作区；热门主题；实时机器学习；
solution: Experience Platform
title: 实时机器学习概述
topic: 概述
description: 实时机器学习可以显着增强您的数字体验内容对最终用户的相关性。 通过在Experience Edge上利用实时参考和持续学习，可以实现这一点。
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---


# 实时机器学习概述(Alpha)

>[!IMPORTANT]
>
>尚未向所有用户提供实时机器学习。 此功能位于alpha中，仍在测试中。 此文档可能会更改。

实时机器学习可以显着增强您的数字体验内容对最终用户的相关性。 通过在[!DNL Experience Edge]上利用实时干预和持续学习，这是可能的。

在集线器和[!DNL Edge]上进行无缝计算的组合，可显着减少过去在为个性化体验提供相关和响应式服务时所涉及的延迟。 因此，实时机器学习为同步决策提供了极低的延迟。 示例包括呈现个性化网页内容或呈现优惠或折扣，以减少客户流失和提高网店转化率。

## 实时机器学习架构{#architecture}

下图提供了实时机器学习体系结构的概述。 目前，Alpha有更简化的版本。

![阿尔法](../images/rtml/alpha-arch.png)

![简化的概述](../images/rtml/end-to-end-arch.png)

## 实时机器学习工作流程

以下工作流程概述了创建和利用实时机器学习模型时涉及的典型步骤和结果。

### 数据获取和准备

在Adobe Experience Platform上使用[!DNL Experience Data Model](XDM)摄取并转换数据。 此数据用于模型培训。 要了解有关XDM的更多信息，请访问[XDM概述](../../xdm/home.md)。

### 创作

通过从头开始创作或将其作为Adobe Experience Platform Jupyter Notebooks中经过预先培训的序列化ONNX模型引入，创建实时机器学习模型。

### 部署

将模型部署到[!DNL Experience Edge]，以使用预测API端点在[!UICONTROL 服务库]中创建实时机器学习服务。

### 推理

使用Prediction REST API端点实时生成机器学习洞察。

### 投放

然后，营销人员可以定义细分和规则，将实时机器学习得分与使用Adobe Target的体验相对应。 这允许访客实时展示品牌网站的相同或下一页高度个性化体验。

## 当前功能

实时机器学习目前采用alpha。 随着更多功能和节点可用，下面概述的功能可能会发生更改。

>[!NOTE]
>
> Alpha限制：
> - 目前，仅支持基于ONNX的模型。
> - 无法序列化节点中使用的函数。 例如，在Pacnots节点中使用的lambda函数。
> - 手动完成[!DNL Edge]部署后有20秒的睡眠。
> - 要进行深入学习，您需要以这样的方式发送数据：调用`df.values`时，它会返回一个DL模型可接受的阵列。 这是因为ONNX模型评分节点使用`df.values`并发送输出以对模型进行评分。



### 功能:

|  | Alpha（5月） |
| --- | --- |
| **功能** |  — 使用RTML笔记本模板，创作、测试和部署自定义机器学习模型。 <br>  — 支持导入预先培训的机器学习模型。<br>  — 实时机器学习SDK。<br>  — 创作节点的起始集。<br>  — 已部署到Adobe Experience Platform Hub。 |
| **可用性** | 北美洲 |
| **创作节点** | - Pactis <br> - ScikitLearn <br> - ONNXode <br> - Split <br> - ModelUpload <br> - OneHotEncoder |
| **评分运行时间** | ONNX |

## 后续步骤

您可以按照[入门指南](./getting-started.md)开始。 本指南将指导您设置创建实时机器学习模型所需的所有先决条件。

