---
keywords: Experience Platform；分析；客户人工智能；热门主题；客户人工智能区段
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: 使用预测得分创建客户区段
description: 预测运行完成后，用户档案会自动使用预测的倾向分数。 通过Customer AI得分丰富用户档案，可创建客户区段以根据其倾向得分查找受众。 本节提供了使用区段生成器创建区段的步骤。
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# 使用预测得分创建客户区段

预测运行完成后，用户档案会自动使用预测的倾向分数。 通过Customer AI得分丰富用户档案，可创建客户区段以根据其倾向得分查找受众。 本节提供了使用区段生成器创建区段的步骤。 有关创建区段的更可靠教程，请参阅 [区段生成器用户指南](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>为了利用这种方法，需要为数据集启用实时客户档案。

在Platform UI中，单击 **[!UICONTROL 区段]** 在左侧导航中，然后单击 **[!UICONTROL 创建区段]**.

![](../images/user-guide/segments.png)

此 **区段生成器** 显示。 从左侧 **[!UICONTROL 字段]** 列和下 **[!UICONTROL 属性]** 选项卡，单击名为的文件夹 **[!UICONTROL XDM个人资料]** 然后单击包含您组织的命名空间的文件夹。 名为的文件夹 **[!UICONTROL 客户人工智能]** 包含预测运行的结果，并以得分所属的实例进行命名。 单击实例文件夹可访问其所需实例的结果。

![](../images/user-guide/results.png)

位于区段生成器的中心，拖放 **[!UICONTROL 分数]** 归因到 *规则生成器画布* 以定义规则。

在右手下 *区段属性* 列中，提供区段的名称。

![](../images/user-guide/properties.png)

左手上方 *字段* 列中，单击 **齿轮** 图标并选择 *合并策略* 从下拉菜单中查找。 单击 **[!UICONTROL 保存]** 以创建区段。

![](../images/user-guide/merge_policy.png)

## 后续步骤

通过学习本教程，您已成功使用区段生成器根据受众的倾向分数找到受众。 您现在可以通过将受众激活到目标来定位受众。 请参阅 [目标概述](../../../destinations/home.md) 以了解更多信息。
