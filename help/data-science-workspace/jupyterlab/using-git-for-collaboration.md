---
keywords: Experience Platform;JupyterLab；笔记本；Data Science Workspace；热门主题；Git;Github
solution: Experience Platform
title: 使用Git在JupyterLab中协作
type: Tutorial
description: Git是一个分布式版本控制系统，用于在软件开发过程中跟踪源代码中的更改。 Git是在Data Science Workspace JupyterLab环境中预安装的。
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# 协作 [!DNL JupyterLab] 使用 [!DNL Git]

[!DNL Git] 是一种分布式版本控制系统，用于在软件开发过程中跟踪源代码中的更改。 Git预安装在 [!DNL Data Science Workspace JupyterLab] 环境。

## 先决条件

>[!NOTE]
>
> 您要使用的Git服务器需要可以通过Internet访问。

的 [!DNL Data Science Workspace JupyterLab] 环境是托管环境，未在公司防火墙中部署，因此您连接到的Git服务器必须可从公共internet访问。 这可以是上的公共或专用存储库 [GitHub](https://github.com/) 或 [!DNL Git] 您决定自行托管的服务器。

## 连接 [!DNL Git] 到 [!DNL Data Science Workspace JupyterLab Notebooks] 环境

首先，启动 [!DNL Adobe Experience Platform] 并导航到 [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) 环境。

在 [!DNL JupyterLab]，选择 **[!UICONTROL 文件]** 将鼠标悬停在 **[!UICONTROL 新建]**. 从显示的下拉菜单中，选择 **[!UICONTROL 终端]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

下一步，在 *终端* 使用以下命令导航到工作区： `cd my-workspace`.

![cd workspace](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> 要查看可用git命令的列表，请发出命令： `git -help` 在终端中。

接下来，使用 `git clone` 命令。 使用 `https://` URL而不是 `ssh://`.

**示例**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![克隆](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> 为了执行任何写操作(`git push` 例如，每个新会话都需要运行以下配置命令。 另请注意，任何推送命令都会提示输入用户名和密码。
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## 后续步骤

克隆完存储库后，您可以像在本地计算机上一样使用Git，以便与其他人在笔记本上协作。 有关您在中可以执行的操作的更多信息 [!DNL JupyterLab]，请参阅 [[!DNL JupyterLab user guide]](./overview.md).
