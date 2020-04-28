---
keywords: Experience Platform;insights; customer ai;popular topics
solution: Experience Platform
title: 利用预测得分创建客户细分
topic: Create a segment
translation-type: tm+mt
source-git-commit: 66ccea896846c1da4310c1077e2dc7066a258063

---


# 利用预测得分创建客户细分

当预测运行完成时，预测倾向得分会由用户档案自动消耗。 利用客户AI得分丰富用户档案，可创建客户细分，以根据其倾向得分查找受众。 本节提供了使用区段生成器创建区段的步骤。 有关创建区段的更强大的教程，请参阅“区 [段生成器”用户指南](../../../segmentation/tutorials/create-a-segment.md)。

>[!IMPORTANT] 为了利用此方法，需要为数据集启用实时客户用户档案。

在平台UI中，单击左 **[!UICONTROL Segments]** 侧导航，然后单击 **[!UICONTROL Create segment]**。

![](../images/user-guide/segments.png)

此时将 *显示“区段生成器* ”。 在左侧的 *字段列中* ，在“属性”( *Attributes* )选项卡下，单击名为的文件夹，然 **[!UICONTROL XDM Individual Profile]** 后单击具有单位命名空间的文件夹。 名为的文 **[!UICONTROL Customer AI]** 件夹包含预测运行的结果，并以得分所属的实例命名。 单击实例文件夹可访问其所需实例的结果。

![](../images/user-guide/results.png)

位于区段生成器中心，将属性拖放到规 **[!UICONTROL Score]** 则生成器画 *布上以定义规则* 。

在右侧的区段属 *性列下* ，为区段提供名称。

![](../images/user-guide/properties.png)

在左侧的“字 *段* ”列上方，单击 **齿轮图标，然后从下拉菜单中** 选择“合并策略 ** ”。 单击 **[!UICONTROL Save]** 以创建区段。

![](../images/user-guide/merge_policy.png)

## 后续步骤

通过本教程，您已使用区段生成器成功找到基于其倾向得分的受众。 您现在可以通过将受众激活到目标来目标它们。 有关详细 [信息，请参阅目标](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) 概述。