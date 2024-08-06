---
keywords: Experience Platform；JupyterLab；笔记本；数据科学Workspace；热门主题；Git；Github
solution: Experience Platform
title: 使用Git在JupyterLab中进行协作
type: Tutorial
description: Git 是一个分布式版本控制系统，用于在软件开发过程中跟踪源代码中的更改。 Git预安装在数据科学Workspace JupyterLab环境中。
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# 使用[!DNL Git]在[!DNL JupyterLab]中协作

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

[!DNL Git]是一个分布式版本控制系统，用于在软件开发期间跟踪源代码中的更改。 已在[!DNL Data Science Workspace JupyterLab]环境中预安装Git。

## 先决条件

>[!NOTE]
>
> 要使用的Git服务器需要可通过Internet访问。

[!DNL Data Science Workspace JupyterLab]环境是托管环境，未部署在您的公司防火墙内，因此您连接到的Git服务器必须可以从公共Internet访问。 这可以是[GitHub](https://github.com/)上的公共或专用存储库，也可以是您决定自己托管的[!DNL Git]服务器的其他实例。

## 将[!DNL Git]连接到[!DNL Data Science Workspace JupyterLab Notebooks]环境

首先 [!DNL Adobe Experience Platform] 启动 [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) 并导航到环境。

在[!DNL JupyterLab]内，选择&#x200B;**[!UICONTROL 文件]**，然后将鼠标悬停在&#x200B;**[!UICONTROL 新建]**&#x200B;上。 从出现的下拉列表中选择&#x200B;**[!UICONTROL 终端]**。

![JupyterLab导航](../images/jupyterlab/tutorials/open-terminal.png)

接下来，在&#x200B;*终端*&#x200B;中，使用以下命令导航到工作区： `cd my-workspace`。

![cd工作区](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> 要查看可用git命令的列表，请在终端中发出命令： `git -help`。

接下来，使用`git clone`命令克隆要使用的存储库。 使用`https://` URL而不是`ssh://`克隆项目。

**示例**：

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![克隆](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> 为了执行任何写入操作（`git push` 例如），需要为每个新会话运行以下配置命令。 另请注意，任何推送命令都会提示输入用户名和密码。
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## 后续步骤

完成存储库的克隆后，您可以像在本地计算机上一样使用Git与他人协作使用笔记本。 有关在[!DNL JupyterLab]中可以执行的操作的详细信息，请参阅[[!DNL JupyterLab user guide]](./overview.md)。
