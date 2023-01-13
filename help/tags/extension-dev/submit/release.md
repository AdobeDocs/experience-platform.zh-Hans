---
title: 发布扩展
description: 了解如何在Adobe Experience Platform中私密或公开发布标记扩展。
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 8862a911f09d47c3a2260faba045f3c79826b52c
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 46%

---

# 发布扩展

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

测试和文档记录完成后，扩展即可发布。 当前，可执行两种类型的发布：

- **私密发布**:完成的扩展适用于贵公司内的所有资产，但不适用于Adobe Experience Platform中的任何其他公司。
- **公开发布**:完成的扩展可在公共商城中提供给所有Adobe Experience Platform用户。

>[!NOTE]
>
>扩展发布后，您将无法再对其进行更改，也无法取消发布。  发布扩展后，可通过 `POST` 发布扩展包的新版本并对新版本执行上述测试和发布步骤，来修复错误和添加功能。

您必须先以私有扩展的形式发布扩展，然后才能公开发布。

## 私密发布

私密发布扩展的最简单方法是使用 [标记扩展发行版](https://www.npmjs.com/package/@adobe/reactor-releaser). 在其文档中，提供了更多的相关说明。

如果您希望直接使用API私密发布扩展，请参阅的示例调用 [私密发布扩展包](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/release_private/) ，以了解更多详细信息。

## 公开发布

完成私密发布后，您可以请求 Adobe 公开发布扩展。这会使您的扩展出现在 Public 目录中。任何数据收集用户都可以将您的扩展安装到任何资产中。

请填写[公开发布申请表单](https://experiencecloudpanel.adobe.com/c/r/DCExtensionReleaseRequest)，以开始完成发布流程。
