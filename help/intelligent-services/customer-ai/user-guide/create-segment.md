---
keywords: Experience Platform；洞察；客户ai；热门主题；客户ai细分
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 创建具有预测分数的客户细分
topic: Create a segment
description: 当预测运行完成时，用户档案会自动消耗预测倾向得分。 利用客户AI得分丰富用户档案，可以创建客户细分，根据受众的倾向得分查找客户。 本节提供使用区段生成器创建区段的步骤。
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# 根据预测得分创建客户细分

当预测运行完成时，用户档案会自动消耗预测倾向得分。 利用客户AI得分丰富用户档案，可以创建客户细分，根据受众的倾向得分查找客户。 本节提供使用区段生成器创建区段的步骤。 有关创建区段的更强大教程，请参阅[区段生成器用户指南](../../../segmentation/ui/segment-builder.md)。

>[!IMPORTANT]
>
>为了利用此方法，需要为数据集启用实时客户用户档案。

在平台UI中，单击左侧导航中的&#x200B;**[!UICONTROL 区段]**，然后单击&#x200B;**[!UICONTROL 创建区段]**。

![](../images/user-guide/segments.png)

出现&#x200B;**区段生成器**。 从左侧&#x200B;**[!UICONTROL 字段]**&#x200B;列和&#x200B;**[!UICONTROL 属性]**&#x200B;选项卡下，单击名为&#x200B;**[!UICONTROL XDM单个用户档案]**&#x200B;的文件夹，然后单击具有您组织命名空间的文件夹。 名为&#x200B;**[!UICONTROL Customer AI]**&#x200B;的文件夹包含预测运行结果，并以得分所属的实例命名。 单击实例文件夹可访问其所需实例的结果。

![](../images/user-guide/results.png)

位于区段生成器的中心，将&#x200B;**[!UICONTROL Score]**&#x200B;属性拖放到&#x200B;*规则生成器画布*&#x200B;上以定义规则。

在右侧的&#x200B;*段属性*&#x200B;列下，提供段的名称。

![](../images/user-guide/properties.png)

在左侧&#x200B;*字段*&#x200B;列上方，单击&#x200B;**gear**&#x200B;图标，并从下拉菜单中选择&#x200B;*合并策略*。 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以创建区段。

![](../images/user-guide/merge_policy.png)

## 后续步骤

通过遵循本教程，您已使用区段生成器成功找到基于受众倾向得分的数据。 您现在可以通过将受众激活到目标来目标。 有关详细信息，请参阅[目标概述](../../../destinations/home.md)。