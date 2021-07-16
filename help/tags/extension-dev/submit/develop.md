---
title: 开发扩展
description: 本文档提供了标记扩展开发过程的一般概述，其中包含指向更多详细流程文档的链接。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 40%

---

# 开发扩展

>[!NOTE]
>
>Adobe Experience Platform Launch正在Experience Platform中被重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../term-updates.md)。

标记扩展应被视为具有其自身要求的（小）产品。 确定 Adobe Experience Platform 用户将希望如何使用您的扩展，可以帮助您将功能分类为扩展应提供的事件类型、条件类型、操作类型和数据元素类型。

利用这些知识，您可以规划扩展中应提供的组件。

## 指南

制定相应计划后，这些指南可以帮助您了解扩展开发流程：

* 左侧导航栏中[扩展开发&#x200B;**下的](../getting-started.md)入门指南和其他文档是了解扩展的很好参考资料。**&#x200B;这些扩展包括有关扩展可以执行的操作、如何存储用户信息并在扩展和Adobe Experience Platform之间传递用户信息、如何将代码捆绑到库中，以及如何在浏览器中在运行时解释和使用扩展代码的详细信息。
* [扩展教程视频](https://youtu.be/rxjtC9o4rl0)是一个很好的入手点。
* [扩展简介](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) YouTube 播放列表将讲解创建扩展包的过程。
* [了解 JSON 模式](https://spacetelescope.github.io/understanding-json-schema/index.html#)一文。
* [JSON Lint/验证器](http://jsonlint.com/)。
* [JSON 查看器](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh)，用于高亮显示和打印 JSON 和 JSONP 的 Chrome 扩展。
* [jsonschema.net](https://jsonschema.net/#/editor) 编辑器，可帮助您从对象创建 JSON 模式。
* [JSON 模式验证器](http://www.jsonschemavalidator.net/)，一种在线交互式 JSON 模式验证器。

## 工具

还有许多 npm 工具可帮助您开发扩展包：

* [标记扩展基架工](https://www.npmjs.com/package/@adobe/reactor-scaffold) 具可帮助您在本地计算机上轻松创建起始项目。
* [标记扩展](https://www.npmjs.com/package/@adobe/reactor-sandbox) 沙盒可帮助您在本地计算机上验证扩展视图和模块。
* [标记扩](https://www.npmjs.com/package/@adobe/reactor-packager) 展包是一个命令行实用程序，用于将标记扩展打包到zip文件中。
* [标记扩](https://www.npmjs.com/package/@adobe/reactor-uploader) 展上载器是一个交互式命令行工具，可帮助您输入技术帐户凭据并将扩展包上载到标记。
* [标记扩展发](https://www.npmjs.com/package/@adobe/reactor-releaser) 布程序是一款交互式命令行工具，可帮助您将扩展发布为私有版本。

## 扩展示例

GitHub上有一些扩展示例，您可以查看这些示例或将其用作起始项目：

* [Hello World 扩展示例](https://github.com/adobe/reactor-helloworld-extension)
* [Facebook 扩展示例](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Typekit 扩展示例](https://github.com/jeffchasin/extension-typekit)
* [Pinterest 扩展示例](https://github.com/jeffchasin/extension-pinterest)

## Slack 工作区

您可以请求访问Slack社区工作区，扩展作者可以使用此[请求表单](http://join.launchdevelopers.chat)相互支持。

**请注意**:虽然此Slack工作区中有Adobe成员，但它不是由Adobe赞助或管理的社区资源。
