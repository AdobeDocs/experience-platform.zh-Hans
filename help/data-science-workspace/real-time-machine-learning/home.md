---
keywords: Experience Platform；开发人员指南；Data Science Workspace；热门主题；实时机器学习；
solution: Experience Platform
title: 实时机器学习概述
description: 实时机器学习功能可以显着提升数字体验内容与最终用户的相关性。 借助Experience Edge上的实时引荐和持续学习，可实现这一点。
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# 实时机器学习概述(Alpha)

>[!IMPORTANT]
>
>尚未向所有用户提供实时机器学习功能。 此功能位于Alpha中，且仍在测试中。 本文档可能会更改。

实时机器学习功能可以显着提升数字体验内容与最终用户的相关性。 这可以通过利用对的实时参考和持续学习来实现 [!DNL Experience Edge].

在集线器和 [!DNL Edge] 显着减少传统上在为相关和响应式的超级个性化体验提供支持时涉及的延迟。 因此，实时机器学习为同步决策提供具有极低延迟的推论。 示例包括呈现个性化的网页内容或显示优惠或折扣，以减少流失率并提高网店转化率。

## 实时机器学习架构 {#architecture}

下图提供了实时机器学习架构的概述。 目前，Alpha具有更简化的版本。

![阿尔法拱门](../images/rtml/alpha-arch.png)

![简化的概述](../images/rtml/end-to-end-arch.png)

## 实时机器学习工作流

以下工作流概述了创建和利用实时机器学习模型时涉及的典型步骤和结果。

### 数据获取和准备

数据会通过 [!DNL Experience Data Model] (XDM)Adobe Experience Platform。 此数据用于模型培训。 要进一步了解XDM，请访问 [XDM概述](../../xdm/home.md).

### 创作

通过从头开始创作实时机器学习模型，或将其作为Adobe Experience Platform Jupyter Notebooks中经过预先培训的序列化ONNX模型引入，创建实时机器学习模型。

### 部署

将模型部署到 [!DNL Experience Edge] 在 [!UICONTROL 服务库] 使用预测API端点。

### 推理

使用预测REST API端点可实时生成机器学习分析。

### 交付

然后，营销人员可以定义区段和规则，以将实时机器学习得分映射到使用Adobe Target的体验。 这样，品牌网站的访客就可以实时获得相同或下一页的超个性化体验。

## 当前功能

“实时机器学习”目前为alpha版。 随着提供更多特性和节点，下面概述的功能可能会发生更改。

>[!NOTE]
>
> Alpha限制：
> - 目前，仅支持基于ONNX的模型。
> - 无法序列化节点中使用的函数。 例如，在Pantics节点中使用的lambda函数。
> - 20秒后就睡了 [!DNL Edge] 部署是手动完成的。
> - 要进行深入学习，需要以如下方式发送数据： `df.values` 称为，它将返回DL模型可接受的阵列。 这是因为ONNX模型评分节点使用 `df.values` 并发送输出以根据模型进行评分。



### 功能:

|  | Alpha（5月） |
| --- | --- |
| **功能** |  — 使用RTML笔记本模板，创作、测试和部署自定义机器学习模型。 <br>  — 支持导入预先培训的机器学习模型。 <br>  — 实时机器学习SDK。 <br>  — 创作节点的起始集。 <br>  — 部署到Adobe Experience Platform中心。 |
| **可用性** | 北美洲 |
| **创作节点** |  — 熊猫 <br> - ScikitLearn <br> - ONNXNode <br>  — 拆分 <br> - ModelUpload <br> - OneHotEncoder |
| **评分运行时间** | ONNX |

## 后续步骤

您可以首先按照 [入门](./getting-started.md) 的双曲余切值。 本指南将指导您完成为创建实时机器学习模型设置所有必需的先决条件。
