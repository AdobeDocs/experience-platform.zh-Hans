---
keywords: Experience Platform；分析；客户人工智能；热门主题；客户人工智能区段
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 创建具有预测得分的客户区段
description: 预测运行完成后，用户档案会自动使用预测的倾向得分。 利用Customer AI扩充用户档案，可创建客户区段，以根据其倾向得分查找受众。 本节提供了使用区段生成器创建区段的步骤。
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# 使用预测的得分创建客户区段

预测运行完成后，用户档案会自动使用预测的倾向得分。 利用Customer AI扩充用户档案，可创建客户区段，以根据其倾向得分查找受众。 本节提供了使用区段生成器创建区段的步骤。 有关创建区段的更加可靠的教程，请参阅 [区段生成器用户指南](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>要使用此方法，需要为数据集启用实时客户资料。

在平台UI中，单击 **[!UICONTROL 区段]** ，然后单击 **[!UICONTROL 创建区段]**.

![](../images/user-guide/segments.png)

的 **区段生成器** 中。 左边 **[!UICONTROL 字段]** 列和下 **[!UICONTROL 属性]** 选项卡上，单击名为 **[!UICONTROL XDM个人配置文件]** 然后，单击具有您组织命名空间的文件夹。 文件夹名为 **[!UICONTROL 客户人工智能]** 包含预测运行的结果，并以得分所属的实例命名。 单击实例文件夹以访问所需实例的结果。

![](../images/user-guide/results.png)

在区段生成器的中心，拖放 **[!UICONTROL 得分]** 属性 *规则生成器画布* 定义规则。

右下 *区段属性* 列中，提供区段的名称。

![](../images/user-guide/properties.png)

在左上方 *字段* 列，单击 **齿轮** 图标，然后选择 *合并策略* 从下拉菜单中。 单击 **[!UICONTROL 保存]** 创建区段。

![](../images/user-guide/merge_policy.png)

## 后续步骤

通过阅读本教程，您已使用区段生成器成功找到了基于受众倾向得分的受众。 您现在可以通过将受众激活到目标来定位受众。 请参阅 [目标概述](../../../destinations/home.md) 以了解更多信息。
