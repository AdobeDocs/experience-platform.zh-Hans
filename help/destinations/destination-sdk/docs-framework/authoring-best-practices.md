---
title: 创作最佳实践
description: 了解在创作目标文档页面时应遵循的规则和提示，以确保其符合Adobe Experience Platform文档质量标准。
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# 创作最佳实践

## 概述 {#overview}

本页介绍了在执行以下操作时应遵循的规则： [创作目标文档](./documentation-instructions.md) 页面，确保其符合Adobe Experience Platform文档质量标准。

## 一般指导 {#general-guidance}

* 填写时 [模板](./self-service-template.md) 有关目标文档，请参阅Adobe参与者指南，以了解有关 [链接](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en)， [表](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#tables)，则 [支持的markdown语法](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en)， [编写指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en)，等等。
* 不要在产品文档中包括观察和估计。
* 在Experience Platform文档中，Adobe作者使用 **粗体格式** 要引用用户界面控件，如下所示：
   * 转到 **[!UICONTROL 连接]** > **[!UICONTROL 目标]**，并选择 **[!UICONTROL 目录]** 选项卡。 查看有关用户界面控件如何记录在中的示例 [目标教程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#select-destination).

## 书写样式

>[!IMPORTANT]
>
>读取 [Adobe文档编写指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) 开始创作目标文档页面之前。

* 把你的句子短一点，尽快切入正题。 如果您的句子长度超过20个单词或使用多个逗号，请考虑将其拆分为单独的句子。 长度超过20个单词的句子对读者来说尤其具有挑战性。
* 别太客气了。 避免在技术文档中使用“请”或“请……”。

## 链接 {#linking}

按照提供的文档模板进行操作，并且不要编辑模板中的现有链接。 包含新链接时，请阅读 [在文档中使用链接](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en) 在投稿人指南中。

## 品牌指南 {#branding}

* AEP不是一个经批准的面向公众的术语。 请在首次使用时使用Adobe Experience Platform，然后依次使用Experience Platform和平台。
   * **不使用**：将数据从AEP导出到YourDestination之前，请确保已阅读并完成这些先决条件。
   * **使用**：将数据从Adobe Experience Platform导出到YourDestination之前，请确保已阅读并完成这些先决条件。

## 图像和屏幕快照 {#images-and-screenshots}

* 有关以下项的信息 [如何链接到图像](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#images)，请参阅投稿人指南。
* 在使用屏幕快照时，请确保您的屏幕快照捕获了整个Platform UI屏幕。
* 在标记图像以突出显示页面上的某个控件或标签时，请尝试遵循Experience Platform文档团队使用的标记样式。 请注意如何在中高亮显示基于配置文件的 [此屏幕快照](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* 请使用 `png` 设置图像格式。
* 请勿使用编号屏幕快照作为文件名。 图像文件名应为描述性的。
   * **不使用**： `1.png`， `2.png`， `3.png`
   * **使用**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* 请为您添加到文档的任何图像使用替换文字，并在替换文字中使用适当的语法。
   * **不使用**：目标连接详细信息
   * **使用**：Platform UI的图像，其中显示填写的目标连接详细信息。

## 过程 {#process}

* 此 [文档模板](./self-service-template.md) 很少根据合作伙伴反馈进行更新。 在开始为目标创作文档之前，请确保已下载 [模板的最新版本](../assets/docs-framework/yourdestination-template.zip).
* 创作文档并从分支存储库中创建文档拉取请求(PR) *除主分支之外*. 在中创作时，请参阅提交目标以供查看一节 [GitHub界面](./use-github-interface-to-create-documentation.md#submit-review) 或位于 [您的本地环境](./work-in-local-environment.md#submit-review).
