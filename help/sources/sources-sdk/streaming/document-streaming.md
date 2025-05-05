---
title: 记录您的Source(流SDK)
description: 在Adobe Experience Platform中启用新源之前的最后一步是记录新源。
exl-id: 65ca7a4d-3e02-4f54-bf07-ea2c92b8dbf1
badge: Beta 版
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# 记录您的源(流SDK)

>[!NOTE]
>
>自助来源流SDK处于测试阶段。 有关使用测试版标记源的更多信息，请阅读[源概述](../../home.md#terms-and-conditions)。

在Adobe Experience Platform中实时设置新源之前的最后一步是记录新源。

此文档指南包括：

* 接下来可以学习的教程，为您的新源创建文档页面；
* 供您为新源填写的文档模板；
* [有关如何使用Markdown编写技术文档的说明](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=zh-Hans)；
* [有关了解Adobe Markdown风格的说明](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=zh-Hans#custom-markdown-extensions)。

## 先决条件

在开始记录新源之前，需要以下项：

* **有效的GitHub用户帐户**：如果您没有现有的GitHub帐户，则必须通过[GitHub注册页面](https://github.com/)创建一个；
* **访问GitHub Desktop**：若要在本地环境中创建源文档，您必须使用[GitHub Desktop应用程序](https://desktop.github.com/)；
* 与Adobe的集成必须处于测试阶段，并且您的源部署在Experience Platform中的暂存环境中。

## 在Experience Platform中为源创建文档的高级说明

概言之，要为源创建文档，您需要创建Experience Platform文档存储库的分支，并在新分支中编辑提供的文档模板。 使用Adobe提供的模板创建一个新的源页面，并在您准备就绪后打开拉取请求(PR)。 下面在创建新源页面的步骤中提供了进一步的操作说明。

## 文档模板

您可以使用预填充的[API文档模板](streaming-template-api.md)或[UI文档模板](streaming-template-ui.md)来协助创建源的文档。 此外，您还可以找到有关如何编辑模板和打开拉取请求的说明。 为您的新源提交的文档将由Adobe文档团队审阅并发布。

您还可以下载以下文档模板：

* [API文档模板](../assets/streaming/streaming-template-api.zip)
* [UI文档模板](../assets/streaming/streaming-template-ui.zip)

## 新建源页面

您可以使用GitHub Web界面或本地环境在Experience Platform中为新源创建文档。 请在下面的链接中找到有关这两个选项的说明：

* [使用GitHub Web界面创建源文档页面](../documentation/github.md)
* [在本地环境中使用文本编辑器创建源文档页面](../documentation/text-editor.md)
