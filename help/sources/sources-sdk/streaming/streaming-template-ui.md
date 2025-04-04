---
title: 适用于流SDK UI的文档自助服务模板
description: 了解如何使用UI将流数据从源引入Adobe Experience Platform。
exl-id: 82254be0-fa31-4114-a0ec-179a990e0904
badge: Beta 版
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

---

# 使用UI创建源连接和数据流以流式传输&#x200B;*YOURSOURCE*&#x200B;数据

*浏览此模板时，替换或删除所有斜体段落（从此段落开始）。*

*从更新页面顶部的元数据（标题和描述）开始。 请忽略此页面上的所有UICONTROL实例。 此标记可帮助我们的机器翻译流程将页面正确翻译为我们支持的多种语言。 我们将在您提交文档后向文档中添加标记。*

本教程提供了使用Experience Platform用户界面创建&#x200B;*YOURSOURCE*&#x200B;源连接器的步骤。

## 概述

*提供贵公司的简短概述，包括贵公司为客户提供的价值。 包括产品文档主页的链接，以便进一步阅读。*

>[!IMPORTANT]
>
>此源连接器和文档页面由&#x200B;*YOURSOURCE*&#x200B;团队创建和维护。 对于任何查询或更新请求，请直接通过&#x200B;*插入链接或电子邮件地址与他们联系，您可以在此联系以获取更新*。

## 先决条件

*在此部分添加有关客户在Adobe Experience Platform用户界面中开始设置源之前需要了解的任何信息。 这可能大约为：*

* *需要添加到允许列表*
* 电子邮件散列的&#x200B;*要求*
* *你方的任何帐户详情*
* *如何获取身份验证凭据以连接到您的平台*

### 收集所需的凭据

要将&#x200B;*YOURSOURCE*&#x200B;连接到Experience Platform，必须提供以下连接属性的值：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| *凭据1* | *请在此处*&#x200B;向源身份验证凭据添加简要说明 | *请在此处添加源身份验证凭据的示例* |
| *凭据二* | *请在此处*&#x200B;向源身份验证凭据添加简要说明 | *请在此处添加源身份验证凭据的示例* |
| *凭据三* | *请在此处*&#x200B;向源身份验证凭据添加简要说明 | *请在此处添加源身份验证凭据的示例* |

有关这些凭据的详细信息，请参阅&#x200B;*YOURSOURCE*&#x200B;身份验证文档。 *请在此处*&#x200B;添加指向您平台的身份验证文档的链接。

### 将&#x200B;*YOURSOURCE*&#x200B;与webhook集成

*流式传输SDK要求您的源能够支持Webhook以便与Experience Platform通信。 在本节中，您必须提供用户必须遵循的步骤，才能将YOURSOURCE与webhook集成。*

## 连接您的&#x200B;*YOURSOURCE*&#x200B;帐户

在Experience Platform UI中，从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;**流**&#x200B;类别下，选择&#x200B;*YOURSOURCE*，然后选择&#x200B;**[!UICONTROL 添加数据]**。

>[!TIP]
>
>下面使用的屏幕截图是示例。 在创建文档时，请将图像替换为实际源的屏幕快照。 您可以使用相同的标记模式和颜色，也可以使用相同的文件名。 请确保屏幕截图会捕获整个Experience Platform UI屏幕。 有关如何上载屏幕截图的信息，请参阅[提交文档以供审阅](../documentation/github.md)上的指南。

![Experience Platform源目录](../assets/streaming/catalog.png)

## 选择数据

此时将显示&#x200B;**[!UICONTROL 选择数据]**&#x200B;步骤，该步骤为您提供了一个界面来选择将带到Experience Platform的数据。

* 界面的左侧是一个浏览器，允许您查看帐户内的可用数据流；
* 界面的右侧部分允许您预览JSON文件中最多100行数据。

选择&#x200B;**[!UICONTROL 上载文件]**&#x200B;以从本地系统上载JSON文件。 或者，您也可以将要上传的JSON文件拖放到[!UICONTROL 拖放文件]面板。

![源工作流的添加数据步骤。](../assets/streaming/add-data.png)

上传文件后，预览界面会更新，以显示您上传的架构预览。 预览界面允许您检查文件的内容和结构。 您还可以使用[!UICONTROL 搜索字段]实用工具访问架构中的特定项目。

完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![源工作流的预览步骤。](../assets/streaming/preview.png)

## 数据流详细信息

此时将显示&#x200B;**数据流详细信息**&#x200B;步骤，该步骤为您提供了使用现有数据集或为数据流建立新数据集的选项，以及提供数据流名称和描述的机会。 在此步骤中，您还可以配置配置文件摄取、错误诊断、部分摄取和警报的设置。

完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![源工作流的数据流详细信息步骤。](../assets/streaming/dataflow-detail.png)

## 映射

此时将显示[!UICONTROL 映射]步骤，该步骤为您提供了一个接口，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

Experience Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以派生计算值或计算值。 有关使用映射器界面和计算字段的全面步骤，请参阅[数据准备UI指南](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html)。

成功映射源数据后，选择&#x200B;**[!UICONTROL 下一步]**。

![源工作流的映射步骤。](../assets/streaming/mapping.png)

## 审查

将显示&#x200B;**[!UICONTROL 审核]**&#x200B;步骤，允许您在创建新数据流之前对其进行审核。 详细信息分为以下类别：

* **[!UICONTROL 连接]**：显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **[!UICONTROL 分配数据集和映射字段]**：显示要将源数据摄取到哪个数据集，包括数据集所遵循的架构。

查看数据流后，单击&#x200B;**[!UICONTROL 完成]**&#x200B;并留出一些时间来创建数据流。

![源工作流的审核步骤。](../assets/streaming/review.png)

## 获取您的流端点URL

创建流数据流后，您现在可以检索流端点URL。 此端点将用于订阅您的webhook，允许您的流源与Experience Platform通信。

要检索您的流端点，请转到刚刚创建的数据流的[!UICONTROL 数据流活动]页面，并从[!UICONTROL 属性]面板的底部复制端点。

![数据流活动中的流终结点。](../assets/testing/endpoint-test.png)

## 后续步骤

*用于创建数据流的其余步骤的工作流将被模块化。 如果您想针对您的源发起任何特定的号召，请参阅下面的其他资源部分。*

通过学习本教程，您已建立与&#x200B;*YOURSOURCE*&#x200B;帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html)。

## 其他资源

*本部分是一个可选部分，您可以在此提供更多链接，以指向您的产品文档或任何其他您认为对客户取得成功很重要的步骤、屏幕截图和细微差别。 您可以使用此部分添加有关源整个工作流的信息或提示，尤其是当存在最终用户可能遇到的特定“疑问”时。*
