---
title: Edge Delivery视图
description: 本指南详细介绍了有关Adobe Experience Platform Assurance中Edge Delivery视图的信息。
exl-id: 570c1bcb-ec6d-465e-84ff-ed910d4f7e8a
source-git-commit: a11f469cb54421e0ca30c7c5878128e216470f7f
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 2%

---

# Assurance中的Edge Delivery视图

**[!UICONTROL Edge Delivery保证]**&#x200B;中的&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;视图提供检查并验证向您的Web和移动应用发送[!UICONTROL AJO入站]边缘消息的功能。 此视图对于排查[!UICONTROL AJO入站] Web和移动营销活动和历程的交付问题特别有用。

## 快速入门

在继续之前，请确保您有权访问以下服务：

- [Adobe Experience Platform 数据收藏集 UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

若要了解如何在应用程序中安装&#x200B;**[!UICONTROL 保证]**，请阅读[实施保证指南](../tutorials/implement-assurance.md)。

## 在Edge Delivery中使用Assurance

打开&#x200B;**[!UICONTROL Assurance]**&#x200B;会话后，您可以将&#x200B;**[!UICONTROL Edge Delivery]**&#x200B;视图添加到&#x200B;**[!UICONTROL Assurance]**。 在左面板底部，选择&#x200B;**[!UICONTROL 配置]**&#x200B;以添加&#x200B;**[!UICONTROL Edge Delivery]**&#x200B;视图并&#x200B;**保存**。

![通过选择左下角的“配置”添加插件](./images/edge-delivery/add-plugin.png)

添加后，在&#x200B;**[!UICONTROL Edge Delivery]**&#x200B;部分中选择&#x200B;**[!UICONTROL Adobe Journey Optimizer]**&#x200B;视图以验证入站边缘投放。

可在Adobe Journey Optimizer视图组中访问![Edge Delivery](./images/edge-delivery/ajo-plugins.png)

## 请求列表

在视图的主窗格中，将显示边缘投放请求的列表。 此列表显示向Experience Edge发出并由&#x200B;**[!UICONTROL 入站投放服务]**&#x200B;处理的所有[!UICONTROL 入站AJO]请求，包括检索个性化决策以及跟踪个性化建议交互（如显示、单击、触发或取消）的请求。

请求按时间戳排序，最近的请求位于顶部。 除了时间戳之外，该列表还包含请求ID列以及请求类型，请求类型可以是以下任一类型：

- **[!UICONTROL 体验投放]**：检索个性化决策的请求
- **[!UICONTROL 体验交互]**：用于跟踪个性化建议交互的请求
- **[!UICONTROL 体验交付和交互]**：检索个性化决策的请求，其中也包含个性化建议交互
- **[!UICONTROL 预览投放]**：检索预览个性化决策的请求

也可以在列表顶部的搜索栏中输入搜索词，以筛选请求。 当按特定值（如ID）进行筛选时，这将很有用。

![入站请求列表显示在主视图中](./images/edge-delivery/request-list.png)

## 详细的请求视图

在主视图中选择请求后，所选请求的详细信息，将显示在右侧。 此视图包括以下部分：

### 请求概述

此部分提供所选请求的高级概述，包括[!UICONTROL 组织ID]、[!UICONTROL Edge群集]、[!UICONTROL 请求ID]和[!UICONTROL 请求类型]、[!UICONTROL 沙盒ID]、[!UICONTROL 沙盒名称]、[!UICONTROL 数据流ID]，以及出现[!UICONTROL 体验交付]请求时的请求表面列表。

![请求概述部分提供高级请求详细信息](./images/edge-delivery/request-overview.png)

### 配置文件

本节提供有关处理请求时使用的配置文件数据的信息，包括身份映射、区段成员资格和同意设置。\
在排除投放等由于缺少或延迟区段成员资格或选择退出同意设置而无法按预期工作的问题时，[!UICONTROL 配置文件]部分非常有用。

![配置文件部分包括身份映射、区段成员资格和同意设置](./images/edge-delivery/profile.png)

### 符合条件的活动

此部分提供符合选定请求条件的活动列表，包括活动类型、ID、身份命名空间、界面、计划和受众。 有关活动的更多详细信息可在[原始执行跟踪部分](#execution)中找到。

![合格活动部分包含合格活动的详细信息](./images/edge-delivery/qualified-activities.png)

### 不合格活动

此部分提供不合格活动的列表。 除了活动类型、ID、身份命名空间、表面、计划和受众之外，此部分还包含活动不符合条件的原因列表。

![不合格活动部分包含不合格活动的详细信息和排除原因](./images/edge-delivery/unqualified-activities.png)

### 消息详细信息

此部分提供有关为所选请求投放的消息的详细信息。 它包括消息ID、片段、决策策略、[!UICONTROL Offer decisioning]参数以及消息选择上下文。

![包含已投放消息详细信息的部分，例如消息ID和选择上下文、片段、决策策略和决策参数](./images/edge-delivery/message-details.png)

### 交互

此部分提供有关在选定请求中跟踪的交互的详细信息。 它包括交互类型（`propositionEventType`下）以及关联建议元数据，例如活动元数据（`scopeDetails.activity`下）和建议事件令牌（在`scopeDetails.characteristics.eventToken`中）。

![通过建议令牌和相关活动元数据跟踪交互](./images/edge-delivery/interactions.png)

### 原始跟踪

此部分提供所选请求的原始跟踪。 它包括请求的完整跟踪，包括在&#x200B;**[!UICONTROL 入站投放服务]**&#x200B;中收到的实际请求、执行跟踪和响应跟踪。 这对于高级故障排除（例如由于投放服务不可用、数据丢失或不正确而导致投放无法按预期工作）或了解请求处理的完整流程非常有用。

#### 请求

请求跟踪包含完整的请求，因为它由&#x200B;**[!UICONTROL 入站投放服务]** **[!UICONTROL Konductor]**&#x200B;上游接收。 它包括请求标头、正文和其他元数据。 例如，可在`event.body.xdm`字段中检查请求的XDM有效负载。

![在请求跟踪中可以找到包括标头和正文的详细请求信息](./images/edge-delivery/request.png)

#### 执行

执行跟踪包括请求的完整跟踪，因为&#x200B;**[!UICONTROL 入站投放服务]**&#x200B;已处理该请求。 它显示了执行上下文、活动资格、报文选择和其他处理步骤。 处理请求期间发生的任何错误或警告都可以在`context.messages`和`context.exceptions`字段中找到。 可在`context.qualifiedActivitiesDetailed`和`context.unqualifiedActivitiesDetailed`字段中找到详细的活动资格信息。

![执行跟踪包括执行上下文、活动资格、消息选择和其他处理详细信息](./images/edge-delivery/execution.png)

#### 响应

响应跟踪包含由&#x200B;**[!UICONTROL 入站投放服务]**&#x200B;下游到&#x200B;**[!UICONTROL Konductor]**&#x200B;返回的完整响应。 它包括响应标头、正文和其他元数据。 通过使用&#x200B;**[!UICONTROL 复制值]**&#x200B;按钮将ID为`1`的消息复制到剪贴板并将其粘贴到JSON查看器中来检查完整的响应正文。

![响应跟踪包含返回下游的完整响应正文](./images/edge-delivery/response.png)
