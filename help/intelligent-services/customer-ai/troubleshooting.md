---
keywords: Experience Platform；快速入门；客户人工智能；热门主题；客户人工智能输入；客户人工智能输出；客户人工智能故障排除；客户人工智能错误
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Customer AI错误疑难解答
description: 查找客户人工智能中常见错误的答案。
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: 3bc750b5e1cf47cbca6b037d099936c80c926cf8
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Customer AI错误疑难解答

当模型训练、评分和配置失败时，客户人工智能显示错误。 在 **[!UICONTROL 服务实例]** 节，列 **[!UICONTROL 上次运行状态]** 显示以下消息之一： **[!UICONTROL 成功]**， **[!UICONTROL 培训问题]**、和 **[!UICONTROL 失败]**.

![上次运行状态](./images/errors/last-run-status.png)

如果 **[!UICONTROL 失败]** 或 **[!UICONTROL 培训问题]** 显示，您可以选择运行状态以打开侧面板。 侧面板包含 **[!UICONTROL 上次运行状态]** 和 **[!UICONTROL 上次运行详细信息]**. **[!UICONTROL 上次运行详细信息]** 包含有关运行失败原因的信息。 如果客户人工智能无法提供有关您的错误的详细信息，请与支持人员联系并提供错误代码。

<img src="./images/errors/last-run-details.png" width="300" /><br />

## 无法在Chrome中无痕访问客户人工智能

由于Google Chrome无痕模式安全设置更新，在Google Chrome无痕模式中加载出错。 正在积极使用Chrome解决此问题，以使experience.adobe.com成为受信任的域。

<img src="./images/errors/error.PNG" width="500" /><br />

### 建议的修复

要解决此问题，您需要添加experience.adobe.com作为始终可以使用Cookie的站点。 首先导航到 **chrome://settings/cookies**. 接下来，向下滚动到 **自定义行为** 部分，然后选择 **添加** “始终可以使用Cookie的站点”旁边的按钮。 在显示的弹出窗口中，复制并粘贴 `[*.]experience.adobe.com` 然后选择 **包括第三方Cookie** “在此网站上”复选框。 完成后，选择 **添加** 和无痕地重新加载客户人工智能。

![建议的修复](./images/errors/cookies2.gif)

## 模型质量差

如果您收到错误“[!UICONTROL 模型质量差。 我们建议使用修改后的配置创建新应用程序]“。 请按照以下建议的步骤帮助进行故障排除。

<img src="./images/errors/model-quality.png" width="300" /><br />

### 建议的修复

“模型质量差”表示模型精度不在可接受的范围内。 训练后，客户人工智能无法构建可靠的模型，且AUC（ROC曲线下的区域）小于0.65。 要修复错误，建议您更改其中一个配置参数并重新运行训练。

首先检查数据的准确性。 您的数据包含预测结果所需的必要字段非常重要。

- 检查您的数据集是否具有最新日期。 客户人工智能始终假定数据在触发模型时处于最新状态。
- 检查定义的预测和资格窗口内的缺失数据。 您的数据需要完整，无间隙。 另外，请确保您的数据集符合 [客户人工智能历史数据要求](./data-requirements.md#data-requirements).
- 在架构字段属性中，检查商务、应用程序、Web和搜索中缺少的数据。

如果您的数据似乎不是问题，请尝试更改资格群体条件，将模型限制为特定用户档案(例如， `_experience.analytics.customDimensions.eVars.eVar142` 在过去56天内存在)。 这会限制训练窗口中使用的数据的群体和大小。

如果限制资格群体无效或不可能，请更改您的预测窗口。

- 尝试将预测时段更改为7天，然后查看错误是否继续发生。 如果错误不再发生，则表明您定义的数据预测窗口可能不足。
