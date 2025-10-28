---
title: 受众构成增强功能
description: 了解针对受众构成所做的增强功能，包括受众扩充和更快的激活。
hide: true
hidefromtoc: true
source-git-commit: 9c790f0b47161301fa8c02c4afb7edfb925e1499
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# 受众构成增强功能

您现在可以访问受众构成的&#x200B;**两个**&#x200B;增强功能：

- [受众扩充](#audience-enrichment)
- [更快的激活](#faster-activation)

## 受众扩充 {#audience-enrichment}

通过受众扩充，可输出值数组，使您的配置文件符合您创建的受众的条件。

要在合成中添加受众扩充，请选择画布中最顶部的&#x200B;**[!UICONTROL Audience]**&#x200B;块。 为受众指定名称后，选择&#x200B;**[!UICONTROL Build rule]**&#x200B;以打开规则生成器画布。

![受众块以及“生成规则”按钮突出显示。](/help/segmentation/images/ui/composition-enhancements/select-build-rule.png)

此时将显示规则生成器画布。 您现在可以创建用于受众扩充的筛选条件。 此筛选条件&#x200B;**必须**&#x200B;包含数组中的属性。 作为数组的属性取决于贵组织的架构结构。 创建筛选条件后，在右侧面板中选择&#x200B;**[!UICONTROL Delivery]**。

![规则生成器画布显示可以具有扩充功能的受众示例。 传递按钮也突出显示。](/help/segmentation/images/ui/composition-enhancements/view-delivery.png)

从左侧面板的列表中选择要用于扩充的对象数组。 如果配置文件上只有一个数组，则会自动为您选择该数组。 选择&#x200B;**[!UICONTROL Save]**&#x200B;以返回到受众合成。

<!-- , as well as the fields you want to be used in the enrichment. -->

![将显示扩充树的架构树。](/help/segmentation/images/ui/composition-enhancements/view-schema-tree.png)

在受众组合中，[!UICONTROL Audience]块现在为“[!UICONTROL Rule builder with enhancement]”类型。 选择&#x200B;**[!UICONTROL Publish]**&#x200B;以通过下一个每日批次激活您的受众。

![受众块已突出显示，表明已添加具有扩充的受众。](/help/segmentation/images/ui/composition-enhancements/rule-builder-with-enrichment.png)

### 行为详细信息和护栏

在使用受众扩充时，请牢记以下详细信息和防护：

- 您只能在受众组合内创建的受众中使用受众扩充
- 合成&#x200B;**中使用的第一个块必须**&#x200B;是基于规则的受众。
- 您&#x200B;**不能**&#x200B;在组合中使用任何其他操作。
- 发布后，您&#x200B;**无法**&#x200B;编辑基于规则的受众上的合成。
   - 如果要更改基本构成或基于规则的受众，您可以&#x200B;*将构成复制到草稿中并编辑草稿。*
- 仅&#x200B;**one**&#x200B;对象数组可用于在单个受众中生成扩充有效负载
   - 有效负载数组可以嵌套在对象中（在配置文件架构中最多七个层），但&#x200B;**不能包含在其他数组中**。
   - 有效负载数组&#x200B;**必须**&#x200B;具有50行或更少的行。
   - 有效负载&#x200B;**中的所有列输出都必须是**&#x200B;基元类型。
   - 仅输出数组的前&#x200B;**20**&#x200B;列。
- 此时仅可使用&#x200B;**10**&#x200B;个受众合成

## 更快的激活 {#faster-activation}

通过更快的激活，您可以在评估构成后立即将受众激活到下游目标。 因此，如果目标设置为在区段评估后激活，则无需等待24小时即可完成评估作业。

有关详细信息，请参阅[将受众激活到批处理配置文件目标指南](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)。
