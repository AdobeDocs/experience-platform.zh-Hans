---
title: 开发扩展
description: 本文档概述了标记扩展开发流程，并提供了指向更多文档的链接，以便了解更详细的流程。
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 43%

---

# 开发扩展

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

标记扩展应被视为具有自身要求的（小型）产品。 确定 Adobe Experience Platform 用户将希望如何使用您的扩展，可以帮助您将功能分类为扩展应提供的事件类型、条件类型、操作类型和数据元素类型。

利用这些知识，您可以规划扩展中应提供的组件。

## 指南

制定相应计划后，这些指南可以帮助您了解扩展开发流程：

* 此 [快速入门指南](../getting-started.md) 下的其他文件 **扩展开发** 在左侧导航中，提供了了解扩展的绝佳参考资料。 其中包括有关扩展功能的详细信息、如何存储用户信息以及在扩展和Adobe Experience Platform之间传递用户信息、如何将代码捆绑到库中，以及如何在浏览器中在运行时解释和使用扩展代码。
* 此 [扩展教程视频](https://youtu.be/rxjtC9o4rl0) 是个很好的起点。
* [扩展简介](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) YouTube 播放列表将讲解创建扩展包的过程。
* [了解 JSON 模式](https://spacetelescope.github.io/understanding-json-schema/index.html#)一文。
* [JSON Lint/验证器](https://jsonlint.com/)。
* [JSON 查看器](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh)，用于高亮显示和打印 JSON 和 JSONP 的 Chrome 扩展。
* [jsonschema.net](https://jsonschema.net/#/editor) 编辑器，可帮助您从对象创建 JSON 模式。
* [JSON 模式验证器](https://www.jsonschemavalidator.net)，一种在线交互式 JSON 模式验证器。

## 工具

还有许多 npm 工具可帮助您开发扩展包：

* [标记扩展基架工具](https://www.npmjs.com/package/@adobe/reactor-scaffold) 帮助您在本地计算机上轻松创建入门项目。
* [标记扩展沙盒](https://www.npmjs.com/package/@adobe/reactor-sandbox) 可帮助您在本地计算机上验证扩展视图和模块。
* [标记扩展打包程序](https://www.npmjs.com/package/@adobe/reactor-packager) 是一个命令行实用程序，用于将标记扩展打包到zip文件中。
* [标记扩展上载程序](https://www.npmjs.com/package/@adobe/reactor-uploader) 是一个交互式命令行工具，可帮助您输入技术帐户凭据并将扩展包上传到标记。
* [Tag Extension发布器](https://www.npmjs.com/package/@adobe/reactor-releaser) 是一个交互式命令行工具，可帮助您将扩展发布为私有版本。

## 扩展示例

GitHub上有一些扩展示例，您可以查看这些示例或将其用作起始项目：

* [Hello World 扩展示例](https://github.com/adobe/reactor-helloworld-extension)
* [Facebook 扩展示例](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Typekit 扩展示例](https://github.com/jeffchasin/extension-typekit)
* [Pinterest 扩展示例](https://github.com/jeffchasin/extension-pinterest)

## Slack 工作区

您可以请求对Slack社区工作区的访问权限，扩展作者可以使用此工作区来相互支持 [申请表](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform).

**请注意**：虽然此Slack工作区中有Adobe的成员，但它不是由Adobe赞助或管理的社区资源。
