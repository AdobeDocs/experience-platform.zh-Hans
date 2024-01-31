---
solution: Experience Platform
title: 用例行动手册中的数据意识概述
description: 了解如何通过将最终启发型沙盒中生成的资源复制到其他沙盒来加快实现价值。
role: Developer
exl-id: 537eff13-f5fe-4cc9-9769-ab47b3cecda7
source-git-commit: ecce42e2c759bda31bc37d0aae1da2c7b3d141fc
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# 将行动手册生成的资源发布到其他沙盒 {#publish-to-other-sandboxes}

用例行动手册是营销模板，旨在为常见营销用例生成受众、架构或历程等资产。 您可以在启发性的沙盒中测试行动手册创建的资产，并在准备就绪后，将资产导入其他开发沙盒，以便进一步使用在这些沙盒中可用的数据进行测试。 对测试感到满意后，您可以将资产从开发沙盒移至生产沙盒。

但是，在某些情况下，您可能已经在其他开发沙盒中设置自己的架构、字段和字段组。 这可能会使用例模板生成的某些资产（例如历程）与您的数据不兼容。 要了解如何使用数据感知功能更好地使生成的资源与现有资源对应和补充，请阅读本教程。

## 先决条件 {#prerequisites}

在阅读本教程之前，请浏览 [可用的用例剧本模板](/help/use-case-playbooks/playbooks/discover.md#search-and-filter) 和 [创建实例](/help/use-case-playbooks/playbooks/create-share-reuse.md) 偏好的剧本。

创建实例会在启发型沙盒中生成一组资源，例如历程、区段、架构和消息。 请阅读并了解如何将这些资源复制到其他沙盒中。

### 创建和发布资源包 {#create-publish-package}

>[!NOTE]
>
> 您只能将包导入其他开发沙盒中。 完成所有必要的更改或更新后，您可以将资源或包从这些开发沙盒导入到生产环境中。 您无法直接从用例行动手册沙盒导入到生产环境。

1. 要将启发性的沙盒中的对象导入另一个沙盒，请浏览到用例剧本的所需实例，然后选择 **[!UICONTROL 发布到其他沙盒]** 将对象导出为文件包。

   ![显示不同用例实例的GIF](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. 一旦您选择 **[!UICONTROL 发布到其他沙盒]** 按钮，此时将显示一个模式窗口。 填写名称和可选说明，然后选择 **[!UICONTROL 创建]**. 此步骤将生成的资源捆绑到一个包中，该包可以导入到其他沙盒中。

   ![用于创建资源包的模式](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. 导航至 **沙盒** 页面，然后选择 **包** 选项卡，找到您的包并将其发布。 要发布处于草稿状态的资源包，请按照 [沙盒工具](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish) 文档。

   ![处于草稿或未发布状态的包](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![发布包](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. 发布成功后，在包浏览页面上，您应会看到 **+** 名称旁边的“已启用”按钮。

   ![“沙盒”页面中的“包”选项卡](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > 当包仍处于草稿模式时，无法导入包，因此打开包详细信息页面并发布包。

5. 选择 **+** 控制并启动工作流以将用例剧本生成的资产导入 **[!UICONTROL Target沙盒]**. 选择目标沙盒，然后使用下拉菜单确认您要导入的包名称。 在继续下一步之前，请添加作业详细信息，例如作业名称和作业描述。

   ![启动导入工作流，选择目标，确认包，添加作业详细信息。](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

6. 在 **[!UICONTROL 查看依赖关系]** 步骤，您可以将架构映射并将其他资产从启发型沙盒复制到目标沙盒中。 此 **[!UICONTROL 完成]** 在映射每个架构之前，按钮处于禁用状态。

   ![在“查看依赖项”步骤中映射架构，启用“完成”按钮。](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### 映射架构 {#map-schemas}

1. 映射第一个架构。 架构映射对话框显示一个下拉列表，用于选择目标架构。 如果源架构是配置文件架构，则除了 [单个合并配置文件架构](/help/xdm/classes/individual-profile.md). 首次显示页面时，您可以看到源数据和目标字段之间自动生成的映射推荐。 通过选择目标字段，然后选择新字段可以编辑映射。 如果修改建议的映射，请使用 **验证** 按钮验证新映射并显示任何可能链接到新映射的错误。 选择 **保存** 映射完成后。

   ![架构映射对话框，其中包含用于选择目标架构的下拉列表。](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. 继续映射架构中的所有字段。 如果架构是 [事件架构](/help/xdm/classes/experienceevent.md)，该对话框显示一个下拉列表，您可在其中查看target沙盒中的所有事件架构。

   ![从下拉列表中选择目标架构](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. 从的可用架构中选择架构 **Target沙盒**.

   ![选择架构](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. 完成映射并选择 **保存**.

   ![保存映射](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. 完成映射架构中的所有字段后，选择 **完成** 以完成导入工作流。

   ![完成流程](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > 您无法修改架构以外的任何资产，因为这是一个鼓舞人心的沙盒，但它们确实显示为包的依赖项。

### 导入状态 {#import-status}

1. 系统会自动将您重定向到 [**导入**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details) 可在其中查看导入进度的页面。

   ![显示导入进度的页面](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. 在导入包时，将在目标沙盒中创建包的资产。 完成后，它们将引用您在导入过程中映射的字段。 该过程现已完成，灵感沙盒中的资产现在也位于您的目标沙盒中以供您测试。

   ![在目标沙盒中生成的资源](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## 后续步骤

阅读本指南后，您现在可以更好地了解如何利用用例行动手册以及 [沙盒工具](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details) 创建引用架构的可执行历程。 了解关于常见问题的更多信息 [Real-Time CDP用例](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md).
