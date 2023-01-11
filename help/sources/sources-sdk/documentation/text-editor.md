---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK;SDK
solution: Experience Platform
title: 在本地环境中使用文本编辑器创建源文档页面
description: 本文档提供了有关如何使用本地环境为源创作文档并提交拉取请求(PR)的步骤。
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 3%

---

# 在本地环境中使用文本编辑器创建源文档页面

本文档提供了有关如何使用本地环境为源创作文档并提交拉取请求(PR)的步骤。

>[!TIP]
>
>以下来自Adobe贡献指南的文档可用于进一步支持您的文档流程： <ul><li>[安装Git和Markdown创作工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)</li><li>[在本地设置适用于文档的 Git 存储库](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)</li><li>[针对主要更改的 GitHub 参与工作流](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en)</li></ul>

## 先决条件

以下教程要求您在本地计算机上安装GitHub Desktop。 如果您没有GitHub Desktop，则可以下载应用程序 [此处](https://desktop.github.com/).

## 连接到GitHub并设置本地创作环境

设置本地创作环境的第一步是导航到 [Adobe Experience Platform GitHub存储库](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

在Platform GitHub存储库的主页上，选择 **分叉**.

![分支存储库](../assets/fork.png)

要将存储库克隆到本地计算机，请选择 **代码**. 从显示的下拉菜单中，选择 **HTTPS** 然后，选择 **使用GitHub Desktop打开**.

>[!TIP]
>
>有关更多信息，请参阅 [在本地设置适用于文档的Git存储库](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository).

![open-git-desktop](../assets/open-git-desktop.png)

接下来，让GitHub Desktop花些时间克隆 `experience-platform.en` 存储库。

![克隆](../assets/cloning.png)

克隆过程完成后，转到GitHub Desktop以创建新分支。 选择 **主控** ，然后选择 **新建分支**

![新分支](../assets/new-branch.png)

在显示的弹出面板中，为分支输入描述性名称，然后选择 **创建分支**.

![create-branch-vs](../assets/create-branch-vs.png)

接下来，选择 **发布分支**.

![publish-branch](../assets/publish-branch.png)

## 为源创作文档页面

现在，通过将存储库克隆到本地计算机并创建新分支，您可以通过 [您选择的文本编辑器](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors).

Adobe建议您使用 [Visual Studio代码](https://code.visualstudio.com/) 以及安装AdobeMarkdown Authoring扩展。 要安装该扩展，请启动Visual Studio代码，然后选择 **扩展** 选项卡。

![扩展](../assets/extension.png)

下一步，输入 `Adobe Markdown Authoring` ，然后选择 **安装** 从显示的页面中。

![安装](../assets/install.png)

在本地计算机就绪后，下载 [源文档模板](../assets/api-template.zip) 并将文件解压到 `experience-platform.en/help/sources/tutorials/api/create/...` with [`...`] 表示您选择的类别。 例如，如果要创建数据库源，请选择数据库文件夹。

最后，按照模板上所述的说明操作，并使用与源相关的相关信息编辑模板。

![edit-template](../assets/edit-template.png)

## 提交文档以供审核

要创建拉取请求(PR)并提交文档以供审核，请首先在 [!DNL Visual Studio Code] （或您选择的文本编辑器）。 接下来，使用GitHub Desktop，输入提交消息并选择 **提交到create-source-documentation**.

![commit-vs](../assets/commit-vs.png)

接下来，选择 **推送源** 将您的工作上传到远程分支。

![推送源](../assets/push-origin.png)

要创建拉取请求，请选择 **创建拉取请求**.

![create-pr-vs](../assets/create-pr-vs.png)

确保基分支和比较分支正确无误。 向PR中添加说明更新的注释，然后选择 **创建拉取请求**. 这会打开一个PR，以将您工作的工作分支合并到Adobe存储库的主控分支中。

>[!TIP]
>
>离开 **允许维护者进行编辑** 复选框，以确保Adobe文档团队可以对PR进行编辑。

![create-pr](../assets/create-pr.png)

您可以通过检查https://github.com/AdobeDocs/experience-platform.en中的拉取请求选项卡，确认已提交拉取请求。

![confirm-pr](../assets/confirm-pr.png)
