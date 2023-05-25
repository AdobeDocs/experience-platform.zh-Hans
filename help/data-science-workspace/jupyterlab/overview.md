---
keywords: Experience Platform；JupyterLab；笔记本；Data Science Workspace；热门主题；jupyterlab
solution: Experience Platform
title: JupyterLab UI概述
description: JupyterLab是Project Jupyter的基于Web的用户界面，并且已紧密集成到Adobe Experience Platform中。 它为数据科学家提供了交互式开发环境，以便使用Jupyter Notebooks、代码和数据。 本文档概述了JupyterLab及其功能，并提供了执行常见操作的说明。
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 3%

---

# [!DNL JupyterLab] UI概述

[!DNL JupyterLab] 是基于Web的用户界面，用于 [Jupyter项目](https://jupyter.org/) 并紧密集成到Adobe Experience Platform中。 它为数据科学家提供了交互式开发环境，以便使用Jupyter Notebooks、代码和数据。

本文档提供了以下内容的概述 [!DNL JupyterLab] 及其功能以及执行常见操作的说明。

## [!DNL JupyterLab] 日期 [!DNL Experience Platform]

Experience Platform的JupyterLab集成伴随着体系结构变化、设计注意事项、自定义的笔记本扩展、预安装的库和Adobe主题界面。

下表概述了JupyterLab on Platform的一些独特功能：

| 功能 | 描述 |
| --- | --- |
| **内核** | 内核提供笔记本和其他 [!DNL JupyterLab] 前端能够以不同的编程语言执行和检查代码。 [!DNL Experience Platform] 提供了额外的内核来支持中的开发 [!DNL Python]、 R 、 PySpark和 [!DNL Spark]. 请参阅 [内核](#kernels) 部分以了解更多详细信息。 |
| **数据访问** | 直接从访问现有数据集 [!DNL JupyterLab] 完全支持读写功能。 |
| **[!DNL Platform]服务集成** | 内置的集成允许您利用其他 [!DNL Platform] 内直接提供服务 [!DNL JupyterLab]. 支持的集成的完整列表在以下位置提供： [与其他Platform服务集成](#service-integration). |
| **身份验证** | 除此之外 <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">JupyterLab的内置安全模型</a>，您的应用程序和Experience Platform之间的每次交互（包括Platform服务到服务通信）都经过加密和身份验证，具体方式为 <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **开发库** | In [!DNL Experience Platform]， [!DNL JupyterLab] 提供预安装的库用于 [!DNL Python]、 R和PySpark。 请参阅 [附录](#supported-libraries) 以获取支持的库的完整列表。 |
| **库控制器** | 当预安装的库无法满足您的需求时，可以为Python和R安装其他库，并临时存储在独立的容器中，以保持 [!DNL Platform] 并确保数据安全。 请参阅 [内核](#kernels) 部分以了解更多详细信息。 |

>[!NOTE]
>
>其他库仅适用于安装这些库的会话。 在启动新会话时，必须重新安装所需的任何其他库。

## 与其他集成 [!DNL Platform] 服务 {#service-integration}

标准化和互操作性是背后的关键概念 [!DNL Experience Platform]. 集成 [!DNL JupyterLab] 日期 [!DNL Platform] 作为嵌入式IDE，它允许与其他对象交互 [!DNL Platform] 服务，让您能够利用 [!DNL Platform] 充分发挥它的潜能。 以下各项 [!DNL Platform] 在以下位置提供了服务： [!DNL JupyterLab]：

* **[!DNL Catalog Service]：** 使用读取和写入功能访问和浏览数据集。
* **[!DNL Query Service]：** 使用SQL访问和浏览数据集，在处理大量数据时提供较低的数据访问开销。
* **[!DNL Sensei ML Framework]：** 能够训练数据和评分数据的模型开发，以及只需单击一下即可创建方法。
* **[!DNL Experience Data Model (XDM)]：** 标准化和互操作性是Adobe Experience Platform背后的关键概念。 [体验数据模型(XDM)](https://www.adobe.com/go/xdm-home-en)(由Adobe推动)致力于标准化客户体验数据并定义客户体验管理的模式。

>[!NOTE]
>
>部分 [!DNL Platform] 上的服务集成 [!DNL JupyterLab] 仅限特定内核。 请参阅以下部分： [内核](#kernels) 了解更多详细信息。

## 主要功能和常见操作

有关的主要功能的信息 [!DNL JupyterLab] 以下各节提供了有关执行常见操作的说明：

* [访问JupyterLab](#access-jupyterlab)
* [JupyterLab接口](#jupyterlab-interface)
* [编码单元格](#code-cells)
* [内核](#kernels)
* [内核会话](#kernel-sessions)
* [启动器](#launcher)

### 访问 [!DNL JupyterLab] {#access-jupyterlab}

In [Adobe Experience Platform](https://platform.adobe.com)，选择 **[!UICONTROL Notebooks]** （从左侧导航列中）。 留出一些时间 [!DNL JupyterLab] 以完全初始化。

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] 界面 {#jupyterlab-interface}

此 [!DNL JupyterLab] 界面由一个菜单栏、一个可折叠的左侧边栏和一个包含文档和活动选项卡的主工作区组成。

**菜单栏**

界面顶部的菜单栏有顶级菜单，其中显示可用的操作 [!DNL JupyterLab] 使用键盘快捷键：

* **文件：** 与文件和目录相关的操作
* **编辑：** 与编辑文档和其他活动相关的操作
* **查看：** 更改外观的操作 [!DNL JupyterLab]
* **运行：** 用于在不同的活动（如笔记本和代码控制台）中运行代码的操作
* **内核：** 用于管理内核的操作
* **选项卡：** 未结文档和活动的列表
* **设置：** 通用设置和高级设置编辑器
* **帮助：** 列表 [!DNL JupyterLab] 和内核帮助链接

**左侧边栏**

左侧边栏包含可单击的选项卡，通过这些选项卡可访问以下功能：

* **文件浏览器：** 已保存的笔记本文档和目录的列表
* **数据资源管理器：** 浏览、访问和浏览数据集和架构
* **运行内核和终端：** 能够终止的活动内核和终端会话的列表
* **命令：** 有用的命令列表
* **单元格检查器：** 单元格编辑器，提供对工具和元数据的访问，用于设置笔记本以进行演示
* **选项卡：** 打开的选项卡列表

选择选项卡以显示其功能，或在展开的选项卡上选择以折叠左侧边栏，如下所示：

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**主要工作区域**

中的主要工作区域 [!DNL JupyterLab] 使您可以将文档和其他活动排列到选项卡面板中，这些面板可以调整大小或进行细分。 将选项卡拖动到选项卡面板的中心以迁移选项卡。 通过将选项卡拖动到面板的左侧、右侧、顶部或底部来划分面板：

![](../images/jupyterlab/user-guide/main_work_area.gif)

### 中的GPU和内存服务器配置 [!DNL Python]/R

In [!DNL JupyterLab] 选择右上角的齿轮图标以打开 *笔记本服务器配置*. 您可以通过滑块打开GPU并分配所需的内存量。 可分配的内存量取决于您的组织已配置的内存量。 选择 **[!UICONTROL 更新配置]** 以保存。

>[!NOTE]
>
>每个组织只能为笔记本配置一个GPU。 如果GPU正在使用中，则需要等待当前已保留GPU的用户将其释放。 可以通过注销或让GPU处于空闲状态四个小时或更长时间来完成此操作。

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### 终止和重新启动 [!DNL JupyterLab]

In [!DNL JupyterLab]，您可以终止会话以防止其他资源被占用。 首先，选择 **电源图标** ![电源图标](../images/jupyterlab/user-guide/power_button.png)，然后选择 **[!UICONTROL 关闭]** 从显示终止会话的弹出窗口。 笔记本会话在12小时不活动后自动终止。

重新启动 [!DNL JupyterLab]，选择 **重新启动图标** ![重新启动图标](../images/jupyterlab/user-guide/restart_button.png) 直接位于电源图标左侧，然后选择 **[!UICONTROL 重新启动]** 从显示的弹出窗口中。

![终止jupyterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### 编码单元格 {#code-cells}

代码单元格是笔记本的主要内容。 它们包含以笔记本相关内核的语言编写的源代码，以及执行代码单元后得到的输出。 每个代码单元格的右侧会显示执行计数，表示其执行顺序。

![](../images/jupyterlab/user-guide/code_cell.png)

下面介绍了常见的单元格操作：

* **添加单元格：** 单击加号(**+**)，以添加空单元格。 新单元格放置在当前正在交互的单元格下方，如果没有特定单元格处于焦点位置，则位于笔记本的末尾。

* **移动单元格：** 将光标放在要移动的单元格的右侧，然后单击并将单元格拖动到新位置。 此外，将单元格从一个笔记本移动到另一个笔记本会复制单元格及其内容。

* **执行单元格：** 单击要执行的单元格的正文，然后单击 **play** 图标(**▶**)。 星号(**\***)在内核处理执行时显示在单元格的执行计数器中，并在完成后替换为整数。

* **删除单元格：** 单击要删除的单元格的正文，然后单击 **剪刀** 图标。

### 内核 {#kernels}

笔记本内核是用于处理笔记本单元格的语言特定计算引擎。 除此之外 [!DNL Python]， [!DNL JupyterLab] 在R、PySpark和 [!DNL Spark] (Scala)。 打开笔记本文档时，将启动关联的内核。 当执行笔记本单元时，内核执行计算并产生可能消耗大量CPU和内存资源的结果。 请注意，在关闭内核之前，不会释放分配的内存。

某些特性和功能仅限于下表所述的特定内核：

| 内核 | 库安装支持 | [!DNL Platform] 集成 |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | 否 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### 内核会话 {#kernel-sessions}

上的每个活动笔记本或活动 [!DNL JupyterLab] 利用内核会话。 通过展开 **运行终端和核心** tab键。 通过观察笔记本界面的右上角，可以识别笔记本内核的类型和状态。 在下图中，笔记本的相关内核为 **[!DNL Python]3** 它的当前状态用右边的灰色圆圈表示。 空心圆表示空闲核，实心圆表示繁忙核。

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

如果内核关闭或长时间不活动，则 **无内核！** 显示带实心的圆。 单击内核状态并选择适当的内核类型以激活内核，如下所示：

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### 启动器 {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

自定义的 *启动器* 为支持的内核提供有用的笔记本模板，以帮助您开始任务，包括：

| 模板 | 描述 |
| --- | --- |
| 空白 | 空的笔记本文件。 |
| 起始者 | 一个预填充的笔记本，演示使用示例数据探索数据。 |
| 零售业 | 预填充的笔记本，其特点是 [零售方法](../pre-built-recipes/retail-sales.md) 使用示例数据。 |
| 方法生成器 | 用于在中创建方法的笔记本模板 [!DNL JupyterLab]. 它预先填充了代码和注释，用于演示和描述方法创建过程。 请参阅 [笔记本到方法教程](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) 详细介绍。 |
| [!DNL Query Service] | 预填充笔记本演示使用 [!DNL Query Service] 直接位于 [!DNL JupyterLab] 提供了大规模分析数据的示例工作流。 |
| XDM事件 | 一个预填充的笔记本，演示对后值体验事件数据的数据探索，重点介绍数据结构中的共有功能。 |
| XDM查询 | 一个预填充的笔记本，演示有关体验事件数据的示例业务查询。 |
| 聚合 | 一个预填充的笔记本，演示将大量数据聚合到较小、可管理的块中的示例工作流。 |
| 聚类 | 一个预填充的笔记本，演示使用聚类算法的端到端机器学习建模过程。 |

某些笔记本模板仅限于某些内核。 下表映射了每个内核的模板可用性：

<table>
    <tr>
        <td></td>
        <th><strong>空白</strong></th>
        <th><strong>起始者</strong></th>
        <th><strong>零售业</strong></th>
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
        <th  ><strong>PySpark 3 ([!DNL Spark] 2.4)</strong></th>
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
        <th ><strong>Scala</strong></th>
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

打开新的 *启动器*，单击 **文件>新建启动器**. 或者，展开 **文件浏览器** 单击左侧的加号(**+**)：

![](../images/jupyterlab/user-guide/new_launcher.gif)

## 后续步骤

要了解有关每个受支持的笔记本及其使用方式的更多信息，请访问 [Jupyterlab notebooks数据访问](./access-notebook-data.md) 开发人员指南。 本指南重点介绍如何使用JupyterLab笔记本访问您的数据，包括读取、写入和查询数据。 数据访问指南还包含有关每个受支持的笔记本可读取的最大数据量的信息。

## 支持的库 {#supported-libraries}

有关Python、R和PySpark中支持的包列表，请复制并粘贴 `!conda list` 然后，在新单元格中运行单元格。 按字母顺序填充的支持资源包列表。

![示例](../images/jupyterlab/user-guide/libraries.PNG)

此外，还使用了以下依赖项，但未列出：
* CUDA 11.2
* CUDNN 8.1

