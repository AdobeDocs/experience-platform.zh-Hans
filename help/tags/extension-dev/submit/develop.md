---
title: 开发扩展
description: 本文档提供了标记扩展开发过程的一般概述，以及指向更多文档的链接，这些文档提供了更详细的流程。
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
source-git-commit: cfcc70d66a34fa51bf0e21525539ba88de7fc367
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 31%

---

# 开发扩展

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

标记扩展应被视为具有自身要求的（小型）产品。 确定Adobe Experience Platform用户将希望如何使用您的扩展，可以帮助您将功能分类为扩展应提供的事件类型、条件类型、操作类型和数据元素类型。

利用这些知识，您可以规划扩展中应提供的组件。

## 指南

制定相应计划后，这些指南可以帮助您了解扩展开发流程：

* 左侧导航栏中&#x200B;**扩展开发**&#x200B;下的[入门指南](../getting-started.md)和其他文档是了解扩展的绝佳参考资料。 其中包括有关扩展功能的详细信息、如何存储用户信息并在扩展和Adobe Experience Platform之间传递用户信息、如何将代码捆绑到库中，以及如何在浏览器中在运行时解释和使用扩展代码。
<!-- * The [extension tutorial video](https://youtu.be/rxjtC9o4rl0) is a great place to start. -->
* [扩展简介](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) YouTube 播放列表将讲解创建扩展包的过程。
* [了解 JSON 架构](https://spacetelescope.github.io/understanding-json-schema/index.html#)一文。
* [JSON Lint/验证器](https://jsonlint.com/)。
* [JSON 查看器](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh)，用于高亮显示和打印 JSON 和 JSONP 的 Chrome 扩展。
* [jsonschema.net](https://jsonschema.net/#/editor)编辑器，可帮助您从对象创建JSON架构。
* [JSON 架构验证器](https://www.jsonschemavalidator.net)，一种在线交互式 JSON 架构验证器。

## 工具

还有许多 npm 工具可帮助您开发扩展包：

* [标记扩展基架工具](https://www.npmjs.com/package/@adobe/reactor-scaffold)可帮助您在本地计算机上轻松创建起始项目。
* [标记扩展沙盒](https://www.npmjs.com/package/@adobe/reactor-sandbox)可帮助您在本地计算机上验证扩展视图和模块。
* [Tag Extension Packager](https://www.npmjs.com/package/@adobe/reactor-packager)是一个命令行实用程序，用于将标记扩展打包到zip文件中。
* [Tag Extension Uploader](https://www.npmjs.com/package/@adobe/reactor-uploader)是一个交互式命令行工具，可帮助您输入技术帐户凭据并将扩展包上载到标记。
* [Tag Extension Releaser](https://www.npmjs.com/package/@adobe/reactor-releaser)是一个交互式命令行工具，可帮助您将扩展发布为私有版本。

## 扩展示例

GitHub上有一些扩展示例，您可以查看这些示例或将其用作起始项目：

* [Hello World 扩展示例](https://github.com/adobe/reactor-helloworld-extension)
* [Facebook 扩展示例](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Typekit 扩展示例](https://github.com/jeffchasin/extension-typekit)
* [Pinterest 扩展示例](https://github.com/jeffchasin/extension-pinterest)

## Slack 工作区

您可以使用此[请求表单](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform)来请求访问Slack社区工作区，扩展作者可以在该工作区中相互支持。

**请注意**：尽管此Slack工作区中有Adobe的成员，但它不是由Adobe赞助或管理的社区资源。
