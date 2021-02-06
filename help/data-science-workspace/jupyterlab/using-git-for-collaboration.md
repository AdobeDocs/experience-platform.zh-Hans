---
keywords: Experience Platform;JupyterLab；笔记本；数据科学工作区；热门主题；Git;Github
solution: Experience Platform
title: 在JupyterLab中使用Git进行协作
topic: tutorial
type: Tutorial
description: Git是一种分布式版本控制系统，用于跟踪软件开发过程中源代码的更改。 Git预安装在Data Science Workspace JupyterLab环境中。
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---


# 使用[!DNL Git]在[!DNL JupyterLab]中协作

[!DNL Git] 是一个分布式版本控制系统，用于跟踪软件开发过程中源代码的变化。Git预安装在[!DNL Data Science Workspace JupyterLab]环境中。

## 先决条件

>[!NOTE]
>
> 您要使用的Git服务器需要通过Internet访问。

[!DNL Data Science Workspace JupyterLab]环境是托管环境，未部署在公司防火墙内，因此您连接到的Git服务器必须可从公共Internet访问。 这可以是[GitHub](https://github.com/)上的公共或专用存储库，或者您已决定自行托管的[!DNL Git]服务器的另一个实例。

## 将[!DNL Git]连接到[!DNL Data Science Workspace JupyterLab Notebooks]环境

开始，方法是启动[!DNL Adobe Experience Platform]并导航到[[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab)环境。

在[!DNL JupyterLab]中，选择&#x200B;**[!UICONTROL 文件]**，然后将指针悬停在&#x200B;**[!UICONTROL 新建]**&#x200B;上。 从出现的下拉菜单中，选择&#x200B;**[!UICONTROL 终端]**。

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

接下来，在&#x200B;*Terminal*&#x200B;中，使用以下命令导航到您的工作区：`cd my-workspace`。

![cd工作区](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> 要查看一列表可用的git命令，请发出以下命令：`git -help`。

然后，使用`git clone`命令克隆要使用的存储库。 使用`https://` URL而不是`ssh://`克隆项目。

**示例**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![克隆](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> 为了执行任何写操作（例如`git push`），需要对每个新会话运行以下配置命令。 另请注意，任何推送命令都会提示输入用户名和密码。
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## 后续步骤

克隆完存储库后，您可以像在本地计算机上一样使用Git，在笔记本上与他人协作。 有关在[!DNL JupyterLab]中可以执行的操作的详细信息，请参阅[[!DNL JupyterLab user guide]](./overview.md)。
