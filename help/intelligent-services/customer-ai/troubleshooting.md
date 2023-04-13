---
keywords: Experience Platform；快速入门；客户人工智能；热门主题；客户人工智能输入；客户人工智能输出；客户人工智能故障诊断；客户人工智能错误
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Customer AI错误疑难解答
description: 查找Customer AI中常见错误的答案。
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: 3bc750b5e1cf47cbca6b037d099936c80c926cf8
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Customer AI错误疑难解答

当模型培训、评分和配置失败时， Customer AI会显示错误。 在 **[!UICONTROL 服务实例]** 部分，列 **[!UICONTROL 上次运行状态]** 显示以下消息之一： **[!UICONTROL 成功]**, **[!UICONTROL 培训问题]**&#x200B;和 **[!UICONTROL 失败]**.

![上次运行状态](./images/errors/last-run-status.png)

如果 **[!UICONTROL 失败]** 或 **[!UICONTROL 培训问题]** 显示时，您可以选择运行状态以打开侧面板。 侧面板包含 **[!UICONTROL 上次运行状态]** 和 **[!UICONTROL 上次运行详细信息]**. **[!UICONTROL 上次运行详细信息]** 包含有关运行失败原因的信息。 如果Customer AI无法提供有关您的错误的详细信息，请联系支持人员并提供的错误代码。

<img src="./images/errors/last-run-details.png" width="300" /><br />

## 无法在Chrome中隐身访问Customer AI

由于Google Chrome的隐身模式安全设置中的更新，在Google Chrome的隐身模式中出现加载错误。 该问题正在与Chrome一起积极处理，以使experience.adobe.com成为可信域。

<img src="./images/errors/error.PNG" width="500" /><br />

### 建议的修复

要解决此问题，您需要将experience.adobe.com添加为始终可以使用Cookie的网站。 首先，导航到 **chrome://settings/cookies**. 接下来，向下滚动到 **自定义行为** 部分，然后选择 **添加** 按钮。 在显示的弹出窗口中，复制并粘贴 `[*.]experience.adobe.com` 然后选择 **包括第三方Cookie** 复选框。 完成后，选择 **添加** 然后隐匿地重新加载Customer AI。

![推荐修复](./images/errors/cookies2.gif)

## 模型质量差

如果收到错误“[!UICONTROL 模型质量较差。 我们建议使用修改后的配置创建新应用程序]&quot; 请按照以下建议步骤帮助进行故障诊断。

<img src="./images/errors/model-quality.png" width="300" /><br />

### 建议的修复

“模型质量差”是指模型精度不在可接受范围内。 客户人工智能在培训后无法构建可靠的模型，且AUC（ROC曲线下的区域）小于0.65。 要修复该错误，建议您更改其中一个配置参数并重新运行培训。

首先检查数据的准确性。 您的数据必须包含预测结果所需的必要字段。

- 检查数据集是否具有最新日期。 Customer AI始终假定数据在触发模型时处于最新状态。
- 检查定义的预测和资格窗口中是否缺少数据。 您的数据必须完整无缺。 另外，请确保您的数据集符合 [客户人工智能历史数据要求](./data-requirements.md#data-requirements).
- 在架构字段属性中，检查商务、应用程序、Web和搜索中是否缺少数据。

如果您的数据似乎不存在问题，请尝试更改资格填充条件以将模型限制为特定用户档案(例如， `_experience.analytics.customDimensions.eVars.eVar142` 存在)。 这可限制培训窗口中使用的数据的群体和大小。

如果限制资格人口不起作用或不可能，请更改您的预测窗口。

- 尝试将预测窗口更改为7天，并查看错误是否继续发生。 如果错误不再发生，则表示您可能没有足够的数据用于定义的预测窗口。
