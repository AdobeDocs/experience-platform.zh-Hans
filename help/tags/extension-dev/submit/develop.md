---
title: 開發擴充功能
description: 本檔案提供標籤擴充功能開發程式的一般概覽，以及更多詳細程式的進一步檔案連結。
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 43%

---

# 开发扩展

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

標籤擴充功能應視為具有自身需求的（小型）產品。 确定 Adobe Experience Platform 用户将希望如何使用您的扩展，可以帮助您将功能分类为扩展应提供的事件类型、条件类型、操作类型和数据元素类型。

有了這些知識，您就可以規劃擴充功能中應該提供哪些元件。

## 指南

制定相应计划后，这些指南可以帮助您了解扩展开发流程：

* 此 [快速入門手冊](../getting-started.md) 下的其他檔案 **擴充功能開發** 左側導覽中的「 」是瞭解擴充功能的絕佳參考資料。 其中包含擴充功能的功能、如何儲存使用者資訊以及在擴充功能和Adobe Experience Platform之間加以傳遞、如何將程式碼整合到程式庫中，以及在執行階段如何在瀏覽器中解譯和使用擴充功能程式碼的詳細資訊。
* 此 [擴充功能教學課程影片](https://youtu.be/rxjtC9o4rl0) 是個絕佳的起點。
* [扩展简介](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) YouTube 播放列表将讲解创建扩展包的过程。
* [了解 JSON 模式](https://spacetelescope.github.io/understanding-json-schema/index.html#)一文。
* [JSON Lint/验证器](https://jsonlint.com/)。
* [JSON 查看器](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh)，用于高亮显示和打印 JSON 和 JSONP 的 Chrome 扩展。
* [jsonschema.net](https://jsonschema.net/#/editor) 编辑器，可帮助您从对象创建 JSON 模式。
* [JSON 模式验证器](https://www.jsonschemavalidator.net)，一种在线交互式 JSON 模式验证器。

## 工具

还有许多 npm 工具可帮助您开发扩展包：

* [標籤延伸架構工具](https://www.npmjs.com/package/@adobe/reactor-scaffold) 可協助您在本機電腦上輕鬆建立入門專案。
* [標籤延伸模組沙箱](https://www.npmjs.com/package/@adobe/reactor-sandbox) 可協助您驗證本機電腦上的擴充功能檢視和模組。
* [標籤延伸封裝程式](https://www.npmjs.com/package/@adobe/reactor-packager) 是一個命令列公用程式，用於將標籤副檔名封裝到zip檔案中。
* [標籤延伸上傳程式](https://www.npmjs.com/package/@adobe/reactor-uploader) 是一款互動式命令列工具，可協助您輸入技術帳戶認證，並將擴充功能套件上傳至標籤。
* [標籤延伸功能發行者](https://www.npmjs.com/package/@adobe/reactor-releaser) 是一款互動式命令列工具，可協助您發行擴充功能供私人使用。

## 扩展示例

GitHub上有範例擴充功能，可供檢閱或作為起始專案：

* [Hello World 扩展示例](https://github.com/adobe/reactor-helloworld-extension)
* [Facebook 扩展示例](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Typekit 扩展示例](https://github.com/jeffchasin/extension-typekit)
* [Pinterest 扩展示例](https://github.com/jeffchasin/extension-pinterest)

## Slack 工作区

您可以要求Slack社群工作區的存取權，擴充功能作者可透過此工具互相支援 [請求表單](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform).

**請注意**：雖然此Slack工作區中有Adobe的成員，但這項社群資源並非由Adobe贊助或主導。
