---
keywords: Experience Platform;JupyterLab；笔记本；数据科学工作区；热门主题；jupyterlab
solution: Experience Platform
title: JupyterLab UI概述
topic: Overview
description: JupyterLab是Project Jupyter的基于Web的用户界面，与Adobe Experience Platform紧密集成。 它为数据科学家提供一个交互式开发环境，以便与Jupyter笔记本，代码和数据一起使用。 本文档概述了JupyterLab及其功能以及执行常见操作的说明。
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1950'
ht-degree: 9%

---


# [!DNL JupyterLab] UI概述

[!DNL JupyterLab] 是Project Jupyter的基于web的用户 [界](https://jupyter.org/) 面，与Adobe Experience Platform紧密集成。它为数据科学家提供一个交互式开发环境，以便与Jupyter笔记本，代码和数据一起使用。

本文档概述了[!DNL JupyterLab]及其功能以及执行常见操作的说明。

## [!DNL JupyterLab] on  [!DNL Experience Platform]

Experience Platform的JupyterLab集成包含架构更改、设计注意事项、自定义笔记本扩展、预安装库和Adobe主题界面。

以下列表概述了JupyterLab在平台上独有的一些功能：

| 功能 | 描述 |
| --- | --- |
| **内核** | 内核提供笔记本和其它[!DNL JupyterLab]前端，能够执行和检查不同编程语言的代码。 [!DNL Experience Platform] 提供额外的内核， [!DNL Python]支持在、R、PySpark和中进行开发 [!DNL Spark]。有关详细信息，请参阅[kernel](#kernels)部分。 |
| **数据访问** | 完全支持读写功能，可直接从[!DNL JupyterLab]内访问现有数据集。 |
| **[!DNL Platform]服务集成** | 内置集成功能允许您直接从[!DNL JupyterLab]中利用其他[!DNL Platform]服务。 [与其他平台服务集成](#service-integration)一节中提供了受支持集成的完整列表。 |
| **身份验证** | 除了<a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">JupyterLab的内置安全模型</a>之外，您的应用程序与Experience Platform之间的每次交互（包括平台服务到服务通信）都通过<a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System](IMS)</a>进行加密和验证。 |
| **开发库** | 在[!DNL Experience Platform]中，[!DNL JupyterLab]为[!DNL Python]、R和PySpark提供预安装的库。 有关所支持库的完整列表，请参见[附录](#supported-libraries)。 |
| **库控制器** | 当您需要预装的库时，可以为Python和R安装额外的库，并临时存储在隔离容器中，以保持[!DNL Platform]的完整性并保证数据的安全。 有关详细信息，请参阅[kernel](#kernels)部分。 |

>[!NOTE]
>
>其他库仅可用于安装它们的会话。 启动新会话时，必须重新安装所需的任何其他库。

## 与其他[!DNL Platform]服务{#service-integration}集成

标准化和互操作性是[!DNL Experience Platform]的主要概念。 将[!DNL Platform]上的[!DNL JupyterLab]集成为嵌入式IDE，可以与其他[!DNL Platform]服务进行交互，从而使您能够充分利用[!DNL Platform]的潜能。 [!DNL JupyterLab]中提供以下[!DNL Platform]服务：

* **[!DNL Catalog Service]：访** 问和浏览具有读写功能的数据集。
* **[!DNL Query Service]：使** 用SQL访问和浏览数据集，在处理大量数据时提供更低的数据访问开销。
* **[!DNL Sensei ML Framework]：可** 以对数据进行培训和评分的模型开发，以及只需单击一下即可创建菜谱。
* **[!DNL Experience Data Model (XDM)]：标** 准化和互操作性是Adobe Experience Platform背后的关键概念。[Adobe驱动的体验数据模型](https://www.adobe.com/go/xdm-home-en)(XDM)旨在实现客户体验数据标准化并定义客户体验管理模式。

>[!NOTE]
>
>[!DNL JupyterLab]上的某些[!DNL Platform]服务集成仅限于特定内核。 有关更多详细信息，请参阅[kernel](#kernels)中的一节。

## 主要功能和常见操作

以下各节提供了有关[!DNL JupyterLab]的主要功能以及执行常见操作的说明：

* [访问JupyterLab](#access-jupyterlab)
* [JupyterLab接口](#jupyterlab-interface)
* [代码单元格](#code-cells)
* [内核](#kernels)
* [内核会话](#kernel-sessions)
* [启动器](#launcher)

### 访问 [!DNL JupyterLab] {#access-jupyterlab}

在[Adobe Experience Platform](https://platform.adobe.com)中，从左侧导航列中选择&#x200B;**笔记本**。 允许一些时间让[!DNL JupyterLab]完全初始化。

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] 界面 {#jupyterlab-interface}

[!DNL JupyterLab]接口由菜单栏、可折叠的左侧提要栏和包含文档和活动选项卡的主工作区组成。

**菜单栏**

界面顶部的菜单栏具有顶级菜单，这些菜单使用[!DNL JupyterLab]的键盘快捷键显示可用的操作：

* **文件：与** 文件和目录相关的操作
* **编辑：与** 编辑文档和其他活动相关的操作
* **视图:** 改变外观的动作  [!DNL JupyterLab]
* **运行：在** 笔记本和代码控制台等不同活动中运行代码的操作
* **内核：用** 于管理内核的操作
* **选项卡：** 打开的列表和活动
* **设置：常** 用设置和高级设置编辑器
* **帮助：** 列表和 [!DNL JupyterLab] 内核帮助链接

**左侧提要栏**

左侧提要栏包含可单击的选项卡，这些选项卡提供对以下功能的访问：

* **文件浏览器：** 已保存的笔记本文档和目录的列表
* **数据浏览器：** 浏览、访问和浏览数据集和模式
* **运行内核和终端：** 具有终止能力的活动内核和终端会话列表
* **命令：** 有用命令的列表
* **单元格检** 查器：一个单元格编辑器，提供对工具和元数据的访问，这些工具和元数据可用于为演示目的设置笔记本
* **选项卡：** 打开的选项卡列表

单击某个选项卡以显示其功能，或单击展开的选项卡折叠左侧提要栏，如下所示：

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**主要工作区**

[!DNL JupyterLab]中的主工作区域允许您将文档和其他活动排列到选项卡面板中，这些选项卡可以调整大小或进行细分。 将选项卡拖动到选项卡面板的中心，以迁移选项卡。 将选项卡拖至面板的左侧、右侧、顶部或底部，以划分面板：

![](../images/jupyterlab/user-guide/main_work_area.gif)

### 代码单元格{#code-cells}

代码单元是笔记本的主要内容。 它们包含笔记本关联内核的语言和作为执行代码单元格结果的输出中的源代码。 每个代码单元的右侧显示一个执行计数，它表示其执行顺序。

![](../images/jupyterlab/user-guide/code_cell.png)

常见单元格操作如下所述：

* **添加单元格：** 单击笔记本菜单&#x200B;**中的加**&#x200B;号(+)以添加空单元格。新单元格被放置在当前正在与之交互的单元格下，或者如果没有特定单元格处于焦点，则放置在笔记本的末尾。

* **移动单元格：** 将光标放在要移动的单元格的右侧，然后单击并将单元格拖动到新位置。此外，将一个单元从一个笔记本移动到另一个单元将复制该单元及其内容。

* **执行单元格：** 单击要执行的单元格的正文，然后从笔记本菜 **** 单中单&#x200B;**击播**&#x200B;放图标()。当内核处理执行时，单元格的执行计数器中显示星号(**\***)，并在完成时替换为整数。

* **删除单元格：** 单击要删除的单元格的正文，然后单击剪 **** 刀图标。

### 内核{#kernels}

笔记本电脑内核是处理笔记本电脑单元的语言专用计算引擎。 除了[!DNL Python]之外，[!DNL JupyterLab]还在R、PySpark和[!DNL Spark](Scala)中提供其他语言支持。 打开笔记本文档时，将启动关联的内核。 当执行笔记本单元时，内核执行计算并产生可能消耗大量CPU和内存资源的结果。 请注意，在内核关闭之前，不会释放已分配的内存。

某些特性和功能仅限于下表所述的特定内核：

| 内核 | 库安装支持 | [!DNL Platform] 集成 |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **斯卡拉** | 否 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### 内核会话{#kernel-sessions}

[!DNL JupyterLab]上的每个活动笔记本或活动都使用内核会话。 所有活动会话都可以通过从左侧提要栏展开&#x200B;**运行终端和内核**&#x200B;选项卡找到。 通过观察笔记本界面的右上角，可以识别笔记本的内核类型和状态。 在下图中，笔记本的关联内核为&#x200B;**[!DNL Python]3**，其当前状态由右侧的灰色圆圈表示。 空心圆表示空闲内核，实心圆表示忙碌内核。

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

如果内核长时间处于关闭或非活动状态，则&#x200B;**无内核！** 显示实心圆。通过单击内核状态并选择相应的内核类型来激活内核，如下所示：

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### 启动器{#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

自定义&#x200B;*Launcher*&#x200B;为您提供了实用的笔记本模板，这些模板用于支持的内核，可帮助您启动任务，包括：

| 模板 | 描述 |
| --- | --- |
| 空白 | 一个空的笔记本文件。 |
| 入门 | 一种预填的笔记本，用样本数据演示数据探索。 |
| 零售销售 | 一种预填充的笔记本，其特征是使用示例数据使用[零售销售菜谱](https://adobe.ly/2wOgO3L)。 |
| Recipe Builder | 用于在[!DNL JupyterLab]中创建菜谱的笔记本模板。 它预填了演示和描述菜谱创建过程的代码和评注。 有关详细的演练，请参阅[笔记本到菜谱教程](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en)。 |
| [!DNL Query Service] | 预填充的笔记本直接演示[!DNL JupyterLab]中[!DNL Query Service]的用法，它提供了可大规模分析数据的示例工作流。 |
| XDM事件 | 预填的笔记本，展示对后值体验事件数据的数据探索，侧重于数据结构中的常见功能。 |
| XDM查询 | 预填的笔记本，展示关于体验查询数据的示例业务事件。 |
| 聚合 | 预先填充的笔记本，展示将大量数据聚合为较小、可管理的块的样本工作流。 |
| 聚类 | 预填充的笔记本电脑，演示使用聚类算法的端对端机器学习建模过程。 |

某些笔记本模板仅限于某些内核。 下表将映射每个内核的模板可用性：

<table>
    <tr>
        <td></td>
        <th><strong>空白</strong></th>
        <th><strong>入门</strong></th>
        <th><strong>零售销售</strong></th>
        <th><strong>Recipe Builder</strong></th>
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

要打开新的&#x200B;*启动器*，请单击&#x200B;**文件>新建启动器**。 或者，从左侧提要栏展开&#x200B;**文件浏览器**&#x200B;并单击加号(**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

### [!DNL Python]/R中的GPU和内存服务器配置

在[!DNL JupyterLab]中，选择右上角的齿轮图标以打开&#x200B;*笔记本服务器配置*。 您可以打开GPU并使用滑块分配所需的内存量。 您可以分配的内存量取决于您的组织已配置的内存量。 选择&#x200B;**[!UICONTROL 更新配置]**&#x200B;以保存。

>[!NOTE]
>
>每个组织只为笔记本提供一个GPU。 如果GPU正在使用，您需要等待当前已保留GPU的用户释放它。 这可以通过注销或将GPU置于空闲状态四小时或更长时间来完成。

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

## 后续步骤

要进一步了解每个受支持的笔记本电脑以及如何使用它们，请访问[Jupyterlab笔记本电脑数据访问](./access-notebook-data.md)开发人员指南。 本指南重点介绍如何使用JupyterLab笔记本访问数据，包括读取、写入和查询数据。 数据访问指南还包含关于每个受支持的笔记本可以读取的最大数据量的信息。

## 支持的库{#supported-libraries}

### [!DNL Python] / R

| 库 | 版本 |
| :------ | :------ |
| 笔记本 | 6.0.0 |
| 请求 | 2.22.0 |
| 极端 | 4.0.0 |
| 叶 | 0.10.0 |
| 小部件 | 7.5.1 |
| 博凯 | 1.3.1 |
| 亨西姆 | 3.7.3 |
| 平行 | 0.5.2 |
| jq | 1.6 |
| keras | 2.2.4 |
| nltk | 3.2.5 |
| 熊猫 | 0.22.0 |
| 潘达斯 | 0.7.3 |
| 枕 | 6.0.0 |
| Scikit图像 | 0.15.0 |
| scikit-learn | 0.21.3 |
| 熏 | 1.3.0 |
| 杂乱 | 1.3.0 |
| 西伯恩 | 0.9.0 |
| statmodels | 0.10.1 |
| 弹性 | 5.1.0.17 |
| gplot | 0.11.5 |
| py-xgboost | 0.90 |
| opencv | 3.4.1 |
| 皮什帕克 | 2.4.3 |
| 火炬 | 1.0.1 |
| wxpython | 4.0.6 |
| 颜色 | 0.3.0 |
| 盖潘达 | 0.5.1 |
| 地源 | 2.1.0 |
| 形象 | 1.6.4 |
| rpy2 | 2.9.4 |
| r-essentials | 3.6 |
| r-arules | 1.6_3 |
| r-fpc | 2.2_3 |
| r-e1071 | 1.7_2 |
| r-gam | 1.16.1 |
| r-gbm | 2.1.5 |
| r-ggthemes | 4.2.0 |
| r-ggvis | 0.4.4 |
| r-igraph | 1.2.4.1 |
| r-leaps | 3.0 |
| r操作 | 1.0.1 |
| r-rocr | 1.0_7 |
| r-rmysql | 0.10.17 |
| r-rodbc | 1.3_15 |
| r-rsqlite | 2.1.2 |
| r-rstan | 2.19.2 |
| r-sqldf | 0.4_11 |
| r-surval | 2.44_1.1 |
| 动物园 | 1.8_6 |
| r-stringdist | 0.9.5.2 |
| r-quadprog | 1.5_7 |
| r-rjson | 0.2.20 |
| r-forecast | 8.7 |
| r-rsolnp | 一点一六 |
| r-陈化 | 一点一二 |
| r-mlr | 2.14.0 |
| 病毒 | 0.5.1 |
| r-corplot | 0.84 |
| r-fnn | 1.1.3 |
| r-lubridate | 1.7.4 |
| r-randomforest | 4.6_14 |
| 逆反 | 1.2.1 |
| r树 | 1.0_39 |
| 皮蒙戈 | 3.8.0 |
| 派箭 | 0.14.1 |
| boto3 | 1.9.199 |
| ipyvolume | 0.5.2 |
| fast | 0.3.2 |
| python-snappy | 0.5.4 |
| ipywebrtc | 0.5.0 |
| jupyter_client | 5.3.1 |
| wordcloud | 1.5.0 |
| graphviz | 2.40.1 |
| python-graphviz | 0.11.1 |
| azure存储 | 0.36.0 |
| [!DNL jupyterlab] | 1.0.4 |
| 熊猫_ml | 0.6.1 |
| tensorflow-gpu | 1.14.0 |
| nodejs | 12.3.0 |
| 模型 | 3.0.5 |
| ipympl | 0.3.3 |
| fonts-anacond | 1.0 |
| psycopg2 | 2.8.3 |
| 鼻子 | 1.3.7 |
| autovizwidget | 0.12.9 |
| 阿尔泰 | 3.1.0 |
| vega_datasets | 0.7.0 |
| 平磨机 | 1.0.1 |
| sql_magic | 0.0.4 |
| iso3166 | 1.0 |
| nbimporter | 0.3.1 |

### PySpark

| 库 | 版本 |
| :------ | :------ |
| 请求 | 2.18.4 |
| 亨西姆 | 2.3.0 |
| keras | 2.0.6 |
| nltk | 3.2.4 |
| 熊猫 | 0.20.1 |
| 潘达斯 | 0.7.3 |
| 枕 | 5.3.0 |
| Scikit图像 | 0.13.0 |
| scikit-learn | 0.19.0 |
| 熏 | 0.19.1 |
| 杂乱 | 1.3.3 |
| statmodels | 0.8.0 |
| 弹性 | 4.0.30.44 |
| py-xgboost | 0.60 |
| opencv | 3.1.0 |
| 派箭 | 0.8.0 |
| boto3 | 1.5.18 |
| azure-存储-blob | 1.4.0 |
| [!DNL python] | 3.6.7 |
| mkl-rt | 11.1 |