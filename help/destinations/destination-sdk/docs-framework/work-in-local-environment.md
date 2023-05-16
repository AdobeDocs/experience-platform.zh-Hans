---
title: 在本地环境中使用文本编辑器创建目标文档页面
description: 本页面上的说明向您展示了如何使用文本编辑器在本地环境中工作，以创作Experience Platform目标的文档页面并提交该页面以供审阅。
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 2%

---

# 在本地环境中使用文本编辑器创建目标文档页面 {#local-authoring}

本页面上的说明向您展示了如何使用文本编辑器在本地环境中工作，以创作文档并提交拉取请求(PR)。 完成此处指定的步骤之前，请确保已阅读 [在Adobe Experience Platform目标中记录您的目标](./documentation-instructions.md).

>[!TIP]
>
>另请参阅Adobe参与者指南中的支持文档：
>* [安装Git和Markdown创作工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [在本地设置适用于文档的 Git 存储库](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [针对主要更改的 GitHub 参与工作流](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## 连接到GitHub并设置本地创作环境 {#set-up-environment}

1. 在您的浏览器中，导航到 `https://github.com/AdobeDocs/experience-platform.en`
2. 至 [分支](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) 在 **分叉** 如下所示。 这会在您自己的GitHub帐户中创建Experience Platform存储库的副本。

   ![分支Adobe文档存储库](../assets/docs-framework/ssd-fork-repository.gif)

3. 将存储库克隆到您的本地计算机. 选择 **代码> HTTPS >使用GitHub Desktop打开**，如下所示。 确保您已 [GitHub Desktop](https://desktop.github.com/) 已安装。 有关进一步的参考，请阅读 [创建存储库的本地克隆](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository) 中的Adobe参与者指南。

   ![将Adobe文档存储库克隆到本地环境](../assets/docs-framework/clone-local.png)

4. 在本地文件结构中，导航到 `experience-platform.en/help/destinations/catalog/[...]`，其中 `[...]` 是目标的所需类别。 例如，如果您要将个性化目标添加到Experience Platform，请选择 `personalization` 文件夹。

## 为您的目标创作文档页面 {#author-documentation}

1. 您的文档页面基于 [自助服务目标模板](../docs-framework/self-service-template.md). 下载 [目标模板](../assets/docs-framework/yourdestination-template.zip). 解压缩并解压缩文件 `yourdestination-template.md` 到上面步骤4中所述的目录。  重命名文件 `YOURDESTINATION.md`，其中YOURDESTINATION是您在Adobe Experience Platform中的目标名称。 例如，如果您的公司名为Moviestar，则需要为文件命名 `moviestar.md`.
2. 在 [选择的文本编辑器](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors). Adobe建议您使用 [Visual Studio代码](https://code.visualstudio.com/) 并安装AdobeMarkdown Authoring扩展。 要安装扩展，请打开Visual Studio代码，选择 **[!DNL Extensions]** ，然后搜索 `adobe markdown authoring`. 选择扩展并单击 **[!DNL Install]**.
   ![安装AdobeMarkdown创作扩展](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. 使用目标的相关信息编辑模板。 按照模板中的说明操作。
4. 有关您计划添加到文档中的任何屏幕截图或图像，请转到 `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`，其中 `[...]` 是目标的所需类别。 例如，如果您要将个性化目标添加到Experience Platform，请选择 `personalization` 文件夹。 为目标创建新文件夹，然后将图像保存在此处。 您必须从正在创作的页面中链接到这些页面。 请参阅 [说明如何链接到图像](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).
5. 准备就绪后，保存正在处理的文件。

## 提交文档以供审核 {#submit-review}

>[!TIP]
>
>请注意，这里没有什么可以打破的。 按照此部分中的说明，您只是建议进行文档更新。 您建议的更新将由Adobe Experience Platform文档团队批准或编辑。

1. 在GitHub Desktop中，为您的更新创建一个工作分支，然后选择 **发布分支** 将分支发布到GitHub。

![本地新分支](../assets/docs-framework/new-branch-local.gif)

1. 在GitHub Desktop中， [提交](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) 您的工作，如下所示。

   ![提交本地](../assets/docs-framework/commit-local.png)

1. 在GitHub Desktop中， [推送](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) 你的工作 [远程](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote) 分支，如下所示。

   ![推送您的提交](../assets/docs-framework/push-local-to-remote.png)

1. 在GitHub Web界面中，打开拉取请求(PR)，将您的工作分支合并到Adobe文档存储库的主控分支中。 确保已选择您处理的分支并选择 **Contribute >打开拉取请求**.

   ![创建拉取请求](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. 确保基分支和比较分支正确无误。 向PR中添加说明更新的注释，然后选择 **创建拉取请求**. 此操作将打开一个PR，将分支的工作分支合并到Adobe存储库的主控分支中。
   >[!TIP]
   >
   >离开 **允许维护者进行编辑** 复选框，以便Adobe文档团队可以对PR进行编辑。

   ![创建拉取请求以Adobe文档存储库](../assets/docs-framework/ssd-create-pull-request-2.png)

1. 此时会显示一则通知，提示您签署Adobe参与者许可协议(CLA)。 这是强制步骤。 签署CLA后，刷新PR页面并提交拉取请求。

1. 您可以通过检查 **拉取请求** 选项卡 `https://github.com/AdobeDocs/experience-platform.en`.

![PR成功](../assets/docs-framework/ssd-pr-successful.png)

1. 谢谢！Adobe文档团队将在PR中联系，以防需要进行任何编辑，并告知您文档何时发布。

>[!TIP]
>
>要添加图像和文档链接，以及有关Markdown的任何其他问题，请阅读 [使用Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) Adobe的协作编写指南。
