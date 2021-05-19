---
keywords: Experience Platform；入门；客户ai；热门主题；客户ai输入；客户ai输出；客户ai疑难解答；客户ai错误
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 客户人工智能错误疑难解答
topic-legacy: Getting started
description: 查找客户人工智能中常见错误的答案。
type: Documentation
source-git-commit: ceb203899cda83aa79b994d45798d6147c3ff3b8
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# 客户人工智能错误疑难解答

当模型培训、评分和配置失败时，客户人工智能会显示错误。 在&#x200B;**[!UICONTROL 服务实例]**&#x200B;部分， **[!UICONTROL LAST RUN STATUS]**&#x200B;的列显示以下消息之一：**[!UICONTROL 成功]**、**[!UICONTROL 培训问题]**&#x200B;和&#x200B;**[!UICONTROL 失败]**。

![上次运行状态](./images/errors/last-run-status.png)

在显示&#x200B;**[!UICONTROL Failed]**&#x200B;或&#x200B;**[!UICONTROL Training issue]**&#x200B;的事件中，您可以选择运行状态以打开侧面板。 侧面板包含您的&#x200B;**[!UICONTROL 上次运行状态]**&#x200B;和&#x200B;**[!UICONTROL 上次运行详细信息]**。 **[!UICONTROL 上次运行]** 详细信息包含有关运行失败原因的信息。在客户AI无法提供有关您错误的详细信息的事件中，请与支持部门联系，并提供错误代码。

<img src="./images/errors/last-run-details.png" width="300" /><br />

## 模型质量差

如果收到错误“[!UICONTROL 模型质量较差。 我们建议使用修改后的配置]创建新应用程序。 请按照以下建议步骤帮助进行疑难解答。

<img src="./images/errors/model-quality.png" width="300" /><br />

### 建议的修复

“模型质量差”是指模型精度不在可接受范围内。 培训后，客户AI无法构建可靠的模型和AUC（ROC曲线下的区域）&lt; 0.65。 要修复该错误，建议您更改其中一个配置参数并重新运行培训。

开始。 您的数据必须包含预测结果所需的必要字段。

- 检查您的数据集是否具有最新日期。 客户人工智能始终假定数据在触发模型时是最新的。
- 检查您定义的预测和资格窗口中是否缺少数据。 您的数据必须完整且无间隙。 另外，请确保您的数据集符合[客户人工智能历史数据要求](./input-output.md#data-requirements)。
- 在您的模式字段属性中检查商务、应用程序、Web和搜索中是否缺少数据。

如果您的数据似乎不是问题所在，请尝试更改资格填充条件以将模型限制为某些用户档案（例如，`_experience.analytics.customDimensions.eVars.eVar142`在过去56天中存在）。 这会限制在培训窗口中使用的数据的数量和大小。

如果限制资格数量无效或不可能，请更改您的预测窗口。

- 尝试将预测窗口更改为7天，并查看错误是否继续发生。 如果不再发生错误，则表明您可能没有足够的数据用于定义的预测窗口。

