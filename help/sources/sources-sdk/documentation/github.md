---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK；SDK
solution: Experience Platform
title: 使用GitHub Web界面创建源文档页面
description: 本文档提供了有关如何使用GitHub Web界面创作文档并提交拉取请求(PR)的步骤。
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 2%

---

# 使用GitHub Web界面创建源文档页面

本文档提供了有关如何使用GitHub Web界面创作文档并提交拉取请求(PR)的步骤。

>[!TIP]
>
>Adobe投稿指南中的以下文档可用于进一步支持您的文档流程： <ul><li>[安装Git和Markdown创作工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)</li><li>[在本地设置适用于文档的 Git 存储库](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)</li><li>[针对主要更改的 GitHub 参与工作流](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html)</li></ul>

## 设置GitHub环境

设置GitHub环境的第一步是导航到 [Adobe Experience Platform GitHub存储库](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

接下来，选择 **分支**.

![分支存储库](../assets/fork.png)

创建分支后，选择 **母版** 并在出现的下拉菜单中为新分支输入名称。 请确保为分支提供描述性名称，因为这将用于包含您的工作，然后选择 **创建分支**.

![create-branch](../assets/create-branch.png)

在分支存储库的GitHub文件夹结构中，导航到 [`experience-platform.en/help/sources/tutorials/api/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/api/create) 然后从列表中选择适合您的源的类别。 例如，如果要为新的CRM源创建文档，请选择 **crm**.

>[!TIP]
>
>如果您正在创建UI文档，请导航到 [`experience-platform.en/help/sources/tutorials/ui/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/ui/create) 并为您的源选择适当的类别。 要添加图像，请导航至 [`experience-platform.en/help/sources/images/tutorials/create/sdk`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/images/tutorials/create) 然后将屏幕截图添加到 `sdk` 文件夹。

![crm](../assets/crm.png)

此时将显示现有CRM源的文件夹。 要添加新源的文档，请选择 **添加文件** 然后选择 **创建新文件** 从出现的下拉菜单中。

![create-new-file](../assets/create-new-file.png)

命名源文件 `YOURSOURCE.md` 其中，YOURSOURCE是您在Platform中的源的名称。 例如，如果您的公司是ACME CRM，则您的文件名应为 `acme-crm.md`.

![git-interface](../assets/git-interface.png)

## 为您的源创作文档页面

要开始记录您的新源，请粘贴源中 [源文档模板](./template.md) 到GitHub Web编辑器中。 您还可以下载模板 [此处](../assets/api-template.zip).

将模板复制到GitHub Web编辑器界面后，按照模板中列出的说明操作，并编辑包含源相关信息的值。

![粘贴模板](../assets/paste-template.png)

完成后，在分支中提交文件。

![提交](../assets/commit.png)

## 提交文档以供审阅

提交文件后，您可以打开拉取Adobe(PR)，将您的工作分支合并到分支文档存储库的主分支中。 确保选中您之前处理的分支，然后选择 **比较和拉取请求**.

![compare-pr](../assets/compare-pr.png)

确保基础分支和比较分支正确。 向PR添加注释以描述您的更新，然后选择 **创建拉取请求**. 这将打开一个PR，以将您工作的工作分支合并到Adobe存储库的主分支。

>[!TIP]
>
>离开 **允许维护者编辑** 选中此复选框以确保Adobe文档团队可以对PR进行编辑。

![create-pr](../assets/create-pr.png)

此时，将显示一条通知，提示您签署Adobe参与者许可协议(CLA)。 这是强制步骤。 签署CLA后，刷新PR页面并提交拉取请求。

您可以通过检查https://github.com/AdobeDocs/experience-platform.en中的“拉取请求”选项卡，确认已提交拉取请求。

![confirm-pr](../assets/confirm-pr.png)
