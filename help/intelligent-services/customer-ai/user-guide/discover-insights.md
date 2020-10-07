---
keywords: Experience Platform;insights;customer ai;popular topics
solution: Experience Platform
title: 利用客户人工智能发掘洞察
topic: Discovering insights
description: 作为智能服务的一部分，客户人工智能为营销人员提供了利用Adobe Sensei预测客户下一步行动的能力。 客户AI用于生成定制倾向得分，如大规模客户流失和转化个别用户档案。 这无需将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。
translation-type: tm+mt
source-git-commit: c5e2ea5daf813bf580a11f0182361197e55c6fe8
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 0%

---


# 利用客户人工智能发掘洞察

作为智能服务的一部分，客户人工智能为营销人员提供了利用Adobe Sensei预测客户下一步行动的能力。 客户AI用于生成定制倾向得分，如大规模客户流失和转化个别用户档案。 这无需将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。

此文档可作为参考，用于与智能服务客户人工智能用户界面中的服务实例洞察进行交互。

## 入门指南

为了利用客户人工智能的洞察，您需要有一个运行状态成功的服务实例。 要创建新服务实例，请 [访问配置客户AI实例](./configure.md)。 如果您最近创建了一个服务实例，但它仍在培训和评分，请允许24小时，它才能完成运行。

## 服务实例概述

在UI [!DNL Adobe Experience Platform] 中，单击左 **[!UICONTROL 侧导]** 航中的“服务”。 出现 *服务* 浏览器并显示可用的智能服务。 在客户AI的容器中，单击“ **[!UICONTROL 打开]**”。

![访问实例](../images/insights/navigate-to-service.png)

出现“Customer AI service（客户人工智能服务）”页面。 此页列表客户AI的服务实例并显示相关信息，包括实例的名称、倾向类型、实例的运行频率以及上次更新的状态。

>[!NOTE]
>
>只有已成功完成评分运行的服务实例才具有洞察。

![创建实例](../images/insights/dashboard.png)

单击服务实例名称开始。

![创建实例](../images/insights/click-the-name.png)

接下来，将显示该服务实例的洞察页面，在该页面中您将获得数据的可视化效果。 本指南中将更详细地说明可视化以及您可以如何处理数据。

![设置页面](../images/insights/landing-page.png)


### 服务实例详细信息

有两种方法可视图服务实例详细信息，第一种是仪表板，第二种是服务实例。

要从视图中仪表板详细信息，请单击服务实例容器，避免附加到名称的超链接。 这将打开一个右边栏，其中提供了其他详细信息，如说明、评分频率、预测目标和合格人群。 此外，您还可以通过单击“编辑”或“删除”来选 **[!UICONTROL 择编]** 辑和 **[!UICONTROL 删除实例]**。

![右边栏](../images/insights/success-run.png)

>[!NOTE]
>
>在评分运行失败的事件中，会提供错误消息。 错误消息列在右边栏 *的“上次运行* ”详细信息下，该详细信息仅对失败运行可见。

![失败运行消息](../images/insights/failed-run.png)

视图服务实例的其他详细信息的第二种方法位于洞察页面中。 您可以单 **[!UICONTROL 击右上]** 角的“显示更多”以填充下拉列表。 详细信息列出，如得分定义、创建时间和倾向类型。 有关所列任何属性的详细信息，请访 [问配置客户AI实例](./configure.md)。

![显示更多](../images/insights/landing-show-more.png)

![显示更多](../images/insights/show-more.png)

### 编辑实例

要编辑实例，请单 **[!UICONTROL 击]** 右上导航中的“编辑”。

![单击“编辑”按钮](../images/insights/edit-button.png)

此时会显示编辑对话框，允许您编辑 *实例的* “ *描述”和* “评分频率”。 要确认更改并关闭对话框，请 **[!UICONTROL 单击]** 右下角的“编辑”。

![编辑跨窗格](../images/insights/edit-instance.png)

### 更多操作

“ **[!UICONTROL 更多]** ”操作按钮位于“编辑”旁的右上导 **[!UICONTROL 航中]**。 单击 **[!UICONTROL 更多操作]** ，将打开一个下拉列表，通过该下拉列表可以选择下列操作之一：

- **[!UICONTROL 删除]**:删除实例。
- **[!UICONTROL 访问分数]**:单击 *访问得分* ，将打开一个对话框，其中提供指向客户AI教 [程下载得分的链接](./download-scores.md) ，该对话框还提供进行API调用所需的数据集ID。
- **[!UICONTROL 视图运行历史]**:将显示一个对话框，其中包含与服务实例关联的所有评分运行的列表。

![更多操作](../images/insights/more-actions.png)

## 评分摘要 {#scoring-summary}

评分汇总显示已评分的用户档案总数，并将其分类为包含高倾向、中倾向和低倾向的时段。 倾向桶根据得分范围确定，低小于24，中为25至74，高大于74。 每个桶都有与图例对应的颜色。

>[!NOTE]
>
>如果是转化倾向得分，则高分以绿色显示，低分以红色显示。 如果您预测客户流失倾向，则高分为红色，低分为绿色。 无论您选择哪种倾向类型，中时段都保持黄色。

![得分摘要](../images/insights/scoring-summary.png)

## 分数分布

“ **[!UICONTROL 分配得分]** ”卡可根据得分直观地汇总人口。 您在“分数分配”卡中 *看到的颜色* ，表示生成的倾向得分类型。

![分数分布](../images/insights/distribution-of-scores.png)

## 影响因素

对于每个分数桶，将生成一张卡片，其中显示该分数桶的前10个影响因素。 这些影响因素为您提供了更多有关客户为何属于不同得分时段的详细信息。

![影响因素](../images/insights/influential-factors.png)

### 创建区段

单击“ **[!UICONTROL 低]** ”、“中”和“高倾向”任意桶中的“创建区段”按钮会将您重定向到区段生成器。

>[!NOTE]
>
>只 **[!UICONTROL 有在为数据集]** 启用实时客户用户档案时，“创建区段”按钮才可用。 有关如何启用实时客户用户档案的更多信息，请 [访问实时客户用户档案概述](../../../rtcdp/overview.md)。

![单击创建区段](../images/insights/influential-factors-create-segment.png)

![创建区段](../images/insights/create-segment.png)

区段生成器用于定义区段。 在从“ **[!UICONTROL 洞察]** ”页面选择创建区段时，客户AI会自动将选定的时段信息添加到区段。 要完成区段的创建，只需填 *写位于**区段构建器用户界面右边栏* 的“名称”和“说明”容器。 为区段指定名称和说明后，单 **[!UICONTROL 击]** 右上角的保存。

>[!NOTE]
>
>由于倾向得分会写入单个用户档案，因此在“区段生成器”中可以像任何其他用户档案属性一样使用这些分数。 当您导航到区段生成器以创建新区段时，您可以在命名空间客户AI下查看所有不同的倾向得分。

![细分填充](../images/insights/segment-saving.png)

要在平台UI中视图新区段，请单击左 **[!UICONTROL 侧导]** 航中的区段。 此时将 **[!UICONTROL 显示]** “浏览”页面，并显示所有可用的区段。

![所有细分](../images/insights/Segments-dashboard.png)

## 后续步骤

本文档概述了客户人工智能服务实例提供的洞察。 您现在可以继续学习在客户AI [中下载分数的教程](./download-scores.md) ，或浏览提 [供的其他Adobe智](../../home.md) 能服务指南。

## Journey Orchestration

以下视频概述了如何使用客户人工智能来查看模型的输出和影响因素。

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)