---
title: 在Adobe Experience Platform中记录您的目标
description: 分步说明，以便您在Adobe Experience Platform中为目标创建文档页面
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: ffd87573b93d642202e51e5299250a05112b6058
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---

# 在Adobe Experience Platform中记录您的目标

>[!IMPORTANT]
>
>只有提交产品化（公共）目标的合作伙伴才需要此处记录的流程。 如果您创建供自己使用的专用目标，则无需为该目标创建和发布文档。

## 概述 {#overview}

欢迎来到Adobe Experience Platform，很高兴你来！
记录目标是在Adobe Experience Platform中实时设置目标之前的最后一步。

本文档部分包括：

* 为新目标创建文档页面的分步说明；
* 模板供您填写目标；
* [有关使用Markdown的常规说明](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en);
* [有关AdobeMarkdown风味的具体说明](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#custom-markdown-extensions) (AdobeMarkdown的风格与常规Markdown非常相似)。
* A [最佳实践页面](./authoring-best-practices.md) 以帮助您为目标页面创作文档页面，该页面符合Experience Platform文档质量标准。

## 先决条件 {#prerequisites}

要根据本文中的说明为目标创建文档，需要以下项目：

* **GitHub帐户**. 注册 [GitHub](https://github.com/) 如果您还没有帐户。
* **GitHub Desktop**. 如果您选择 [在本地环境中创建文档](./work-in-local-environment.md)，您必须使用 [GitHub Desktop](https://desktop.github.com/).
* 您与Adobe的集成必须处于测试阶段，且目标部署在Adobe Experience Platform的暂存环境中。

## 在Adobe Experience Platform中为您的目标创建文档的高级说明 {#high-level-instructions}

要为目标创建文档，您需要 [创建分支](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) Adobe Experience Platform文档存储库的页面，并编辑 [提供的文档模板](./self-service-template.md) 在新的分支中。 使用Adobe提供的模板创建新目标页面。 准备就绪后，打开拉取请求(PR)。 下面将进一步说明如何执行此操作： [创建新目标页面的步骤](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## 文档模板 {#documentation-template}

为了帮助您创建文档页面，Adobe已预填了 [文档模板](./self-service-template.md) 为你。 在下面，您可以找到如何编辑模板和打开拉取请求的说明。 Adobe文档团队将审核并发布您新目标的文档。

[在此处下载模板](../assets/docs-framework/yourdestination-template.zip) 并解压缩文件以解压缩 `yourdestination.md` 文件。

有关使用模板创建文档页面的说明，请参阅下文。

## 创建新目标页面的步骤 {#steps-to-create-docs-page}

您可以使用GitHub Web界面或本地环境，在Adobe Experience Platform中为新目标创建文档。 请在以下链接中找到两个选项的说明：

* [使用GitHub Web界面创建目标文档页面](./use-github-interface-to-create-documentation.md)
* [在本地环境中使用文本编辑器创建目标文档页面](./work-in-local-environment.md)

## 最佳实践 {#best-practices}

查看 [创作最佳实践](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) 在创建目标文档页面之前和期间。 另请务必阅读 [Adobe文档编写指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) 有关Adobe文档团队在创作文档时使用的一些更多编写提示。