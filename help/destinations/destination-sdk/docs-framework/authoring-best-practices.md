---
title: 创作最佳实践
description: 了解在创作目标文档页面时应遵循的规则和提示，以确保它符合Adobe Experience Platform文档质量标准。
source-git-commit: 35e5c388e9572a3b27ec4bce55e766725936eda4
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# 创作最佳实践

## 概述 {#overview}

本页介绍了在 [创作目标文档](./documentation-instructions.md) 页面，以确保其符合Adobe Experience Platform文档质量标准。

## 一般指导 {#general-guidance}

* 在 [模板](./self-service-template.md) 有关目标文档，请参阅Adobe参与者指南，以了解有关 [链接](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en), [表](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#tables), [支持的markdown语法](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en), [编写指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en)，等等。
* 在产品文档中不要包含观察和估计。
* 在Experience Platform文档中，Adobe作者使用 **粗体格式** 要引用用户界面控件，请如下所示：
   * 转到 **[!UICONTROL 连接]** > **[!UICONTROL 目标]**，然后选择 **[!UICONTROL 目录]** 选项卡。 查看 [目标教程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#select-destination).

## 链接 {#linking}

请按照提供的文档模板操作，但不要编辑模板中的现有链接。 包含新链接时，请阅读 [在文档中使用链接](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en) 参与者指南中的。

## 品牌策略准则 {#branding}

* AEP不是已批准的面向公众的术语。 请先使用Adobe Experience Platform，然后Experience Platform，再使用Platform。
   * **不使用**:在将数据从AEP导出到YourDestination之前，请确保已阅读并完成这些先决条件。
   * **使用**:在将数据从Adobe Experience Platform导出到YourDestination之前，请确保已阅读并完成这些先决条件。

## 图像和屏幕截图 {#images-and-screenshots}

* 有关 [如何链接到图像](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#images)，请参阅参与者指南。
* 使用屏幕截图时，请确保您的屏幕截图可捕获整个Platform UI屏幕。
* 在标记图像以突出显示页面上的特定控件或标签时，请尝试遵循Experience Platform文档团队使用的标记样式。 请注意基于用户档案的内容如何在 [此屏幕截图](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* 请使用 `png` 设置图像格式。
* 请勿使用编号的屏幕截图作为文件名。 图像文件名应当具有描述性。
   * **不使用**: `1.png`, `2.png`, `3.png`
   * **使用**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* 请对您添加到文档中的任何图像使用替换文本，并在替换文本中使用正确的语法。
   * **不使用**:目标连接详细信息
   * **使用**:平台UI的图像，显示已填充的目标连接详细信息。

## 过程 {#process}

* 的 [文档模板](./self-service-template.md) 会根据合作伙伴的反馈，偶尔更新。 在开始为目标位置创作文档之前，请确保已下载 [模板的最新版本](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip).
* 创作文档并从分支的分支创建文档拉取请求(PR) *除主分支之外*. 在中创作时，请参阅提交目标以供审阅一节 [GitHub界面](./use-github-interface-to-create-documentation.md#submit-review) 或 [您的本地环境](./work-in-local-environment.md#submit-review).