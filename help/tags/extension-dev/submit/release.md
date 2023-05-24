---
title: 發行擴充功能
description: 瞭解如何在Adobe Experience Platform中私下或公開發佈標籤擴充功能。
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 60d88be5d710314cdc6900f4b63643c740b91fa6
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 44%

---

# 发布扩展

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

完成測試和檔案化後，擴充功能即可發行。 当前，可执行两种类型的发布：

- **私人發行**：完成的擴充功能可供貴公司內的所有屬性使用，但不適用於Adobe Experience Platform中的任何其他公司。
- **公開發行**：所有Adobe Experience Platform使用者皆可在公開Marketplace中取得已完成的擴充功能。

>[!NOTE]
>
>擴充功能一經發行即無法變更，也無法取消發行。  发布扩展后，可通过 `POST` 发布扩展包的新版本并对新版本执行上述测试和发布步骤，来修复错误和添加功能。

您必须先以私有扩展的形式发布扩展，然后才能公开发布。

## 私密发布

要發行具有私人可用性的擴充功能，最簡單的方式是使用 [標籤延伸功能發行者](https://www.npmjs.com/package/@adobe/reactor-releaser). 在其文档中，提供了更多的相关说明。

如果您想要直接使用API發行具有私人可用性的擴充功能，請參閱的呼叫範例 [私下發行擴充功能套件](../../api/endpoints/extension-packages.md/#private-release) API檔案中取得更多詳細資訊。

## 公开发布

完成私密发布后，您可以请求 Adobe 公开发布扩展。这会使您的扩展出现在 Public 目录中。任何資料收集使用者都可將您的擴充功能安裝至任何屬性。

请填写[公开发布申请表单](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest)，以开始完成发布流程。
