---
title: 使用GitHub Web界面创建目标文档页面
description: 本页中的说明向您展示了如何使用GitHub Web界面为您的Experience Platform目标创作文档页面，并提交该页面以供审阅。
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 1%

---

# 使用GitHub Web界面创建目标文档页面 {#github-interface}

以下说明将向您展示如何使用GitHub Web界面创作文档和提交拉取请求(PR)。 完成此处指定的步骤之前，请确保已阅读 [在Adobe Experience Platform目标中记录您的目标](./documentation-instructions.md).

>[!TIP]
>
>另请参阅Adobe参与者指南中的支持文档：
>* [安装Git和Markdown创作工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [在本地设置适用于文档的 Git 存储库](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [针对主要更改的 GitHub 参与工作流](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## 设置GitHub创作环境 {#set-up-environment}

1. 在您的浏览器中，导航到 `https://github.com/AdobeDocs/experience-platform.en`.
2. 至 [分支](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) 在 **分叉** 如下所示。 这会在您自己的GitHub帐户中创建Experience Platform存储库的副本。

   ![分支Adobe文档存储库](../assets/docs-framework/ssd-fork-repository.gif)

3. 在存储库的分支中，为项目创建新分支，如下所示。 将这个新分支用于您的工作。

   ![新建GitHub分支](../assets/docs-framework/new-branch-github.gif)

4. 在分支存储库的GitHub文件夹结构中，导航到 `experience-platform.en/help/destinations/catalog/[...]`，其中 `[...]` 是目标的所需类别。 例如，如果您要将个性化目标添加到Experience Platform，请选择 `personalization` 类别。 选择 **添加文件>创建新文件**.

   ![添加新文件](../assets/docs-framework/github-navigate-and-create-file.gif)

5. 命名目标 `YOURDESTINATION.md`，其中YOURDESTINATION是您在Adobe Experience Platform中的目标名称。 例如，如果您的公司名为Moviestar，则需要为文件命名 `moviestar.md`.

## 为您的目标创作文档页面 {#author-documentation}

1. 您将根据 [文档自助模板](./self-service-template.md). **[下载](../assets/docs-framework/yourdestination-template.zip)** 然后解压缩该模板以提取 `.md` 文件模板。
2. 在在线标记编辑器中粘贴和编辑包含目标相关信息的模板内容，例如 [dillinger.io](https://dillinger.io/). 有关应填写哪些内容以及可以删除哪些段落的详细信息，请按照模板中的说明进行操作。

   >[!TIP]
   >
   >您可以随时关闭浏览器窗口，稍后重新打开。 您的工作会自动保存，在您重新打开浏览器时，将等待您完成。
3. 将内容从Markdown编辑器复制到GitHub中的新文件中。
4. 对于您计划使用的任何屏幕截图或图像，请使用GitHub界面将文件上传到 `experience-platform.en/help/destinations/assets/catalog/[...]`，其中 `[...]` 是目标的所需类别。 例如，如果您要将个性化目标添加到Experience Platform，请选择 `personalization` 类别。 您需要从要创作的页面链接到图像。 请参阅 [说明如何链接到图像](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).

   ![将图像上传到GitHub](../assets/docs-framework/upload-image.gif)

5. 准备就绪后，将文件保存在分支中。

![确认文件创建](../assets/docs-framework/ssd-confirm-file-creation.png)

## 提交文档以供审核 {#submit-review}

>[!TIP]
>
>请注意，这里没有什么可以打破的。 按照此部分中的说明，您只是建议进行文档更新。 您建议的更新将由Adobe Experience Platform文档团队批准或编辑。

1. 保存文件并上传所需的图像后，您可以打开拉取请求(PR)，以将工作分支合并到Adobe文档存储库的主控分支中。 确保已选择您处理的分支并选择 **Contribute >打开拉取请求**.

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
