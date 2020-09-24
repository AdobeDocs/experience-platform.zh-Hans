---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;Git;Github
solution: Experience Platform
title: 在JupyterLab中使用Git进行协作
topic: tutorial
type: Tutorial
description: Git是一种分布式版本控制系统，用于跟踪软件开发过程中源代码的更改。 Git预安装在Data Science Workspace JupyterLab环境中。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---


# 协作使 [!DNL JupyterLab] 用 [!DNL Git]

[!DNL Git] 是一个分布式版本控制系统，用于跟踪软件开发过程中源代码的变化。 Git预安装在环境 [!DNL Data Science Workspace JupyterLab] 中。

## 先决条件

>[!NOTE]
>
> 您要使用的Git服务器需要通过Internet访问。

该环境 [!DNL Data Science Workspace JupyterLab] 是托管环境，未在您的企业防火墙中部署，因此您连接到的Git服务器必须可从公共Internet访问。 这可以是GitHub上的公共或 [专用存储库](https://github.com/) ，也可以是您决定 [!DNL Git] 自己托管的服务器的另一个实例。

## 连 [!DNL Git] 接到 [!DNL Data Science Workspace JupyterLab Notebooks] 环境

开始, [!DNL Adobe Experience Platform] 启动并导航 [到[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) 环境。

在中 [!DNL JupyterLab]，选择 **[!UICONTROL 文件]** ，然后悬停在 **[!UICONTROL 新建]**。 从显示的下拉菜单中，选择 **[!UICONTROL 终端]**。

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

然后，在终 *端中* ，使用以下命令导航到您的工作区： `cd my-workspace`.

![cd工作区](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> 要查看一列表可用的git命令，请发出以下命令： `git -help` 在终端中。

然后，使用命令克隆要使用的存储 `git clone` 库。 使用URL而不是 `https://` URL克隆您的项 `ssh://`目。

**示例**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![克隆](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> 要执行任何写操作(例`git push` 如)，需要对每个新会话运行以下配置命令。 另请注意，任何推送命令都会提示输入用户名和密码。
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## 后续步骤

克隆完存储库后，您可以像在本地计算机上一样使用Git，在笔记本上与他人协作。 有关您可在中执行的操作的 [!DNL JupyterLab]详细信 [息，请参阅[!DNL JupyterLab用户指南]](./overview.md)。
