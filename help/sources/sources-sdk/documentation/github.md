---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK;SDK
solution: Experience Platform
title: 使用GitHub Web界面创建源文档页面
description: 本文档提供了有关如何使用GitHub Web界面创作文档和提交拉取请求(PR)的步骤。
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 2%

---

# 使用GitHub Web界面创建源文档页面

本文档提供了有关如何使用GitHub Web界面创作文档和提交拉取请求(PR)的步骤。

>[!TIP]
>
>以下来自Adobe贡献指南的文档可用于进一步支持您的文档流程： <ul><li>[安装Git和Markdown创作工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)</li><li>[在本地设置适用于文档的 Git 存储库](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)</li><li>[针对主要更改的 GitHub 参与工作流](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en)</li></ul>

## 设置GitHub环境

设置GitHub环境的第一步是导航到 [Adobe Experience Platform GitHub存储库](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

接下来，选择 **分叉**.

![分支存储库](../assets/fork.png)

创建分支后，选择 **主控** 然后在显示的下拉菜单中输入新分支的名称。 确保为分支提供描述性名称，因为该名称将用于包含您的作品，然后选择 **创建分支**.

![创建分支](../assets/create-branch.png)

在分支存储库的GitHub文件夹结构中，导航到 [`experience-platform.en/help/sources/tutorials/api/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/api/create) 然后，从列表中选择源的相应类别。 例如，如果您正在为新CRM源创建文档，请选择 **crm**.

>[!TIP]
>
>如果您要为UI创建文档，请导航到 [`experience-platform.en/help/sources/tutorials/ui/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/ui/create) 并为源选择相应的类别。 要添加图像，请导航到 [`experience-platform.en/help/sources/images/tutorials/create/sdk`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/images/tutorials/create) 然后，将屏幕截图添加到 `sdk` 文件夹。

![crm](../assets/crm.png)

此时会显示现有CRM源的文件夹。 要为新源添加文档，请选择 **添加文件** 然后选择 **创建新文件** 下拉菜单中。

![create-new-file](../assets/create-new-file.png)

命名源文件 `YOURSOURCE.md` 其中，YOURSOURCE是Platform中源的名称。 例如，如果您的公司是ACME CRM，则您的文件名应为 `acme-crm.md`.

![git-interface](../assets/git-interface.png)

## 为源创作文档页面

要开始记录新源，请粘贴 [源文档模板](./template.md) 到GitHub Web编辑器中。 您还可以下载模板 [此处](../assets/api-template.zip).

将模板复制到GitHub Web编辑器界面后，按照模板中概述的说明操作，并编辑包含源相关信息的值。

![粘贴模板](../assets/paste-template.png)

完成后，在分支中提交文件。

![提交](../assets/commit.png)

## 提交文档以供审核

提交文件后，您可以打开拉取请求(PR)，以将工作分支合并到Adobe文档存储库的主控分支中。 确保已选中您正在处理的分支，然后选择 **比较和拉取请求**.

![比较pr](../assets/compare-pr.png)

确保基分支和比较分支正确无误。 向PR中添加说明更新的注释，然后选择 **创建拉取请求**. 这会打开一个PR，以将您工作的工作分支合并到Adobe存储库的主控分支中。

>[!TIP]
>
>离开 **允许维护者进行编辑** 复选框，以确保Adobe文档团队可以对PR进行编辑。

![create-pr](../assets/create-pr.png)

此时会显示一则通知，提示您签署Adobe参与者许可协议(CLA)。 这是强制步骤。 签署CLA后，刷新PR页面并提交拉取请求。

您可以通过检查https://github.com/AdobeDocs/experience-platform.en中的拉取请求选项卡，确认已提交拉取请求。

![confirm-pr](../assets/confirm-pr.png)
