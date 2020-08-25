---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;jupyterlab
solution: Experience Platform
title: JupyterLab用户指南
topic: Overview
description: JupyterLab是Project Jupyter的基于Web的用户界面，与Adobe Experience Platform紧密集成。 它为数据科学家提供一个交互式开发环境，以便与Jupyter笔记本、代码和数据一起使用。
translation-type: tm+mt
source-git-commit: 38cb8eeae3ac0a1852c59e433d1cacae82b1c6c0
workflow-type: tm+mt
source-wordcount: '3684'
ht-degree: 11%

---


# [!DNL JupyterLab] 用户指南

[!DNL JupyterLab] 是Project Jupyter的基于Web的用 [户界面](https://jupyter.org/) ，紧密集成到Adobe Experience Platform。 它为数据科学家提供一个交互式开发环境，以便与Jupyter笔记本、代码和数据一起使用。

本文档概述其 [!DNL JupyterLab] 功能以及执行常见操作的说明。

## [!DNL JupyterLab] on [!DNL Experience Platform]

Experience Platform的JupyterLab集成包含架构更改、设计注意事项、自定义笔记本扩展、预安装库和Adobe主题界面。

以下列表概述了JupyterLab在平台上独有的一些功能：

| 功能 | 描述 |
| --- | --- |
| **内核** | 内核提供笔记本和 [!DNL JupyterLab] 其他前端以不同编程语言执行和检查代码的能力。 [!DNL Experience Platform] 提供额外的内核， [!DNL Python]支持在、R、PySpark和中进行开发 [!DNL Spark]。 有关更多 [详细信息](#kernels) ，请参阅内核部分。 |
| **数据访问** | 完全支持读写功能， [!DNL JupyterLab] 直接从内部访问现有数据集。 |
| **[!DNL Platform]服务集成** | 内置集成功能允许您直接从内 [!DNL Platform] 部利用其他服务 [!DNL JupyterLab]。 与其他平台服务集成部分提供支持的集 [成的完整列表](#service-integration)。 |
| **身份验证** | 除了JupyterLab <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">的内置安全模型</a>，您的应用程序与Experience Platform之间的每次交互（包括平台服务到服务通信）都经过加密，并通过 <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)进行验证</a>。 |
| **开发库** | 在 [!DNL Experience Platform]中 [!DNL JupyterLab] ，提供预装的 [!DNL Python]PySpark、R和PySpark库。 有关受 [支持库](#supported-libraries) 的完整列表，请参阅附录。 |
| **库控制器** | 当您需要预装的库时，可以为Python和R安装额外的库，并临时存储在隔离的容器中，以保持数据的完整性 [!DNL Platform] 和安全性。 有关更多 [详细信息](#kernels) ，请参阅内核部分。 |

>[!NOTE]
>
>其他库仅可用于安装它们的会话。 启动新会话时，必须重新安装所需的任何其他库。

## 与其他服务集 [!DNL Platform] 成 {#service-integration}

标准化和互操作性是背后的关键概念 [!DNL Experience Platform]。 集成到 [!DNL JupyterLab] 作为 [!DNL Platform] 嵌入式IDE，可以与其他服务交互， [!DNL Platform] 使您能够充分利用 [!DNL Platform] 其潜能。 以下服 [!DNL Platform] 务可在以下网站 [!DNL JupyterLab]提供：

* **[!DNL Catalog Service]:** 使用读写功能访问和浏览数据集。
* **[!DNL Query Service]:** 使用SQL访问和浏览数据集，在处理大量数据时提供更低的数据访问开销。
* **[!DNL Sensei ML Framework]:** 模型开发，能够对数据进行培训和评分，并且只需单击一下即可创建菜谱。
* **[!DNL Experience Data Model (XDM)]:** 标准化和互操作性是Adobe Experience Platform背后的关键概念。 [Adobe驱动的体验数据模型](https://www.adobe.com/go/xdm-home-en)(XDM)旨在实现客户体验数据标准化并定义客户体验管理模式。

>[!NOTE]
>
>上的 [!DNL Platform] 某些服务集 [!DNL JupyterLab] 成仅限于特定内核。 有关详细信息，请 [参阅](#kernels) “内核”一节。

## 主要功能和常见操作

以下各节提供了 [!DNL JupyterLab] 有关执行常见操作的主要功能和说明的信息：

* [访问JupyterLab](#access-jupyterlab)
* [JupyterLab接口](#jupyterlab-interface)
* [代码单元格](#code-cells)
* [内核](#kernels)
* [内核会话](#kernel-sessions)
* [PySpark/Spark执行资源](#execution-resource)
* [启动器](#launcher)

### 访问 [!DNL JupyterLab] {#access-jupyterlab}

在 [Adobe Experience Platform](https://platform.adobe.com)，从左 **侧导航列** 中选择“笔记本”。 允许一些时间 [!DNL JupyterLab] 进行完全初始化。

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] 界面 {#jupyterlab-interface}

界 [!DNL JupyterLab] 面由菜单栏、可折叠的左侧提要栏和包含文档和活动选项卡的主工作区组成。

**菜单栏**

界面顶部的菜单栏有顶级菜单，这些菜单显示使用键盘快捷键 [!DNL JupyterLab] 可执行的操作：

* **文件：** 与文件和目录相关的操作
* **编辑：** 与编辑文档和其他活动相关的操作
* **视图:** 改变外观的动作 [!DNL JupyterLab]
* **运行：** 在不同活动（如笔记本电脑和代码控制台）中运行代码的操作
* **内核：** 用于管理内核的操作
* **选项卡：** 一列表开放式文档和活动
* **设置：** 常用设置和高级设置编辑器
* **帮助：** 列表和内 [!DNL JupyterLab] 核帮助链接

**左侧提要栏**

左侧提要栏包含可单击的选项卡，这些选项卡提供对以下功能的访问：

* **文件浏览器：** 保存的笔记本文档和目录的列表
* **数据浏览器：** 浏览、访问和浏览数据集和模式
* **运行内核和终端：** 具有终止能力的活动内核和终端会话的列表
* **命令：** 有用命令的列表
* **单元格检查器：** 提供对工具和元数据的访问的单元格编辑器，这些工具和元数据可用于为演示目的设置笔记本
* **选项卡：** 一列表打开的选项卡

单击某个选项卡以显示其功能，或单击展开的选项卡折叠左侧提要栏，如下所示：

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**主要工作区**

中的主要工作区 [!DNL JupyterLab] 域允许您将文档和其他活动排列到选项卡的面板中，这些选项卡可以调整大小或细分。 将选项卡拖动到选项卡面板的中心，以迁移选项卡。 将选项卡拖至面板的左侧、右侧、顶部或底部，以划分面板：

![](../images/jupyterlab/user-guide/main_work_area.gif)

### 代码单元格 {#code-cells}

代码单元是笔记本的主要内容。 它们包含笔记本关联内核的语言和作为执行代码单元格结果的输出中的源代码。 每个代码单元的右侧显示一个执行计数，它表示其执行顺序。

![](../images/jupyterlab/user-guide/code_cell.png)

常见单元格操作如下所述：

* **添加单元格：** 单击笔记本菜单&#x200B;**中的加**&#x200B;号(+)以添加空单元格。 新单元格被放置在当前正在与之交互的单元格下，或者如果没有特定单元格处于焦点，则放置在笔记本的末尾。

* **移动单元格：** 将光标放在要移动的单元格的右侧，然后单击并将单元格拖动到新位置。 此外，将一个单元从一个笔记本移动到另一个单元将复制该单元及其内容。

* **执行单元格：** 单击要执行的单元格的正文，然后单击 **笔记本菜** 单中&#x200B;****&#x200B;的播放图标()。 当内核处&#x200B;**理执行时**，单元格的执行计数器中会显示星号(\*)，并在完成时替换为整数。

* **删除单元格：** 单击要删除的单元格的正文，然后单击剪 **刀** 图标。

### 内核 {#kernels}

笔记本电脑内核是处理笔记本电脑单元的语言专用计算引擎。 此外，还 [!DNL Python]在 [!DNL JupyterLab] R、PySpark和(Scala)中提供 [!DNL Spark] 其他语言支持。 打开笔记本文档时，将启动关联的内核。 当执行笔记本单元时，内核执行计算并产生可能消耗大量CPU和内存资源的结果。 请注意，在内核关闭之前，不会释放已分配的内存。

某些特性和功能仅限于下表所述的特定内核：

| 内核 | 库安装支持 | [!DNL Platform] 集成 |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | 是 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **斯卡拉** | 否 | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### 内核会话 {#kernel-sessions}

每个活动笔记本或活动 [!DNL JupyterLab] 都使用内核会话。 通过从左侧提要栏扩展“运行终 **端和内核”选项卡** ，可以找到所有活动会话。 通过观察笔记本界面的右上角，可以识别笔记本的内核类型和状态。 在下图中，笔记本的关联内核为 **[!DNL Python]3** ，其当前状态由右侧的灰色圆圈表示。 空心圆表示空闲内核，实心圆表示忙碌内核。

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

如果内核长时间处于关闭或非活动状态，则无 **内核！** 显示实心圆。 通过单击内核状态并选择相应的内核类型来激活内核，如下所示：

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### 启动器 {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

自定义的 *Launcher* ，为您提供实用的笔记本模板，以支持其内核，帮助您启动任务，包括：

| 模板 | 描述 |
| --- | --- |
| 空白 | 一个空的笔记本文件。 |
| 入门 | 一种预填的笔记本，用样本数据演示数据探索。 |
| 零售销售 | 预填的笔记本，其中包含使 <a href="https://adobe.ly/2wOgO3L" target="_blank">用示例数据的“零售</a> 销售菜谱”。 |
| Recipe Builder | 用于在中创建菜谱的笔记本模 [!DNL JupyterLab]板。 它预填了演示和描述菜谱创建过程的代码和评注。 有关详细的 <a href="https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en" target="_blank">演练，请参阅笔记本</a> ，参阅菜谱教程。 |
| [!DNL Query Service] | 一种预填充的笔记本，其演示直接在 [!DNL Query Service] 提供的 [!DNL JupyterLab] 样本工作流中使用，该样本可大规模分析数据。 |
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

要打开新的启动 *器*，请单 **击“文件”>“新建启动器**”。 或者，从左侧 **提要栏** 展开“文件”浏览器并单击加号&#x200B;**(+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

### /R中的GPU和内存服 [!DNL Python]务器配置

在 [!DNL JupyterLab] 中，选择右上角的齿轮图标以打开笔记本 *服务器配置*。 您可以打开GPU并使用滑块分配所需的内存量。 您可以分配的内存量取决于您的组织已配置的内存量。 选择 **[!UICONTROL 要保存]** 的更新配置。

>[!NOTE]
>每个组织只为笔记本提供一个GPU。 如果GPU正在使用，您需要等待当前已保留GPU的用户释放它。 这可以通过注销或将GPU置于空闲状态四小时或更长时间来完成。

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

## 使用笔 [!DNL Platform] 记本电脑访问数据

每个支持的内核都提供内置功能，允许您从笔记本 [!DNL Platform] 中的数据集读取数据。 但是，对分页数据的支持仅限于 [!DNL Python] 和R笔记本。

### 笔记本数据限制

以下信息定义可读取的最大数据量、已使用的数据类型以及读取数据所需的估计时间范围。 对 [!DNL Python] 于基准测试和R，使用配置为40GB RAM的笔记本电脑服务器。 对于PySpark和Scala，以下基准测试使用的数据库群集配置为64GB RAM、8个核心、2 DBU（最多4个工作程序）。

使用的ExperienceEvent模式数据在大小上各不相同，从1000(1K)行开始，范围最多可达10亿(1B)行。 请注意，对于PySpark [!DNL Spark] 和指标，XDM数据使用10天的日期范围。

临时模式数据已使用“创建表为选 [!DNL Query Service] 择”(CTAS)进行预处理。 此数据也从1000行(1K)开始，范围最多为10亿行(1B)。

#### [!DNL Python] 笔记本数据限制

**XDM体验事件模式:** 在22分钟内，您最多应能读取200万行（磁盘上约6.1 GB数据）的XDM数据。 添加其他行可能会导致错误。

| 行数 | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| 磁盘大小(MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK（秒） | 20.3 | 86.8 | 63 | 659 | 1315 |

**临时模式:** 在14分钟内，您最多应能读取500万行非XDM（临时）数据（磁盘上约5.6 GB数据）。 添加其他行可能会导致错误。

| 行数 | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| 磁盘大小(MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK（秒） | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

#### R笔记本数据限制

**XDM体验事件模式:** 在13分钟内，您最多可以读取100万行XDM数据（磁盘上的3GB数据）。

| 行数 | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| 磁盘大小(MB) | 18.73 | 187.5 | 308 | 3000 |
| R内核（秒） | 14.03 | 69.6 | 86.8 | 775 |

**临时模式:** 在大约10分钟内，您应该能够读取最多300万行临时数据（磁盘上有293MB数据）。

| 行数 | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| 磁盘大小(MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK（秒） | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

#### PySpark(内[!DNL Python] 核)笔记本数据限制：

**XDM体验事件模式:** 在交互模式下，您应能在约20分钟内读取最多500万行（磁盘上约13.42GB数据）的XDM数据。 交互模式仅支持多达500万行。 如果您希望读取较大的数据集，建议您切换到“批处理”模式。 在“批处理”模式下，您应该能够在约14小时内读取最多5亿行XDM数据（磁盘上约1.31TB数据）。

| 行数 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁盘大小 | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| SDK（交互模式） | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK（批处理模式） | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**临时模式:** 在交互模式下，您应能在不到3分钟内读取最多10亿行（磁盘上的数据约为1.05TB）的非XDM数据。 在“批处理”模式下，您应能在约18分钟内读取最多10亿行非XDM数据（磁盘上的数据约为1.05TB）。

| 行数 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| 磁盘大小 | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| SDK交互模式（以秒为单位） | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | 22s | 28.4s | 40s | 97.4s | 154.5s |
| SDK批处理模式（秒） | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

#### [!DNL Spark] （Scala内核）笔记本数据限制：

**XDM体验事件模式:** 在交互模式下，您应该能够在大约18分钟内读取最多500万行（磁盘上的13.42GB数据）的XDM数据。 交互模式仅支持多达500万行。 如果您希望读取较大的数据集，建议您切换到“批处理”模式。 在“批处理”模式下，您应该能够在约14小时内读取最多5亿行XDM数据（磁盘上约1.31TB数据）。

| 行数 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁盘大小 | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| SDK交互模式（以秒为单位） | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| SDK批处理模式（秒） | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**临时模式:** 在交互模式下，您应能在不到3分钟内读取最多10亿行（磁盘上的数据约为1.05TB）的非XDM数据。 在“批处理”模式下，您应能在约16分钟内读取最多10亿行非XDM数据（磁盘上的数据约为1.05TB）。

| 行数 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| 磁盘大小 | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| SDK交互模式（以秒为单位） | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | 29.2s | 29.7s | 36.9s | 83.5s | 139s |
| SDK批处理模式（秒） | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

### 在/R中读取数 [!DNL Python]据集

[!DNL Python] 而R型笔记本电脑允许您在访问数据集时对数据进行分页。 读取有分页和无分页数据的示例代码如下所示。

[//]: # (In the following samples, the first step is currently required but once the SDK is complete, users are no longer required to explicitly define client_context)

#### 在/R中读取数 [!DNL Python]据集，无分页

执行以下代码将读取整个数据集。 如果执行成功，则数据将保存为变量引用的Pactis数据帧 `df`。

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

* `{DATASET_ID}`:要访问的数据集的唯一标识

#### 在/R中读取 [!DNL Python]带有分页的数据集

执行以下代码将从指定的数据集中读取数据。 分页是通过分别通过函数和函数限制和偏移数据 `limit()` 来实现 `offset()` 的。 限制数据指要读取的数据点的最大数，而偏移指在读取数据之前要跳过的数据点的数量。 如果读取操作成功执行，则数据将保存为变量引用的Pactis数据帧 `df`。

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$limit(100L)$offset(10L)$read() 
```

* `{DATASET_ID}`:要访问的数据集的唯一标识

### 从PySpark//Scala中的数据集[!DNL Spark]中读取

打开活动的PySpark或Scala笔记本时，从左侧提要栏展开 **Data Explorer** 选项卡，然后单击“数 **据集** ”以视图可用数据集的列表。 右键单击要访问的数据集列表，然后单击“在笔记本 **中浏览数据”**。 将生成以下代码单元格：

#### PySpark([!DNL Spark] 2.4) {#pyspark2.4}

随着Spark 2.4的推出，提供 [`%dataset`](#magic) 了自定义幻灯。

```python
# PySpark 3 (Spark 2.4)

%dataset read --datasetId {DATASET_ID} --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

#### Scala([!DNL Spark] 2.4) {#spark2.4}

```scala
// Scala (Spark 2.4)

// initialize the session
import org.apache.spark.sql.{Dataset, SparkSession}
val spark = SparkSession.builder().master("local").getOrCreate()

val dataFrame = spark.read.format("com.adobe.platform.query")
    .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
    .option("ims-org", sys.env("IMS_ORG_ID"))
    .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
    .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
    .option("mode", "batch")
    .option("dataset-id", "{DATASET_ID}")
    .load()
dataFrame.printSchema()
dataFrame.show()
```

>[!TIP]
>在Scala中，您可 `sys.env()` 以使用从中声明和返回值 `option`。

### 在PySpark 3(2.4)笔记本中使[!DNL Spark] 用%dataset magic {#magic}

随着2.4 [!DNL Spark] 的推出， `%dataset` 自定义魔术功能将被提供用于新的PySpark 3(2.4)[!DNL Spark] 笔记本([!DNL Python] 3内核)。

**用法**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**描述**

用于从 [!DNL Data Science Workspace] 笔记本（3内核）读取或写入数据集 [!DNL Python] 的自定[!DNL Python] 义魔术命令。

* **{action}**:要对数据集执行的操作类型。 两个操作可用于“读取”或“写入”。
* **—datasetId {id}**:用于提供要读或写的数据集的id。 这是必需参数。
* **—dataFrame {df}**:熊猫数据框。 这是必需参数。
   * 当操作为“read”时，{df}是数据集读取操作结果可用的变量。
   * 当操作为“write”时，此数据帧{df}将写入数据集。
* **—mode（可选）**:允许的参数为“batch”和“interactive”。 默认情况下，该模式设置为“交互”。 在读取大量数据时，建议使用“批处理”模式。

**示例**

* **阅读示例**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
* **编写示例**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

### 查询数据使 [!DNL Query Service] 用 [!DNL Python]

[!DNL JupyterLab] on允 [!DNL Platform] 许您在笔记本中使 [!DNL Python] 用SQL通过Adobe Experience Platform <a href="https://www.adobe.com/go/query-service-home-en" target="_blank">查询服务访问数据</a>。 通过访问数 [!DNL Query Service] 据对于处理大型数据集很有用，因为它具有出色的运行时间。 请注意，使用查询 [!DNL Query Service] 数据的处理时间限制为十分钟。

在中使 [!DNL Query Service] 用 [!DNL JupyterLab]之前，请确保您对SQL语法有 <a href="https://www.adobe.com/go/query-service-sql-syntax-en" target="_blank">[!DNL Query Service] 正确的了解</a>。

使用查询 [!DNL Query Service] 数据需要您提供目标数据集的名称。 您可以使用数据资源管理器查找所需的数据集，从而生成必 **要的代码单元**。 右键单击数据集列表，然后单 **击笔记本中的查询** ，以在笔记本中生成以下两个代码单元格：


要在中利用 [!DNL Query Service] , [!DNL JupyterLab]您必须先在工作笔记本和之间创建 [!DNL Python] 连接 [!DNL Query Service]。 这可以通过执行第一生成的单元来实现。

```python
qs_connect()
```

在第二个生成的单元格中，必须在SQL查询之前定义第一行。 默认情况下，生成的单元格定义一个可选变量(`df0`)，该变量将查询结果保存为Apnotics数据帧。 <br>该 `-c QS_CONNECTION` 参数是必需的，它告诉内核执行SQL查询 [!DNL Query Service]。 有关一 [列表其](#optional-sql-flags-for-query-service) 他参数，请参见附录。

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Python变量可以在SQL查询中直接引用，方法是使用字符串格式的语法并将变量打包在大括号(`{}`)中，如下例所示：

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### 在/R中过滤ExperienceEvent [!DNL Python]数据

要访问和过滤或R笔记本 [!DNL Python] 中的ExperienceEvent数据集，您必须提供数据集(`{DATASET_ID}`)的ID以及使用逻辑运算符定义特定时间范围的过滤器规则。 定义时间范围时，将忽略任何指定的分页，并考虑整个数据集。

筛选操作符的列表说明如下：

* `eq()`: 等于
* `gt()`: 大于
* `ge()`: 大于或等于
* `lt()`: 小于
* `le()`: 小于或等于
* `And()`:逻辑AND运算符
* `Or()`:逻辑OR运算符

以下单元格将ExperienceEvent数据集筛选为2019年1月1日至2019年12月31日之间仅存的数据。

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

### 在PySpark/[!DNL Spark]

在PySpark或Scala笔记本中访问和过滤ExperienceEvent数据集时，需要您提供数据集标识(`{DATASET_ID}`)、组织的IMS标识以及定义特定时间范围的过滤器规则。 过滤时间范围是使用函数定义的， `spark.sql()`其中函数参数是SQL查询字符串。

以下单元格将ExperienceEvent数据集筛选为2019年1月1日至2019年12月31日之间仅存的数据。

#### PySpark 3([!DNL Spark] 2.4) {#pyspark3-spark2.4}

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

#### Scala([!DNL Spark] 2.4) {#scala-spark}

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

>[!TIP]
>
>
>在Scala中，您可 `sys.env()` 以使用从中声明和返回值 `option`。 这样，如果您知道变量将仅用于一次，就无需定义变量。 以下示例从上 `val userToken` 述示例中开始，并将其在行中声明 `option` 为替代内容：
>
> 
```scala
> .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
> ```

## 支持的库 {#supported-libraries}

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
| r-rsolnp | 1.16 |
| r-陈化 | 1.12 |
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

## 可选的SQL标志 [!DNL Query Service] {#optional-sql-flags-for-query-service}

此表概述了可用于的可选SQL标志 [!DNL Query Service]。

| **标志** | **描述** |
| --- | --- |
| `-h`, `--help` | 显示帮助消息并退出。 |
| `-n`, `--notify` | 切换选项以通知查询结果。 |
| `-a`, `--async` | 使用此标志可异步执行查询，并可在查询执行时释放内核。 将查询结果分配给变量时要小心，因为如果查询不完成，则可能未定义。 |
| `-d`, `--display` | 使用此标志可阻止显示结果。 |

