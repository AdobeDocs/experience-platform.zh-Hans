---
keywords: Experience Platform；洞察；客户人工智能；热门主题；客户人工智能区段
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: 使用预测得分创建客户区段
description: 预测运行完成后，用户档案会自动使用预测的倾向分数。 通过Customer AI得分丰富用户档案，可创建客户区段以根据其倾向得分查找受众。 本节提供了使用区段生成器创建区段的步骤。
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 使用预测得分创建客户区段

预测运行完成后，用户档案会自动使用预测的倾向分数。 通过Customer AI得分丰富用户档案，可创建客户区段以根据其倾向得分查找受众。 本节提供了使用区段生成器创建区段的步骤。 有关创建区段的更可靠教程，请参阅[区段生成器用户指南](../../../segmentation/ui/segment-builder.md)。

>[!IMPORTANT]
>
>为了利用这种方法，需要为数据集启用实时客户档案。

在Experience Platform UI中，单击左侧导航中的&#x200B;**[!UICONTROL 区段]**，然后单击&#x200B;**[!UICONTROL 创建区段]**。

![](../images/user-guide/segments_new.png)

出现&#x200B;**区段生成器**。 从左侧&#x200B;**[!UICONTROL 字段]**&#x200B;列和&#x200B;**[!UICONTROL 属性]**&#x200B;选项卡下，单击名为&#x200B;**[!UICONTROL XDM个人配置文件]**&#x200B;的文件夹，然后单击包含您组织的命名空间的文件夹。 名为&#x200B;**[!UICONTROL Customer AI]**&#x200B;的文件夹包含预测运行的结果，并以得分所属的实例命名。 单击实例文件夹可访问其所需实例的结果。

![](../images/user-guide/results_new.png)

位于区段生成器的中心，将&#x200B;**[!UICONTROL 分数]**&#x200B;属性拖放到&#x200B;*规则生成器画布*&#x200B;上以定义规则。

在右侧&#x200B;*区段属性*&#x200B;列下，提供区段的名称。

![](../images/user-guide/properties_new.png)

在左侧&#x200B;*字段*&#x200B;列上方，单击&#x200B;**齿轮**&#x200B;图标，然后从下拉列表中选择&#x200B;*合并策略*。 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以创建区段。

![](../images/user-guide/merge_policy_new.png)

## 后续步骤

通过学习本教程，您已成功使用区段生成器根据受众的倾向分数找到受众。 您现在可以通过将受众激活到目标来定位受众。 有关详细信息，请参阅[目标概述](../../../destinations/home.md)。
