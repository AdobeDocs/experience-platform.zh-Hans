---
keywords: Experience Platform；分析；客户人工智能；热门主题；客户人工智能区段
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: 创建具有预测得分的客户区段
topic-legacy: Create a segment
description: 预测运行完成后，用户档案会自动使用预测的倾向得分。 利用Customer AI扩充用户档案，可创建客户区段，以根据其倾向得分查找受众。 本节提供了使用区段生成器创建区段的步骤。
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# 使用预测的得分创建客户区段

预测运行完成后，用户档案会自动使用预测的倾向得分。 利用Customer AI扩充用户档案，可创建客户区段，以根据其倾向得分查找受众。 本节提供了使用区段生成器创建区段的步骤。 有关创建区段的更可靠教程，请参阅[区段生成器用户指南](../../../segmentation/ui/segment-builder.md)。

>[!IMPORTANT]
>
>要使用此方法，需要为数据集启用实时客户资料。

在Platform UI中，单击左侧导航中的&#x200B;**[!UICONTROL 区段]**，然后单击&#x200B;**[!UICONTROL 创建区段]**。

![](../images/user-guide/segments.png)

此时会显示&#x200B;**区段生成器**。 从左&#x200B;**[!UICONTROL Fields]**&#x200B;列的&#x200B;**[!UICONTROL Attributes]**&#x200B;选项卡下，单击名为&#x200B;**[!UICONTROL XDM Indivial Profile]**&#x200B;的文件夹，然后单击具有您组织命名空间的文件夹。 名为&#x200B;**[!UICONTROL Customer AI]**&#x200B;的文件夹包含预测运行的结果，并以得分所属的实例命名。 单击实例文件夹以访问所需实例的结果。

![](../images/user-guide/results.png)

位于区段生成器的中心，将&#x200B;**[!UICONTROL Score]**&#x200B;属性拖放到规则生成器画布&#x200B;*上以定义规则。*

在右侧的&#x200B;*区段属性*&#x200B;列下，提供区段的名称。

![](../images/user-guide/properties.png)

在左侧的&#x200B;*字段*&#x200B;列上方，单击&#x200B;**齿轮**&#x200B;图标，然后从下拉菜单中选择&#x200B;*合并策略*。 单击&#x200B;**[!UICONTROL Save]**&#x200B;以创建区段。

![](../images/user-guide/merge_policy.png)

## 后续步骤

通过阅读本教程，您已使用区段生成器成功找到了基于受众倾向得分的受众。 您现在可以通过将受众激活到目标来定位受众。 有关更多信息，请参阅[目标概述](../../../destinations/home.md) 。
