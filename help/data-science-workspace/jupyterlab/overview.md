---
keywords: Experience Platform;JupyterLab；笔记本；数据科学工作区；热门主题；jupyterlab
solution: Experience Platform
title: JupyterLab UI概述
topic: Overview
description: JupyterLab是Project Jupyter的基于Web的用户界面，与Adobe Experience Platform紧密集成。 它为数据科学家提供了一个交互式开发环境，以便他们能够与Jupyter笔记本、代码和数据一起工作。 本文档概述了JupyterLab及其功能以及执行常见操作的说明。
translation-type: tm+mt
source-git-commit: 9d84fc1eb898020ed4b154c091fcc9fc4933c7de
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 3%

---


# [!DNL JupyterLab] UI概述

[!DNL JupyterLab] 是Project Jupyter的基于web的用 [户](https://jupyter.org/) 界面，与Adobe Experience Platform紧密集成。它为数据科学家提供了一个交互式开发环境，以便他们能够与Jupyter笔记本、代码和数据一起工作。

本文档概述了[!DNL JupyterLab]及其功能以及执行常见操作的说明。

## [!DNL JupyterLab] on  [!DNL Experience Platform]

Experience Platform的JupyterLab集成附带了架构更改、设计注意事项、自定义的笔记本扩展、预安装的库和Adobe主题界面。

以下列表概述了JupyterLab在平台上独有的一些功能：

| 功能 | 描述 |
| --- | --- |
| **内核** | 内核提供笔记本和其他[!DNL JupyterLab]前端以不同编程语言执行和检查代码的能力。 [!DNL Experience Platform] 提供其他内核，支持 [!DNL Python]在、R、PySpark和中进行开发 [!DNL Spark]。有关详细信息，请参阅[kernel](#kernels)部分。 |
| **数据访问** | 直接从[!DNL JupyterLab]中访问现有数据集，并完全支持读写功能。 |
| **[!DNL Platform]服务集成** | 内置集成功能允许您直接从[!DNL JupyterLab]中使用其他[!DNL Platform]服务。 [与其他平台服务集成](#service-integration)部分提供了受支持集成的完整列表。 |
| **身份验证** | 除了<a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">JupyterLab的内置安全模型</a>之外，您的应用程序与Experience Platform之间的每次交互（包括平台服务到服务通信）都会通过<a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System](IMS)</a>进行加密和验证。 |
| **开发库** | 在[!DNL Experience Platform]中，[!DNL JupyterLab]为[!DNL Python]、R和PySpark提供预安装的库。 有关所支持库的完整列表，请参见[附录](#supported-libraries)。 |
| **库控制器** | 当您需要预安装的库时，可以为Python和R安装额外的库，并临时存储在隔离容器中，以保持[!DNL Platform]的完整性并保证数据的安全。 有关详细信息，请参阅[kernel](#kernels)部分。 |

>[!NOTE]
>
>其他库仅可用于安装它们的会话。 启动新会话时，必须重新安装所需的任何其他库。

## 与其他[!DNL Platform]服务{#service-integration}集成

标准化和互操作性是[!DNL Experience Platform]背后的关键概念。 将[!DNL Platform]上的[!DNL JupyterLab]集成为嵌入式IDE后，它可以与其他[!DNL Platform]服务交互，从而使您能够充分利用[!DNL Platform]的潜力。 [!DNL JupyterLab]中提供以下[!DNL Platform]服务：

* **[!DNL Catalog Service]：使** 用读写功能访问和浏览数据集。
* **[!DNL Query Service]:** 使用SQL访问和浏览数据集，在处理大量数据时提供较低的数据访问开销。
* **[!DNL Sensei ML Framework]：具** 有数据培训和评分功能的模型开发，以及只需单击一下即可创建菜谱。
* **[!DNL Experience Data Model (XDM)]：标** 准化和互操作性是Adobe Experience Platform的主要概念。[体验数据模型(XDM)](https://www.adobe.com/go/xdm-home-en)(由Adobe驱动)是一种旨在标准化客户体验数据并定义客户体验管理模式的努力。

>[!NOTE]
>
>[!DNL JupyterLab]上的某些[!DNL Platform]服务集成仅限于特定内核。 有关更多详细信息，请参阅[kernel](#kernels)上的部分。

## 主要功能和常见操作

以下各节提供了有关[!DNL JupyterLab]的主要功能以及执行常见操作的说明的信息：

* [访问JupyterLab](#access-jupyterlab)
* [JupyterLab接口](#jupyterlab-interface)
* [代码单元格](#code-cells)
* [内核](#kernels)
* [内核会话](#kernel-sessions)
* [启动器](#launcher)

### 访问 [!DNL JupyterLab] {#access-jupyterlab}

在[Adobe Experience Platform](https://platform.adobe.com)中，从左侧导航列中选择&#x200B;**[!UICONTROL 笔记本]**。 允许一段时间，使[!DNL JupyterLab]完全初始化。

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] 界面 {#jupyterlab-interface}

[!DNL JupyterLab]接口由菜单栏、可折叠的左侧栏和包含文档和活动选项卡的主工作区组成。

**菜单栏**

界面顶部的菜单栏具有顶级菜单，这些菜单使用键盘快捷键显示[!DNL JupyterLab]中可用的操作：

* **文件：与** 文件和目录相关的操作
* **编辑：与** 编辑文档和其他活动相关的操作
* **视图:** 更改  [!DNL JupyterLab]
* **运行：在** 笔记本和代码控制台等不同活动中运行代码的操作
* **内核：用** 于管理内核的操作
* **选项卡：** 打开的文档和活动列表
* **设置：常** 用设置和高级设置编辑器
* **帮助：** 列表和 [!DNL JupyterLab] 内核帮助链接

**左侧栏**

左侧提要栏包含可单击的选项卡，这些选项卡提供对以下功能的访问：

* **文件浏览器：** 已保存的笔记本文档和目录的列表
* **数据浏览器：** 浏览、访问和浏览数据集和模式
* **运行内核和终端：** 具有终止能力的活动内核和终端会话列表
* **命令：** 有用命令的列表
* **单元格检** 查器：一个单元格编辑器，提供对工具和元数据的访问，这些工具和元数据可用于设置用于演示目的的笔记本
* **选项卡：** 打开的选项卡列表

选择一个选项卡以显示其功能，或在展开的选项卡上选择以折叠左侧提要栏，如下所示：

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**主要工作区**

[!DNL JupyterLab]中的主要工作区域允许您将文档和其他活动排列到可调整大小或细分的选项卡面板中。 将选项卡拖动到选项卡面板的中心以迁移选项卡。 将选项卡拖动到面板的左侧、右侧、顶部或底部，以划分面板：

![](../images/jupyterlab/user-guide/main_work_area.gif)

### [!DNL Python]/R中的GPU和内存服务器配置

在[!DNL JupyterLab]中，选择右上角的齿轮图标以打开&#x200B;*笔记本服务器配置*。 您可以通过使用滑块打开GPU并分配所需的内存量。 您可以分配的内存量取决于您的组织已调配的内存量。 选择&#x200B;**[!UICONTROL 更新配置]**&#x200B;以保存。

>[!NOTE]
>
>每个组织只为笔记本提供一个GPU。 如果GPU正在使用，您需要等待当前已保留GPU的用户释放它。 可以通过注销或将GPU保持空闲状态四小时或更长时间来执行此操作。

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### 终止并重新启动[!DNL JupyterLab]

在[!DNL JupyterLab]中，您可以终止会话以阻止使用其他资源。 开始，选择&#x200B;**电源图标** ![电源图标](../images/jupyterlab/user-guide/power_button.png)，然后从显示的快显窗口中选择&#x200B;**[!UICONTROL 关闭]**&#x200B;以终止您的会话。 笔记本会话在12小时未活动后自动终止。

要重新启动[!DNL JupyterLab]，请选择位于电源图标左侧的&#x200B;**重新启动图标** ![重新启动图标](../images/jupyterlab/user-guide/restart_button.png)，然后从显示的跨距中选择&#x200B;**[!UICONTROL 重新启动]**。

![终止jupterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### 代码单元格{#code-cells}

代码单元是笔记本的主要内容。 它们包含笔记本关联内核的语言和作为执行代码单元格结果的输出的源代码。 每个代码单元的右侧显示一个执行计数，该计数表示其执行顺序。

![](../images/jupyterlab/user-guide/code_cell.png)

常见单元格操作如下所述：

* **添加单元格：** 单击笔记本菜单中的加&#x200B;**号**(+)可添加空单元格。新单元格放置在当前正在与之交互的单元格下方，或者如果没有特定单元格处于焦点，则放置在笔记本末尾。

* **移动单元格：** 将光标放在要移动的单元格的右侧，然后单击并将单元格拖动到新位置。此外，将单元从一个笔记本移动到另一个笔记本，复制单元及其内容。

* **执行单元格：** 单击要执行的单元格的正文，然后单击笔记本 **** 菜单中&#x200B;**的播放图**&#x200B;标(▶)。内核处理执行时，单元格的执行计数器中会显示星号(**\***)，在完成后，将替换为整数。

* **删除单元格：** 单击要删除的单元格的正文，然后单击剪 **** 刀图标。

### 内核{#kernels}

笔记本电脑内核是处理笔记本电脑单元的语言特定计算引擎。 除了[!DNL Python]之外，[!DNL JupyterLab]还提供R、PySpark和[!DNL Spark](Scala)中的其他语言支持。 打开笔记本文档时，将启动关联的内核。 当执行笔记本单元时，内核执行计算并产生可能消耗大量CPU和内存资源的结果。 请注意，在内核关闭之前，不会释放已分配的内存。

某些特性和功能仅限于下表所述的特定内核：

| 内核 | 库安装支持 | [!DNL Platform] 集成 |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **斯卡拉** | 否 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### 内核会话{#kernel-sessions}

[!DNL JupyterLab]上的每个活动笔记本或活动都使用内核会话。 从左侧边栏中展开&#x200B;**运行终端和内核**&#x200B;选项卡可找到所有活动会话。 通过观察笔记本界面的右上角，可以识别笔记本的内核类型和状态。 在下图中，笔记本的关联内核为&#x200B;**[!DNL Python]3**，其当前状态由右侧的灰色圆表示。 空心圆表示空闲内核，实心圆表示繁忙内核。

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

如果内核长时间处于关闭或非活动状态，则&#x200B;**无内核！** 显示实心圆。通过单击内核状态并选择相应的内核类型来激活内核，如下所示：

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### 启动器{#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

自定义&#x200B;*Launcher*&#x200B;为您提供了有用的笔记本模板，用于支持这些模板的内核，以帮助您启动任务，包括：

| 模板 | 描述 |
| --- | --- |
| 空白 | 一个空的笔记本文件。 |
| 入门 | 预填的笔记本，演示使用样本数据进行数据探索。 |
| 零售 | 预填的笔记本，使用示例数据显示[零售销售方法](https://adobe.ly/2wOgO3L)。 |
| 菜谱生成器 | 用于在[!DNL JupyterLab]中创建菜谱的笔记本模板。 它预填了演示和描述菜谱创建过程的代码和评注。 有关详细的演练，请参阅[笔记本到菜谱教程](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en)。 |
| [!DNL Query Service] | 预填充的笔记本，用于演示在[!DNL JupyterLab]中直接使用[!DNL Query Service]的情况，并提供了可大规模分析数据的示例工作流。 |
| XDM事件 | 一个预先填写的笔记本，它展示了对后值体验事件数据的数据探索，重点介绍数据结构中的常见功能。 |
| XDM查询 | 预装的笔记本，可演示有关体验事件数据的业务查询示例。 |
| 聚合 | 预填的笔记本，演示将大量数据聚合为较小、可管理的块的示例工作流。 |
| 聚类 | 预填的笔记本电脑，用聚类算法演示端到端机器学习建模过程。 |

某些笔记本模板仅限于某些内核。 下表将映射每个内核的模板可用性：

<table>
    <tr>
        <td></td>
        <th><strong>空白</strong></th>
        <th><strong>入门</strong></th>
        <th><strong>零售</strong></th>
        <th><strong>菜谱生成器</strong></th>
        <th><strong>[!DNL查询服务]</strong></th>
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

要打开新的&#x200B;*Launcher*，请单击&#x200B;**“文件”>“新建Launcher**”。 或者，从左侧边栏展开&#x200B;**文件浏览器**，然后单击加号(**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## 后续步骤

要进一步了解每个受支持的笔记本以及如何使用它们，请访问[Jupyterlab笔记本数据访问](./access-notebook-data.md)开发人员指南。 本指南重点介绍如何使用JupyterLab笔记本访问数据，包括读取、写入和查询数据。 数据访问指南还包含关于每个受支持的笔记本电脑可以读取的最大数据量的信息。

## 支持的库{#supported-libraries}

要列表Python、R和PySpark中支持的包，请在新单元格中复制并粘贴`!pip list --format=columns`，然后运行该单元格。 按字母顺序填充受支持包的列表。

![示例](../images/jupyterlab/user-guide/libraries.PNG)