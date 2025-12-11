---
title: 扩展开发快速入门
description: 开始在Adobe Experience Platform中开发您自己的标记扩展。
exl-id: 3925b928-0180-4a4f-aaa6-42f342089560
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 59%

---

# 扩展开发入门

为了帮助您启动、运行和构建扩展，我们将使用由Adobe工程师提供的开源基架工具为您的扩展包创建必要的文件和文件结构，因此您只需做一个最重要的部分即可：实际编写代码。

## 先决条件

* 安装 [Node.js](https://nodejs.org/en/download/)。

## 扩展设置

创建扩展文件的存放目录。

```shell
mkdir example && cd example
```

本指南利用扩展基架工具来构建初始扩展结构，以便开发人员可以快速开始编码。如果需要，可以在不使用基架工具的情况下手动完成此过程。

运行基架工具。

```shell
npx @adobe/reactor-scaffold
```

基架工具将提示输入一些初始配置选项，如下所示：

* 显示名称 - 扩展的可见名称
* Platform — 指定扩展是针对Web、移动还是边缘开发
* 版本 - 扩展的版本
* 描述 - 扩展的简短用途描述
* 作者 - 扩展的作者姓名

>[!NOTE]
> 对于移动扩展，将询问有关Android和iOS应用程序结构的几个问题。

然后，基架工具将提供用于构建扩展结构的选项：

* [扩展配置视图](./configuration.md)：视图 HTML 文件，扩展可通过该文件从用户那里收集全局设置。
* [事件类型](./web/event-types.md)：定义要观察的活动。例如，了解用户何时快速滚动，或者用户何时与页面元素交互。然后可以在规则中利用事件来执行操作。
* [条件类型](./web/condition-types.md)：条件类型评估某些内容是 true 还是 false。例如，如果用户浏览器是Chrome、他们正在使用iPad，或者用户位于特定域上，则可以返回此值。
* [操作类型](./web/action-types.md)：事件发生时要执行的操作。例如，发送分析信标、显示产品建议、保存 Cookie 或打开支持聊天。
* [数据元素类型](./web/data-element-types.md)：数据元素类型检索一段数据。此数据可以位于本地存储、Cookie、DOM 元素或自定义位置中。
* [共享模块](./web/shared.md)（仅限Web）：共享模块是一种扩展可用来与其他扩展进行通信的机制。
* [视图](./web/views.md)：每个事件、条件、操作或数据元素类型可以提供允许用户提供设置的视图。
* Exchange URL（仅限Web和Edge）：将扩展发布到Adobe的公共目录时，请在此处提供列表URL。
* 图标路径：扩展名的图标文件的路径。

>[!NOTE]
>
>* 基架工具的后续运行将跳过初始配置。
>* 可以添加每个事件、条件、操作的多个视图。
>* 只能存在一个配置视图。

## 后续步骤

* 遵循[提交流程概述](./submit/overview.md)，并准备[验证](./submit/upload-and-test.md#validate)和[上传](./submit/upload-and-test.md#integration)您的扩展以在标记生态系统中进行测试。
