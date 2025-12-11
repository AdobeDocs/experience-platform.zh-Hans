---
title: 库
description: 了解标记库的概念以及标记库在Adobe Experience Platform中的运行方式。
exl-id: 4d6f86e6-5684-4635-aaf1-87ba10cd7d94
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 67%

---

# 库

库由一系列指令构成，这些指令用于指示扩展、数据元素和规则在部署后如何相互交互。 创建库时，您可以指定要对库进行的更改。 生成时，这些更改将与在之前的库中提交、批准或发布的所有内容组合到一起。

库中包含对以下项目的添加或移除：

* 规则
* 元素
* 扩展配置

必须先将库分配到环境，然后才能将其编译到内部版本中。 库将作为一个整体获得批准或拒绝。您无法批准或拒绝库中的单个项目。 在发布工作流程中，库将在多个环境之间移动。

## 创建库 {#create-a-library}

要创建库，请完成以下步骤。

1. 打开 [!UICONTROL Publishing] 选项卡。

   [!UICONTROL Publishing] 页面会列出开发库，并提供提交这些库以供审批、将其移至暂存环境或将其发布到生产环境的方法。

1. 选择 **[!UICONTROL Add New Library]**。

   ![](../../images/library-create.jpg)

1. 命名库。
1. 将库分配到开发环境。
1. 向库中添加更改。要添加项目，请选择 **[!UICONTROL Add a Change]**，然后选取要添加的项目。任何已编辑或已删除的项目均可添加到所选库中。

   ![](../../images/library-add-change.jpg)

   您可以将以下项目添加到库中：

   * 规则
   * 数据元素
   * 扩展配置

1. 要添加任何已更改的资源，请选择 **[!UICONTROL Add All Changed Resources]**。
1. 选择 **[!UICONTROL Save]** 或 **[!UICONTROL Save and Build for Development]**。

   部署时将编译一个内部版本并将其部署到所分配的环境。

创建库后，可使用该库的下拉菜单选择以下任一选项：

* **编辑**：此选项允许您更改库配置。

* **用于开发的内部版本**：此选项编译内部版本并将其部署到分配的环境。

* **提交以供审批**：此选项使库可供审批者将其移至发布流程中的下一步。

* **删除**：此选项从发布流程中删除当前选定的库。

![](../../images/library-menu.png)

## 添加到库 {#add-to-a-library}

要将添加到库，请完成以下步骤。

1. 安装要添加的[扩展](../managing-resources/extensions/overview.md)。
1. 创建要添加的[数据元素](../managing-resources/data-elements.md)和规则。
1. 打开 **[!UICONTROL Publishing]** 选项卡。
1. 选择要更改的[库](libraries.md)，然后选择 **[!UICONTROL Edit]**。
1. 使用规则、数据元素和扩展按钮选择要添加到库中的项目。
1. 保存更改。

对库所做的更改将显示在库内容更改日志中。

>[!NOTE]
>
>数据元素依赖于扩展；而规则同时依赖于数据元素和扩展。如果您的库中未包含所有必需组件，则在生成时将失败，为此，您需要添加必需的组件，然后才能成功完成生成。以后发行的版本将在对库进行更改时检查依赖关系。

## 从库中移除项目

要从库中移除某个项目，必须先将其停用，然后再发布已停用状态。

1. 禁用要移除的扩展，以及依赖这些扩展的任何数据元素和规则。
1. 禁用要移除的数据元素和规则。
1. 打开 **[!UICONTROL Publishing]** 选项卡。
1. 选择要更改的库。
1. 使用规则、数据元素和扩展按钮选择要从库中移除的已禁用项目。
1. 保存更改。

## 管理库更改

要编辑库选项，请完成以下步骤。

1. 选择库，然后选择 **[!UICONTROL Edit]** 以查看库更改。所有更改都将显示在 [!UICONTROL Library Contents] 列表中。

   ![](../../images/library-contents.jpg)

1. 选择要查看的更改，然后选择修订版本。

   ![](../../images/library-contents-revision.jpg)

1. 选择是显示&#x200B;**所有**&#x200B;项还是&#x200B;**已更改**&#x200B;项。
1. 选择修订版本，然后选择 **[!UICONTROL Select Revision]**。
1. 选择 **[!UICONTROL Add a Change]** 或 **[!UICONTROL Add All Changed Resources]**。

## 活动库 {#active-library}

库可以封装一系列您希望对已部署代码进行的更改。活动库可以为您提供更大的便利，允许您快速循环访问各项更改并查看相应影响。

扩展、规则和数据元素现在可以直接保存到您正在处理的库中。 如果需要，还可以从[!UICONTROL Active Library]下拉列表中创建新内部版本，甚至创建新库。

以下列表提供了有关管理活动库的更多信息。

1. [创建一个新库](libraries.md#create-a-library)。
1. 转到[规则](../managing-resources/rules.md)、[数据元素](../managing-resources/data-elements.md)或[扩展](../managing-resources/extensions/overview.md)。
1. 选择您的活动库。
1. 进行更改，然后保存并生成库。
1. 测试所做的更改，并根据需要重复这些步骤。
