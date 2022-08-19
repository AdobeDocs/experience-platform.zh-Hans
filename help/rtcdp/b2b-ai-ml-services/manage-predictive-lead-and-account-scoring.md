---
title: 在实时CDP B2B中管理预测性潜在客户和客户评分
type: Documentation
description: 本文档提供了有关管理Experience PlatformCDP B2B中的预测潜在客户和帐户评分功能的信息。
source-git-commit: 5ac8e099a6de563371f9a53a8b4816e6cf4d1953
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 2%

---

# 在Real-time Customer Data Platform B2B Edition中管理预测潜在客户和帐户评分

>[!NOTE]
>
>只有具有“管理B2B AI”权限的用户才能创建、更改和删除得分目标。

本教程将指导您完成管理预测潜在客户和帐户评分服务的得分目标的步骤。 得分目标可以是个人资料或帐户资料

## 创建新分数

要创建新分数，请选择 **[!UICONTROL 服务]** 在侧栏中，然后选择 **[!UICONTROL 创建分数]**.

![plas-new-score](../assets/../b2b-ai-ml-services/assets/plas-create-score.png)

的 **[!UICONTROL 基本信息]** 屏幕，提示您选择配置文件类型、输入名称和可选描述。 完成后，选择 **[!UICONTROL 下一个]**.

![plas-enter-basic-information](../assets/../b2b-ai-ml-services/assets/plas-basic-information.png)

的 **[!UICONTROL 定义目标]** 屏幕。 选择下拉箭头，然后从显示的下拉窗口中选择目标类型。

![plas-select-a-goal](../assets/../b2b-ai-ml-services/assets/plas-define-goal.png)

的 **[!UICONTROL 目标详情]** 对话框。 选择下拉箭头，然后从显示的下拉窗口中选择目标字段名称。

![plas-select-a-goal-field-name](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-name.png)

的 **[!UICONTROL 目标条件]** 将显示“选择”。 选择下拉箭头，然后从显示的下拉窗口中选择条件。

![plas-goal-specifics-condition](../assets/../b2b-ai-ml-services/assets/plas-goal-specidics-condition.png)

的 **[!UICONTROL 目标值]** 字段。 接下来，配置 [!UICONTROL 目标详情]. 选择 [!UICONTROL 输入字段值] ，然后输入目标值。

>[!NOTE]
>
>可以添加多个目标值。

![plas-goal-defics-field-value](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-value.png)

要添加其他字段，请选择 **[!UICONTROL 添加字段]**.

![plas-goal-defics-add-event](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-add-event.png)

要配置预测时间范围，请选择下拉箭头，然后选择您选择的时间范围。

![plas-prediction-timmeran](../assets/../b2b-ai-ml-services/assets/plas-prediction-timeframe.png)

所选合并策略确定如何选择人员用户档案的字段值。 使用下拉箭头选择您选择的合并策略，然后选择 **[!UICONTROL 完成]**.

的 **[!UICONTROL 评分设置已完成]** 出现对话框，确认已创建新得分。 选择 **[!UICONTROL 确定]**.

![plas-score-complete](../assets/../b2b-ai-ml-services/assets/plas-score-complete.png)

>[!NOTE]
>
>完成每个评分过程可能最多需要24小时。

您将返回到 **[!UICONTROL 服务]** 选项卡，您可以在此处查看在得分列表中创建的新得分。

![已创建plas-score](../assets/../b2b-ai-ml-services/assets/plas-score-created.png)

选择分数可查看有关上次运行详细信息的详细信息和其他信息。

![plas-score-additional information](../assets/../b2b-ai-ml-services/assets/plas-score-info.png)

有关在上次运行详细信息下可看到的错误代码的详细信息，请参阅 [潜在AI管道错误代码](#leads-ai-pipeline-error-codes) 在本文档中。

## 编辑分数

要编辑分数，请从 **[!UICONTROL 服务]** 选项卡，选择 **[!UICONTROL 编辑]** 从屏幕右侧的其他详细信息面板。

![plas-edit-score](../assets/../b2b-ai-ml-services/assets/plas-edit-score.png)

的 **[!UICONTROL 编辑实例]** 对话框中，您可以在其中编辑对得分的描述。 进行更改并选择 **[!UICONTROL 保存]**.

![plas-edit-save](../assets/../b2b-ai-ml-services/assets/plas-edit-save.png)

>[!NOTE]
>
>无法更改得分配置，因为这将触发模型再培训和再评分。 它等同于删除分数并创建新分数。 要编辑得分的配置，您需要克隆此得分或创建新得分。

您将返回到 **[!UICONTROL 服务]** 选项卡。 选择分数，以在屏幕右侧的其他详细信息面板中查看更新的描述详细信息。

## 克隆分数

要克隆得分，请从 **[!UICONTROL 服务]** 选项卡，选择 **[!UICONTROL 克隆]** 从屏幕右侧的其他详细信息面板。

![plas-clone-score](../assets/../b2b-ai-ml-services/assets/plas-clone-score.png)

的 **[!UICONTROL 基本信息]** 屏幕。 配置文件类型、名称和描述将从原始分数中克隆。 修改这些详细信息并选择 **[!UICONTROL 下一个]**.

![plas-clone-basic-info](../assets/../b2b-ai-ml-services/assets/plas-clone-basic-info.png)

的 **[!UICONTROL 定义目标]** 屏幕。 像创建新得分时一样完成目标部分，然后选择 **[!UICONTROL 完成]**.

您将返回到 **[!UICONTROL 服务]** 选项卡，您可以在列表中查看新克隆的分数。

>[!NOTE]
>
>的 **[!UICONTROL 定义目标]** 部分未从原始分数中克隆。

## 删除分数

要删除分数，请从 **[!UICONTROL 服务]** 选项卡，选择 **[!UICONTROL 删除]** 从屏幕右侧的其他详细信息面板。

![plas-delete-score](../assets/../b2b-ai-ml-services/assets/plas-delete-score.png)

的 **[!UICONTROL 删除文档]** 确认对话框。 选择 **[!UICONTROL 删除]**.

![plas-delete-score-confirmation](../assets/../b2b-ai-ml-services/assets/plas-delete-score-confirmation.png)

>[!NOTE]
>
>删除得分定义也会删除人员配置文件或帐户配置文件上的所有预测得分，但不会删除为得分定义创建的字段组。 字段组在数据模型中将保持为“孤立”。

您将返回到 **[!UICONTROL 服务]** 选项卡中，您将无法再在列表中看到分数。

## 引导AI管道错误代码

| 错误代码 | 错误消息 |
| --- | --- |
| 401 | 错误401。 Lead AI管道已停止：帐户评分的有效帐户不足。 帐户计数：{}。 |
| 402 | 错误402。 Lead AI管道已停止：联系人的有效联系人不足，无法进行联系评分。 联系人计数：{}。 |
| 403 | 错误403。 Lead AI管道已停止：模型培训的活动量不足。 事件计数：{}。 |
| 404 | 错误404。 Lead AI管道已停止：模型培训的转化不足。 转化计数：{}。 |
| 405 | 错误405。 Lead AI管道已停止：活动过于稀疏，无法进行有效的模型培训。 只有{}%的帐户具有活动。 |
| 406 | 错误406。 Lead AI管道已停止：活动过于稀疏，无法进行有效的模型培训。 只有{}%的联系人具有活动。 |
| 407 | 错误407。 Lead AI管道已停止：评分数据活动类型与培训数据不匹配。 |
| 408 | 错误408。 Lead AI管道已停止：活动功能的缺失率过高。 缺失率：{}。 |
| 409 | 错误409。 Lead AI管道已停止：测试auc过低。 测试音频：{}。 |
| 410 | 错误410。 Lead AI管道已停止：参数调整后，测试auc过低。 测试音频：{}。 |
| 411 | 错误411。 Lead AI管道已停止：培训数据没有足够的转化来生成可靠的模型。 转化: {}. |
| 412 | 错误412。 Lead AI管道已停止：测试数据没有任何计算AUC-ROC的转换。 |

| 警告/信息代码 | 消息 |
| --- | --- |
| 100 | 信息100。 引导人工智能质量检查：帐户计数为：{}。 |
| 101 | 信息101。 引导人工智能质量检查：联系人数为：{}。 |
| 102 | 信息102。 引导人工智能质量检查：机会的数量是：{}。 |
| 103 | 信息103。 引导人工智能质量检查：测试auc低。 开始参数调整。 测试受众：{}。 |
| 200 | 警告200。 引导人工智能质量检查：缺少第一图形特征的速率是：{}。 |
| 201 | 警告201。 引导人工智能质量检查：活动功能的缺失率是：{}。 |

## 后续步骤

通过阅读本教程，您现在可以成功创建和管理分数。 有关更多详细信息，请参阅以下文档：

* [预测潜在客户和帐户评分](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
* [监控预测潜在客户和帐户评分作业](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)
