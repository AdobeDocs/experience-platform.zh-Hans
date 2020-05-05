---
keywords: Experience Platform;machine learning model;Data Science Workspace;Real-time Customer Profile;popular topics
solution: Experience Platform
title: 利用机器学习洞察丰富实时客户用户档案
topic: Tutorial
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# 利用机器学习洞察丰富实时客户用户档案

Adobe Experience Platform Data Science Workspace提供用于创建、评估和利用机器学习模型生成数据预测和洞察的工具和资源。 当机器学习洞察被引入支持用户档案的数据集时，同一数据也被引入用户档案记录，然后，通过使用Experience Platform Segmentation Service将这些数据细分为相关元素的子集。

此文档提供分步教程，用于通过机器学习洞察丰富实时客户用户档案，步骤分为以下几节：

1. [创建输出模式和数据集](#create-an-output-schema-and-dataset)
2. [配置输出模式和数据集](#configure-an-output-schema-and-dataset)
3. [使用区段生成器创建区段](#create-segments-using-the-segment-builder)

## 入门指南

本教程需要对Adobe Experience Platform的各个方面进行有效的了解，这些方面涉及用户档案数据的获取和细分的创建。 在开始本教程之前，请查看以下服务的相关文档：

* [实时客户用户档案](../../rtcdp/overview.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
* [身份服务](../../identity-service/home.md): 通过将来自不同数据源的身份融入平台，实现实时客户用户档案。
* [体验数据模型(XDM)](../../xdm/home.md): 平台组织客户体验数据的标准化框架。

除了上述文档之外，还强烈建议您查看以下模式和模式编辑指南：

* [模式合成基础](../../xdm/schema/composition.md): 介绍XDM模式、构件、原则和最佳做法，以组成要在Experience Platform中使用的模式。
* [模式编辑器教程](../../xdm/tutorials/create-schema-ui.md): 提供有关使用Experience Platform中的模式编辑器创建模式的详细说明。

## 创建输出模式和数据集 {#create-an-output-schema-and-dataset}

通过评分洞察丰富实时客户用户档案的第一步是了解数据定义的真实对象（如人）。 了解数据使您能够描述和设计对数据有意义的结构，就像设计关系数据库一样。

编写模式从指定类开始。 类定义模式将包含的数据的行为方面（记录或时间序列）。 本节提供使用模式生成器创建模式的基本说明。 有关更详细的教程，请参阅有关使用 [模式编辑器创建模式的教程](../../xdm/tutorials/create-schema-ui.md)。

1. 在Adobe Experience Platform上，单击选 **[!UICONTROL Schema]** 项卡以访问模式浏览器。 单击 **[!UICONTROL Create Schema]** 访问模式 *编辑器*，您可以在该编辑器中交互构建和创建模式。
   ![](../images/models-recipes/enrich-rtcdp/schema_browser.png)

2. 在“合 *成* ”窗口中， **[!UICONTROL Assign]** 单击以浏览可用类。
   * 要分配现有类，请单击并突出显示所需的类，然后单击 **[!UICONTROL Assign Class]**。
      ![](../images/models-recipes/enrich-rtcdp/existing_class.png)

   * 要创建自定义类，请单 **[!UICONTROL Create New Class]** 击浏览器窗口中心顶部附近的。 提供类名、说明，然后选择类的行为。 完成 **[!UICONTROL Assign Class]** 后单击。
      ![](../images/models-recipes/enrich-rtcdp/create_new_class.png)
   此时，模式的结构应包含一些类字段，您可以指定混音。 混音是由一个或多个字段组成的组，用于描述特定概念。

3. 在“合 *成* ”窗口中， **[!UICONTROL Add]** 单击“ *Mixins* ”子部分。
   * 要指定现有混音，请单击并高亮显示所需的混音，然后单击 **[!UICONTROL Add Mixin]**。 与类不同，只要适合，多个混音就可以分配给单个模式。
      ![](../images/models-recipes/enrich-rtcdp/existing_mixin.png)

   * 要创建新混音，请单击 **[!UICONTROL Create New Mixin]** 浏览器窗口中心顶部附近的“找到”。 提供混音的名称和说明，然后 **[!UICONTROL Assign Mixin]** 单击完成。
      ![](../images/models-recipes/enrich-rtcdp/create_new_mixin.png)

   * 要添加混音字段，请在“合成”窗口中单击混音 *的名* 称。 随后，将提供通过单击“结构”窗口添加混 **[!UICONTROL Add Field]** 音字段 *的选* 项。 确保相应地提供混合属性。
      ![](../images/models-recipes/enrich-rtcdp/mixin_properties.png)

4. 构建完模式后，在“结构”窗口中单击模式的顶 *级字段* ，在右侧属性窗口中显示模式的属性。 提供名称和说明，然后单击 **[!UICONTROL Save]** 以创建模式。
   ![](../images/models-recipes/enrich-rtcdp/save_schema.png)

5. 使用新创建的模式创建输出数据集， **[!UICONTROL Datasets]** 方法是从左侧导航列单击，然后单 **[!UICONTROL Create dataset]**&#x200B;击。 在下一个屏幕上，选择 **[!UICONTROL Create dataset from schema]**。
   ![](../images/models-recipes/enrich-rtcdp/dataset_overview.png)

6. 使用模式浏览器，找到并选择新创建的模式，然后单击 **[!UICONTROL Next]**。
   ![](../images/models-recipes/enrich-rtcdp/choose_schema.png)

7. 提供名称和可选说明，然后单击 **[!UICONTROL Finish]** 以创建数据集。
   ![](../images/models-recipes/enrich-rtcdp/configure_dataset.png)

现在您已创建输出模式数据集，您可以继续下一节，配置并启用这些数据集以进行用户档案扩充。

## 配置输出模式和数据集 {#configure-an-output-schema-and-dataset}

在启用用户档案集之前，您需要先配置数据集的模式，使其具有主标识字段，然后启用用户档案模式。 如果要创建并启用新模式，可参阅有关使用模式编 [辑器创建模式的教程](../../xdm/tutorials/create-schema-ui.md)。 否则，请按照以下说明启用现有模式和数据集。

1. 在Adobe Experience Platform上，使用模式浏览器查找要启用用户档案的输出模式，然后单击其名称以视图其合成。
   ![](../images/models-recipes/enrich-rtcdp/schemas.png)

2. 展开模式结构并查找要设置为主标识符的相应字段。 单击所需字段以显示其属性。
   ![](../images/models-recipes/enrich-rtcdp/schema_structure.png)

3. 通过启用字段的属性、属性，然后选 **[!UICONTROL Identity]** 择相 **[!UICONTROL Primary Identity]** 应的字段，将字段设置为主标识 **[!UICONTROL Identity Namespace]**。 进行 **[!UICONTROL Apply]** 更改后单击。
   ![](../images/models-recipes/enrich-rtcdp/set_identity.png)

4. 单击模式结构的顶级对象以显示模式属性，并通过切换开关启用用户档案 **[!UICONTROL Profile]** 。 单 **[!UICONTROL Save]** 击以完成更改，现在可以启用使用此模式创建的数据集进行用户档案。
   ![](../images/models-recipes/enrich-rtcdp/enable_schema.png)

5. 使用数据集浏览器查找要启用用户档案的数据集，并单击其名称以访问其详细信息。
   ![](../images/models-recipes/enrich-rtcdp/datasets.png)

6. 通过切换右侧信息列中 **[!UICONTROL Profile]** 的开关来启用用户档案集。
   ![](../images/models-recipes/enrich-rtcdp/enable_dataset.png)

当数据被收录到启用用户档案的数据集中时，同一数据也被收录为用户档案记录。 现在您的模式和数据集已准备就绪，可使用适当的模型执行评分运行，从而将一些数据生成到数据集中，并继续本教程以使用“区段生成器”创建洞察区段。

## 使用区段生成器创建区段 {#create-segments-using-the-segment-builder}

现在，您已经生成并引入了对支持用户档案的数据集的洞察，您可以通过使用区段生成器识别相关元素的子集来管理这些数据。 按照以下步骤构建您自己的细分。

1. 在Adobe Experience Platform上，单击选 **[!UICONTROL Segments]** 项卡，然 **[!UICONTROL Create Segment]** 后单击选项卡以访问Segment Builder。
   ![](../images/models-recipes/enrich-rtcdp/segments_overview.png)

2. 在区段生成器中，左边栏提供对核心区段构建块的访问： 属性、事件和现有细分。 每个构件块都显示在各自的选项卡中。 选择您的启用用户档案的模式所扩展的类，然后浏览并查找您的区段的构建块。
   ![](../images/models-recipes/enrich-rtcdp/segment_builder.png)

3. 将构建块拖放到规则构建器画布上，通过提供比较语句完成它们。
   ![](../images/models-recipes/enrich-rtcdp/drag_fill.gif)

4. 在构建细分时，您可以通过观察“细分属性”面板来预览估 *计的细分* 结果。
   ![](../images/models-recipes/enrich-rtcdp/preview_segment.gif)

5. 选择适当 **[!UICONTROL Merge Policy]**&#x200B;的区段，提供名称和可选说明，然后 **[!UICONTROL Save]** 单击以完成新区段。
   ![](../images/models-recipes/enrich-rtcdp/save_segment.png)


## 后续步骤 {#next-steps}

此文档会指导您完成启用模式和数据集进行用户档案所需的步骤，并简要演示了使用区段生成器创建分析区段的工作流。 要进一步了解区段和区段生成器，请参阅分段 [服务概述](../../segmentation/home.md)。