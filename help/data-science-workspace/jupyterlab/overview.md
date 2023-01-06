---
keywords: Experience Platform;JupyterLab；笔记本；Data Science Workspace；热门主题；jupyterlab
solution: Experience Platform
title: JupyterLab UI概述
description: JupyterLab是Project Jupyter的基于Web的用户界面，与Adobe Experience Platform紧密集成。 它为数据科学家提供了一个交互式开发环境，以便与Jupyter Notebooks、代码和数据合作。 本文档概述了JupyterLab及其功能以及执行常见操作的说明。
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 3%

---

# [!DNL JupyterLab] UI概述

[!DNL JupyterLab] 是 [朱佩特工程](https://jupyter.org/) 与Adobe Experience Platform紧密结合。 它为数据科学家提供了一个交互式开发环境，以便与Jupyter Notebooks、代码和数据合作。

本文档提供了 [!DNL JupyterLab] 以及执行常见操作的说明。

## [!DNL JupyterLab] on [!DNL Experience Platform]

Experience Platform的JupyterLab集成附带体系结构更改、设计注意事项、自定义的笔记本扩展、预安装的库以及以Adobe为主题的界面。

以下列表概述了JupyterLab在Platform上独有的一些功能：

| 功能 | 描述 |
| --- | --- |
| **内核** | 内核提供笔记本和其他 [!DNL JupyterLab] 前端能够以不同的编程语言执行和检查代码。 [!DNL Experience Platform] 提供了其他内核，用于支持 [!DNL Python]、 R、PySpark和 [!DNL Spark]. 请参阅 [核](#kernels) 部分以了解更多详细信息。 |
| **数据访问** | 直接从内部访问现有数据集 [!DNL JupyterLab] 完全支持读写功能。 |
| **[!DNL Platform]服务集成** | 内置集成允许您利用其他 [!DNL Platform] 直接从内部 [!DNL JupyterLab]. 在 [与其他Platform服务集成](#service-integration). |
| **身份验证** | 除 <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">JupyterLab的内置安全模型</a>，则您的应用程序与Experience Platform之间的每次交互（包括平台服务到服务通信）都会通过 <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **开发库** | 在 [!DNL Experience Platform], [!DNL JupyterLab] 为 [!DNL Python]、R和PySpark。 请参阅 [附录](#supported-libraries) 以获取支持的库的完整列表。 |
| **库控制器** | 如果您没有预安装的库以满足您的需求，则可以为Python和R安装其他库，并将其临时存储在独立的容器中以保持 [!DNL Platform] 保证数据安全。 请参阅 [核](#kernels) 部分以了解更多详细信息。 |

>[!NOTE]
>
>其他库仅可用于安装它们的会话。 启动新会话时，必须重新安装所需的任何其他库。

## 与其他 [!DNL Platform] 服务 {#service-integration}

标准化和互操作性是其背后的关键概念 [!DNL Experience Platform]. 集成 [!DNL JupyterLab] on [!DNL Platform] 作为嵌入式IDE，它可以与其他 [!DNL Platform] 服务，让您能够利用 [!DNL Platform] 充分发挥潜力。 以下 [!DNL Platform] 服务在 [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** 访问和探索具有读写功能的数据集。
* **[!DNL Query Service]:** 使用SQL访问和浏览数据集，在处理大量数据时提供更低的数据访问开销。
* **[!DNL Sensei ML Framework]:** 能够训练和评分数据的模型开发，以及通过单击创建方法。
* **[!DNL Experience Data Model (XDM)]:** 标准化和互操作性是Adobe Experience Platform背后的关键概念。 [体验数据模型(XDM)](https://www.adobe.com/go/xdm-home-en)在Adobe的驱动下，努力标准化客户体验数据并定义客户体验管理模式。

>[!NOTE]
>
>部分 [!DNL Platform] 服务集成 [!DNL JupyterLab] 仅限于特定内核。 请参阅 [核](#kernels) 以了解更多详细信息。

## 主要功能和常见操作

有关 [!DNL JupyterLab] 以下各节提供了有关执行常见操作的说明：

* [访问JupyterLab](#access-jupyterlab)
* [JupyterLab接口](#jupyterlab-interface)
* [代码单元格](#code-cells)
* [内核](#kernels)
* [内核会话](#kernel-sessions)
* [启动器](#launcher)

### 访问 [!DNL JupyterLab] {#access-jupyterlab}

在 [Adobe Experience Platform](https://platform.adobe.com)，选择 **[!UICONTROL 笔记本]** 从左侧导航列。 允许一些时间 [!DNL JupyterLab] 完全初始化。

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] 界面 {#jupyterlab-interface}

的 [!DNL JupyterLab] 界面由菜单栏、可折叠的左侧栏以及包含文档和活动选项卡的主工作区组成。

**菜单栏**

界面顶部的菜单栏具有可显示 [!DNL JupyterLab] 使用其键盘快捷键：

* **文件：** 与文件和目录相关的操作
* **编辑：** 与编辑文档和其他活动相关的操作
* **查看：** 更改外观的操作 [!DNL JupyterLab]
* **运行：** 在不同活动（如笔记本和代码控制台）中运行代码的操作
* **内核：** 用于管理内核的操作
* **选项卡：** 打开的文档和活动列表
* **设置：** 常用设置和高级设置编辑器
* **帮助：** 列表 [!DNL JupyterLab] 和内核帮助链接

**左侧栏**

左侧的侧栏包含可单击的选项卡，这些选项卡提供对以下功能的访问：

* **文件浏览器：** 保存的笔记本文档和目录列表
* **数据资源管理器：** 浏览、访问和浏览数据集和模式
* **运行内核和终端：** 能够终止的活动内核和终端会话的列表
* **命令：** 有用命令的列表
* **单元格检查器：** 单元格编辑器，提供对工具和元数据的访问，这些工具和元数据可用于设置用于演示目的的笔记本
* **选项卡：** 打开的选项卡列表

选择一个选项卡以显示其功能，或在展开的选项卡上选择以折叠左侧边栏，如下所示：

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**主要工作区**

主要工作领域 [!DNL JupyterLab] 允许您将文档和其他活动排列到选项卡的面板中，这些选项卡可以调整大小或进行细分。 将选项卡拖动到选项卡面板的中心，以迁移选项卡。 将面板除以向面板的左、右、顶或底部拖动制表符：

![](../images/jupyterlab/user-guide/main_work_area.gif)

### 中的GPU和内存服务器配置 [!DNL Python]/R

在 [!DNL JupyterLab] 选择右上角的齿轮图标以打开 *笔记本服务器配置*. 您可以打开GPU并使用滑块分配所需的内存量。 您可以分配的内存量取决于贵组织已配置的内存量。 选择 **[!UICONTROL 更新配置]** 保存。

>[!NOTE]
>
>每个组织只为笔记本配置一个GPU。 如果GPU正在使用，则需要等待当前已保留GPU的用户释放该GPU。 这可以通过注销或将GPU保留在空闲状态四小时或更长时间来完成。

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### 终止并重新启动 [!DNL JupyterLab]

在 [!DNL JupyterLab]，则可以终止会话以阻止使用其他资源。 首先，选择 **电源图标** ![电源图标](../images/jupyterlab/user-guide/power_button.png)，然后选择 **[!UICONTROL 关闭]** 中的“终止会话”对话框。 笔记本会话在没有活动12小时后自动终止。

要重新启动，请执行以下操作 [!DNL JupyterLab]，选择 **重新启动图标** ![重新启动图标](../images/jupyterlab/user-guide/restart_button.png) 位于电源图标的左侧，然后选择 **[!UICONTROL 重新启动]** 中。

![终止jupterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### 代码单元格 {#code-cells}

代码单元格是笔记本的主要内容。 它们包含以笔记本关联内核的语言和作为执行代码单元结果的输出的源代码。 每个代码单元格的右侧将显示执行计数，该代码单元格表示其执行顺序。

![](../images/jupyterlab/user-guide/code_cell.png)

常见单元格操作描述如下：

* **添加单元格：** 单击加号(**+**)以添加空单元格。 新单元格放置在当前正在交互的单元格下，或者如果没有特定单元格处于焦点中，则放置在笔记本的末尾。

* **移动单元格：** 将光标放在要移动的单元格右侧，然后单击并将单元格拖动到新位置。 此外，将单元格从一个笔记本移动到另一个笔记本会复制该单元格及其内容。

* **执行单元格：** 单击要执行的单元格的正文，然后单击 **play** 图标(**▶**)。 星号(**\***)会在内核处理执行时显示在单元格的执行计数器中，并在完成后被替换为整数。

* **删除单元格：** 单击要删除的单元格的正文，然后单击 **剪刀** 图标。

### 内核 {#kernels}

笔记本内核是处理笔记本单元的语言专用计算引擎。 除 [!DNL Python], [!DNL JupyterLab] 在R、PySpark和 [!DNL Spark] （斯卡拉）。 打开笔记本文档时，将启动关联的内核。 当执行笔记本单元时，内核执行计算并产生可能消耗大量CPU和内存资源的结果。 请注意，在内核关闭之前，不会释放已分配的内存。

某些特性和功能仅限于下表所述的特定内核：

| 内核 | 库安装支持 | [!DNL Platform] 集成 |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **斯卡拉** | 否 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### 内核会话 {#kernel-sessions}

每个活动笔记本或活动 [!DNL JupyterLab] 利用内核会话。 通过展开 **运行终端和内核** 选项卡。 可通过观察笔记本界面的右上方来识别笔记本的内核类型和状态。 在下图中，笔记本的关联内核是 **[!DNL Python]3** 其当前状态由右侧的灰色圆表示。 空心圆表示空闲内核，实心圆表示忙内核。

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

如果内核已关闭或处于非活动状态一段时间，则 **没有内核！** 显示实心圆。 通过单击内核状态并选择相应的内核类型来激活内核，如下所示：

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### 启动器 {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

自定义 *启动器* 为支持的内核提供了有用的笔记本模板，以帮助您启动任务，包括：

| 模板 | 描述 |
| --- | --- |
| 空白 | 空的笔记本文件。 |
| 入门 | 预填充的笔记本演示使用示例数据进行数据探索。 |
| 零售销售 | 预装的笔记本 [零售销售方法](../pre-built-recipes/retail-sales.md) 使用示例数据。 |
| 方法生成器 | 用于在 [!DNL JupyterLab]. 它预填充了用于演示和描述方法创建过程的代码和评注。 请参阅 [笔记本 — 方法教程](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) 详细的演练。 |
| [!DNL Query Service] | 预填充的笔记本，用于演示 [!DNL Query Service] 直接 [!DNL JupyterLab] 提供了可大规模分析数据的示例工作流。 |
| XDM事件 | 预填充的笔记本，展示了关于后值体验事件数据的数据探索，重点介绍整个数据结构中通用的功能。 |
| XDM查询 | 一个预填充的笔记本，用于演示有关Experience Event数据的示例业务查询。 |
| 聚合 | 预填充的笔记本，展示了将大量数据聚合为更小、可管理的块的示例工作流。 |
| 聚类 | 一种预填充的笔记本，用于演示使用聚类算法的端到端机器学习建模过程。 |

某些笔记本模板仅限于某些内核。 下表映射了每个内核的模板可用性：

<table>
    <tr>
        <td></td>
        <th><strong>空白</strong></th>
        <th><strong>入门</strong></th>
        <th><strong>零售销售</strong></th>
        <th><strong>方法生成器</strong></th>
        <th><strong>[!DNL Query Service]</strong></th>
        <th><strong>XDM事件</strong></th>
        <th><strong>XDM查询</strong></th>
        <th><strong>聚合</strong></th>
        <th><strong>聚类</strong></th>
    </tr>
    <tr>
        <th><strong>[!DNL Python]</strong></th>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
    </tr>
    <tr>
        <th ><strong>R</strong></th>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
    </tr>
      <tr>
        <th  ><strong>PySpark 3([!DNL Spark] 2.4)</strong></th>
        <td >否</td>
        <td >是</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >是</td>
        <td >是</td>
        <td >否</td>
    </tr>
    <tr>
        <th ><strong>斯卡拉</strong></th>
        <td >是</td>
        <td >是</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >否</td>
        <td >是</td>
    </tr>
</table>

打开新 *启动器*，单击 **文件>新建启动器**. 或者，展开 **文件浏览器** 从左侧边栏中，单击加号(**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## 后续步骤

要进一步了解每个受支持的笔记本以及如何使用它们，请访问 [Jupyterlab笔记本数据访问](./access-notebook-data.md) 开发人员指南。 本指南重点介绍如何使用JupyterLab笔记本访问数据，包括读取、写入和查询数据。 数据访问指南还包含有关每个受支持的笔记本可读取的最大数据量的信息。

## 支持的库 {#supported-libraries}

有关Python、R和PySpark中支持的包列表，请复制并粘贴 `!conda list` 在新单元格中，然后运行该单元格。 按字母顺序填充受支持包的列表。

![示例](../images/jupyterlab/user-guide/libraries.PNG)

此外，还使用了以下依赖项，但未列出这些依赖项：
* CUDA 11.2
* CUDNN 8.1

