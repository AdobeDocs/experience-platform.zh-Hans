---
keywords: Experience Platform;insights;customer ai;popular topics
solution: Experience Platform
title: 根据预测得分创建客户细分
topic: Create a segment
description: 当预测运行完成时，用户档案会自动消耗预测倾向得分。 利用客户AI得分丰富用户档案，可以创建客户细分，根据受众的倾向得分查找客户。 本节提供使用区段生成器创建区段的步骤。
translation-type: tm+mt
source-git-commit: c5e2ea5daf813bf580a11f0182361197e55c6fe8
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# 根据预测得分创建客户细分

当预测运行完成时，用户档案会自动消耗预测倾向得分。 利用客户AI得分丰富用户档案，可以创建客户细分，根据受众的倾向得分查找客户。 本节提供使用区段生成器创建区段的步骤。 有关创建区段的更强大教程，请参阅“区 [段生成器”用户指南](../../../segmentation/ui/segment-builder.md)。

>[!IMPORTANT]
>
>为了利用此方法，需要为数据集启用实时客户用户档案。

在平台UI中，单击左 **[!UICONTROL 侧导航]** 中的区段，然后单击 **[!UICONTROL 创建区段]**。

![](../images/user-guide/segments.png)

此时 **会显示“区段** ”生成器。 在左侧 **[!UICONTROL 的]** “字段”列和“属性” **[!UICONTROL 选项卡下，单击名]** 为“XDM个人用户档案”的文件夹 **** ，然后单击具有组织命名空间的文件夹。 名为Customer **[!UICONTROL AI的文件夹]** 包含预测运行的结果，并以得分所属的实例命名。 单击实例文件夹可访问其所需实例的结果。

![](../images/user-guide/results.png)

位于区段生成器的中心，将“分数”属 **[!UICONTROL 性拖放]** 到规则 *生成器画布上以* 定义规则。

在右侧的区 *段属性* 列下，提供区段的名称。

![](../images/user-guide/properties.png)

在左侧的“字 *段* ”列上方，单 **击齿轮图** 标，并从下拉 *菜单中选择* “合并策略”。 Click **[!UICONTROL Save]** to create the segment.

![](../images/user-guide/merge_policy.png)

## 后续步骤

通过遵循本教程，您已使用区段生成器成功找到基于受众倾向得分的数据。 您现在可以通过将受众激活到目标来目标。 有关更多 [信息](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) ，请参阅目标概述。