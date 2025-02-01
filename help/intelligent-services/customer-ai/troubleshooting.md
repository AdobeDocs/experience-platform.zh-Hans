---
keywords: Experience Platform；入门；客户人工智能；热门主题；客户人工智能输入；客户人工智能输出；客户人工智能故障诊断；客户人工智能错误
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Customer AI错误疑难解答
description: 查找客户人工智能中常见错误的答案。
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '1755'
ht-degree: 1%

---

# Customer AI错误疑难解答

当模型训练、评分和配置失败时，客户人工智能显示错误。 在&#x200B;**[!UICONTROL 服务实例]**&#x200B;部分中，**[!UICONTROL 上次运行状态]**&#x200B;的列显示以下消息之一：**[!UICONTROL 成功]**、**[!UICONTROL 培训问题]**&#x200B;和&#x200B;**[!UICONTROL 失败]**。

![上次运行状态](./images/errors/last-run-status.png)

如果显示&#x200B;**[!UICONTROL 失败]**&#x200B;或&#x200B;**[!UICONTROL 培训问题]**，您可以选择运行状态以打开侧面板。 侧面板包含您的&#x200B;**[!UICONTROL 上次运行状态]**&#x200B;和&#x200B;**[!UICONTROL 上次运行详细信息]**。 **[!UICONTROL 上次运行详细信息]**&#x200B;包含有关运行失败原因的信息。 如果客户人工智能无法提供有关您的错误的详细信息，请与支持人员联系并提供错误代码。

![](./images/errors/last-run-details.png){width=300}

## 无法无痕访问Chrome中的客户人工智能

由于Google Chrome无痕模式安全设置发生更新，导致Google Chrome无痕模式中存在加载错误。 Chrome正在积极处理此问题，以使experience.adobe.com成为受信任的域。

![错误图像](./images/errors/error.PNG){width=500}

### 建议的修复

要解决此问题，您需要将experience.adobe.com添加为始终可以使用Cookie的站点。 首先导航到&#x200B;**chrome://settings/cookies**。 接下来，向下滚动到&#x200B;**自定义行为**&#x200B;部分，然后选择“始终可以使用Cookie的站点”旁边的&#x200B;**添加**&#x200B;按钮。 在显示的弹出窗口中，复制并粘贴`[*.]experience.adobe.com`，然后选中&#x200B;**在此网站中包含第三方Cookie**&#x200B;复选框。 完成后，选择&#x200B;**添加**，然后无痕重新加载客户人工智能。

![建议的修复](./images/errors/cookies2.gif)

## 模型质量差

如果收到错误“[!UICONTROL 模型质量差”。 我们建议使用修改的配置]创建新应用程序。 请按照下面建议的步骤来帮助进行故障排除。

![](./images/errors/model-quality.png){width=300}

### 建议的修复

“模型质量差”表示模型精度不在可接受的范围内。 客户人工智能无法在训练后构建可靠的模型且AUC（ROC曲线下的区域）小于0.65。 要修复错误，建议您更改其中一个配置参数并重新运行训练。

首先检查数据的准确性。 您的数据包含预测结果所需的必要字段很重要。

- 检查您的数据集是否具有最新日期。 客户人工智能始终假定数据在触发模型时处于最新状态。
- 在定义的预测和资格窗口中检查缺少的数据。 您的数据必须完整，不存在缺口。 另外，请确保您的数据集符合[Customer AI历史数据要求](./data-requirements.md#data-requirements)。
- 在架构字段属性中检查商务、应用程序、Web和搜索中缺少的数据。

如果您的数据似乎不是问题，请尝试更改资格群体条件，将模型限制为特定配置文件（例如，过去56天内存在`_experience.analytics.customDimensions.eVars.eVar142`）。 这会限制训练窗口中使用的数据的群体和大小。

如果限制资格群体无效或不可能，请更改您的预测窗口。

- 尝试将预测时段更改为7天，然后查看错误是否继续出现。 如果错误不再发生，则表示您定义预测窗口的数据可能不足。

### 错误

| 错误代码 | 标题 | 消息模板 | 消息示例 |
| ---------- | ----- | ---------------- | --------------- |
| 400 | 目标不足 | 满足预测目标定义的用户（总共{{actual_num_samples}}个）太少，从{{outcome_window_start}}到{{outcome_window_end}}。 我们要求至少{{min_num_samples}}个具有合格事件的用户构建模型。 <br><br>建议的解决方案： <br><br>1。 检查数据可用性<br>2。 缩短预测目标时间范围<br>3。 修改预测目标定义以包含更多用户（错误代码：VALIDATION-400 NOT_ENOUGH_OBJECTIVE） | 满足预测目标定义从2020-04-01到2021-04-01的用户太少（总共200个）。 我们要求至少500名具有合格活动的用户构建模型。 <br><br>建议的解决方案： <br>1。 检查数据可用性<br>2。 缩短预测目标时间范围<br>3。 修改预测目标定义以包含更多用户。 （错误代码：VALIDATION-400 NOT_ENOUGH_OBJECTIVE） |
| 401 | 人口不足 | 从{{eligibility_window_start}}到{{eligibility_window_end}}的合格用户太少（总共{{actual_num_samples}}个）。 我们至少需要{{min_num_samples}}个符合条件的用户才能构建模型。 <br><br>建议的解决方案： <br>1。 检查数据可用性<br>2。 如果提供了合格群体定义，请缩短合格筛选时间范围3。 如果未提供符合条件的群体定义，请尝试添加一个（错误代码：VALIDATION-401 NOT_ENOUGH_POPULATION） | 从2020-04-01到2021-04-01，符合条件的用户（共200个）太少。 我们至少需要500个符合条件的用户才能构建模型。<br><br>建议的解决方案：<br>1。 检查数据可用性<br>2。 如果提供了符合条件的群体定义，请缩短符合条件筛选的时间范围。<br>3. 如果未提供符合条件的群体定义，请尝试添加一个。 （错误代码：VALIDATION-401 NOT_ENOUGH_POPULATION） |
| 402 | 模型错误 | 我们无法使用当前输入数据集和配置生成质量模型。 <br><br>建议包括： <br>1。 修改您的配置以添加符合条件的群体定义。 <br>2. 使用其他数据源提高模型质量<br>3。 添加自定义事件以在模型中包含更多数据（错误代码：VALIDATION-402 BAD_MODEL） | 我们无法使用当前输入数据集和配置生成质量模型。 <br><br>建议包括： <br>1。 请考虑修改您的配置以添加符合条件的群体定义。 <br>2. 请考虑使用其他数据源来提高模型质量。 （错误代码：VALIDATION-402 BAD_MODEL） |
| 403 | 不符合条件的分数 | 得分分布与预期偏差太大。 <br><br>建议包括： <br>1。 请确保模型已使用最近的数据进行训练，否则请考虑重新训练您的模型。 <br>2. 请确保评分任务中没有数据问题（例如缺少数据/数据延迟）。 （错误代码：VALIDATION-403 INELIGIBLE_SCORES） | 得分分布与预期偏差太大。 <br><br>建议包括： <br>1。 请确保模型已使用最近的数据进行训练，否则请考虑重新训练您的模型。 <br>2. 请确保评分任务中没有数据问题（例如缺少数据/数据延迟）。 （错误代码：VALIDATION-403 INELIGIBLE_SCORES） |
| 405 | 无评分数据 | 没有可用于从{{eligibility_window_start}}到{{eligibility_window_end}}评分的用户行为或配置文件数据。请检查数据以确保定期更新。 （错误代码：VALIDATION-405 NO_SCORING_DATA） | 从2020-04-01到2021-04-01，没有可用于评分的用户行为或个人资料数据。 请检查数据以确保定期更新。 （错误代码：VALIDATION-405 NO_SCORING_DATA） |
| 407 | 历史事件数据不足 | 没有足够的数据来构建模型。 从2020-04-01到2021-04-01，数据只有90天。 <br><br>我们需要120天的近期数据。 有关详细信息，请查看数据要求文档。 <br><br>建议的解决方案： <br>1。 检查数据可用性<br>2。 缩短预测目标时间范围<br>3。 如果提供了符合条件的群体定义，请缩短资格筛选时间范围<br>4。 如果未提供符合条件的群体定义，请尝试添加一个（错误代码：VALIDATION-407 NOT_ENOUGH_HISTORICAL_EVENT_DATA） | 没有足够的数据来构建模型。 从2020-04-01到2021-04-01，数据只有90天。<br><br>我们需要120天的近期数据。 有关详细信息，请查看数据要求文档。<br><br>建议的解决方案：<br>1。 检查数据可用性。<br>2. 缩短预测目标时间范围。<br>3. 如果提供了符合条件的群体定义，请缩短符合条件筛选的时间范围。<br>4。 如果未提供符合条件的群体定义，请尝试添加一个。 （错误代码：VALIDATION-407 NOT_ENOUGH_HISTORICAL_EVENT_DATA） |
| 408 | 没有符合条件的最近数据 | 在{{etl_window_end}}之前的{{data_days}}天内没有符合条件的用户的用户行为数据。 请检查数据集以确保定期更新它。 （错误代码：VALIDATION-408 NO_RECENT_DATA_FOR_ELIGIBLE_POPULATION） | 2021-04-01之前60天内没有符合条件的用户的用户行为数据。 请检查数据集以确保定期更新它。 （错误代码：VALIDATION-408 NO_RECENT_DATA_FOR_ELIGIBLE_POPULATION） |
| 409 | 无目标 | 没有用户满足从{{outcome_window_start}}到{{outcome_window_end}}的预测目标定义。 我们要求至少{{min_num_samples}}个具有合格事件的用户构建模型。 <br><br>建议的解决方案： <br>1。 检查数据可用性<br>2。 修改预测目标定义（错误代码：VALIDATION-409 NO_OBJECTIVE） | 没有用户符合预测目标定义2020-04-01到2021-04-01。 我们要求至少500名具有合格活动的用户构建模型。 <br><br>建议的解决方案：<br>1。 检查数据可用性。<br>2. 修改预测目标定义。 （错误代码：VALIDATION-409 NO_OBJECTIVE） |
| 410 | 无群体 | 没有从{{eligibility_window_start}}到{{eligibility_window_end}}的合格用户。 我们至少需要{{min_num_samples}}个符合条件的用户才能构建模型。 <br><br>建议的解决方案： <br>1。 检查数据可用性<br>2。 如果提供了符合条件的群体定义，请修改条件或增加资格筛选时间范围（错误代码：VALIDATION-410 NO_POPULATION） | 2020-04-01到2021-04-01期间没有符合条件的用户。 我们至少需要500个符合条件的用户才能构建模型。 <br><br>建议的解决方案：<br>1。 检查数据可用性。 <br> 2. 如果提供了符合条件的群体定义，请修改条件或增加资格筛选时间范围。 （错误代码：VALIDATION-410 NO_POPULATION） |
| 411 | ETL后无输入数据 | 在{{etl_start_date}}和{{etl_end_date}}之间没有可供模型使用的用户行为或配置文件数据。 请确保数据集具有足够的数据。 （错误代码：VALIDATION-411 NO_INPUT_DATA_AFTER_ETL） | 没有可供模型在2020-04-01和2021-04-01之间使用的用户行为或配置文件数据。 请确保数据集具有足够的数据。 （错误代码：VALIDATION-411 NO_INPUT_DATA_AFTER_ETL） |
| 412 | ETL后无事件 | 在{{etl_start_date}}和{{etl_end_date}}之间没有可供模型使用的用户行为数据。 请确保数据集具有足够的数据。 | 没有可供模型在2020-04-01和2021-04-01之间使用的用户行为数据。 请确保数据集具有足够的数据。 （错误代码：VALIDATION-412 NO_EVENT_DATA_AFTER_ETL） |
| 413 | 目标中的单一值 | CustomerAI要求数据集具有符合和未符合预测目标定义条件的事件。 输入数据集仅包含{{etl_window_start}}到{{etl_window_end}}之间的限定事件。 <br><br>建议的解决方案： <br>1。 修改预测目标定义<br>2。 验证数据的完整性或使用包含非限定事件示例的其他预测目标（错误代码：VALIDATION-413 SINGLE_VALUE_IN_OBJECTIVE） | CustomerAI要求数据集具有符合和未符合预测目标定义条件的事件。 输入数据集仅包含2020-04-01和2021-04-01之间的符合条件的事件。<br><br>建议的解决方案：<br>1。 修改预测目标定义。<br>2. 验证数据的完整性或使用包含非限定事件示例的其他预测目标。 （错误代码：VALIDATION-413 SINGLE_VALUE_IN_OBJECTIVE） |
| 414 | 无影响因素 | 影响因素模型生成了意外输出。 我们建议使用修改后的配置创建新应用程序。 （错误代码：VALIDATION-414 NO_INFLUSHING_FACTORS） | 影响因素模型生成了意外输出。 我们建议使用修改后的配置创建新应用程序。 （错误代码：VALIDATION-414 NO_INFLUSHING_FACTORS） |