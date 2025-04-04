---
title: 创作最佳实践
description: 了解在创作目标文档页面时应遵循的规则和提示，以确保其符合Adobe Experience Platform文档质量标准。
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 创作最佳实践

## 概述 {#overview}

本页介绍了在[创作目标文档](./documentation-instructions.md)页面时应遵循的规则，以确保其符合Adobe Experience Platform文档质量标准。

## 一般指导 {#general-guidance}

* 在填写目标文档的[模板](./self-service-template.md)时，请参阅Adobe参与者指南以了解有关[链接](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html)、[表](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#tables)、[支持的Markdown语法](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html)、[编写指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html)等的信息。
* 不要在产品文档中包括观察和估计。
* 在Experience Platform文档中，Adobe作者使用&#x200B;**粗体格式**&#x200B;来引用用户界面控件，如下所示：
   * 转到&#x200B;**[!UICONTROL 连接]** > **[!UICONTROL 目标]**，然后选择&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡。 在[目标教程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#select-destination)中查看用户界面控件的说明示例。

## 写作风格

>[!IMPORTANT]
>
>在开始创作目标文档页面之前，请阅读[Adobe文档的编写指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html)。

* 把你的句子短一点，尽快切入正题。 如果您的句子超过20个单词或使用多个逗号，请考虑将其拆分为单独的句子。 长度超过20个词的句子对读者来说尤其具有挑战性。
* 别太客气了。 避免在技术文档中使用“请”或“请……”。

## 链接 {#linking}

按照提供的文档模板操作，不要编辑模板中的现有链接。 当包含新链接时，请使用参与者指南中的文档](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html)中的链接阅读[。

## 品牌指南 {#branding}

* AEP不是一个公认的公开术语。 请先使用Adobe Experience Platform，然后再使用Experience Platform，最后再使用Experience Platform。
   * **请勿使用**：在将数据从AEP导出到YourDestination之前，请确保已阅读并完成这些先决条件。
   * **使用**：在将数据从Adobe Experience Platform导出到YourDestination之前，请确保已阅读并完成这些先决条件。

## 图像和屏幕快照 {#images-and-screenshots}

* 有关[如何链接到图像](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#images)的信息，请参阅参与者指南。
* 在使用屏幕截图时，请确保您的屏幕截图捕获了整个Experience Platform UI屏幕。
* 在标记图像以突出显示页面上的某个控件或标签时，请尝试遵循Experience Platform文档团队使用的标记样式。 请注意，在[此屏幕快照](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency)中如何高亮显示基于配置文件的。
* 请使用`png`格式图像。
* 请勿使用编号屏幕截图作为文件名。 图像文件名应为描述性的。
   * **不使用**： `1.png`，`2.png`，`3.png`
   * **使用**： `yourdestination-authentication-details.png`，`yourdestination-destination-details.png`
* 请为您添加到文档的任何图像使用替换文本，并在替换文本中使用正确的语法。
   * **不使用**：目标连接详细信息
   * **使用**： Experience Platform UI的图像，显示填写的目标连接详细信息。

## 进程 {#process}

* [文档模板](./self-service-template.md)很少根据合作伙伴反馈进行更新。 开始为目标创作文档之前，请确保已下载[最新版本的模板](../assets/docs-framework/yourdestination-template.zip)。
* 创作文档并从分支&#x200B;*中除主分支*&#x200B;之外的其他分支创建文档拉取请求(PR)。 在[GitHub接口](./use-github-interface-to-create-documentation.md#submit-review)或[您的本地环境](./work-in-local-environment.md#submit-review)中进行创作时，请参阅提交目标以供审核部分。
