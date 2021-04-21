---
keywords: Experience Platform；洞察；客户ai；热门主题；客户ai细分
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 使用预测得分创建客户细分
topic-legacy: Create a segment
description: 当预测运行完成时，预测倾向得分会被用户档案自动消耗。 通过用户档案人工智能得分丰富受众，可创建客户细分，根据客户倾向得分查找客户。 本节提供使用区段生成器创建区段的步骤。
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 根据预测得分创建客户细分

当预测运行完成时，预测倾向得分会被用户档案自动消耗。 通过用户档案人工智能得分丰富受众，可创建客户细分，根据客户倾向得分查找客户。 本节提供使用区段生成器创建区段的步骤。 有关创建区段的更强大教程，请参阅[区段生成器用户指南](../../../segmentation/ui/segment-builder.md)。

>[!IMPORTANT]
>
>要使用此方法，需要为数据集启用实时客户用户档案。

在平台UI中，单击左侧导航中的&#x200B;**[!UICONTROL Segments]**，然后单击&#x200B;**[!UICONTROL Create segment]**。

![](../images/user-guide/segments.png)

出现&#x200B;**区段生成器**。 从左&#x200B;**[!UICONTROL Fields]**&#x200B;列和&#x200B;**[!UICONTROL Attributes]**&#x200B;选项卡下，单击名为&#x200B;**[!UICONTROL XDM Individual Profile]**&#x200B;的文件夹，然后单击具有您的组织命名空间的文件夹。 名为&#x200B;**[!UICONTROL Customer AI]**&#x200B;的文件夹包含预测运行的结果，并以分数所属的实例命名。 单击实例文件夹可访问所需实例的结果。

![](../images/user-guide/results.png)

位于区段生成器的中心，将&#x200B;**[!UICONTROL Score]**&#x200B;属性拖放到&#x200B;*规则生成器画布*&#x200B;上以定义规则。

在右侧的&#x200B;*区段属性*&#x200B;列下，提供区段的名称。

![](../images/user-guide/properties.png)

在左侧&#x200B;*字段*&#x200B;列上方，单击&#x200B;**gear**&#x200B;图标，然后从下拉菜单中选择&#x200B;*合并策略*。 单击&#x200B;**[!UICONTROL Save]**&#x200B;以创建区段。

![](../images/user-guide/merge_policy.png)

## 后续步骤

通过本教程，您已使用“区段生成器”成功找到基于受众倾向得分的客户。 您现在可以通过将受众激活到目标位置来目标这些客户。 有关详细信息，请参阅[目标概述](../../../destinations/home.md)。
