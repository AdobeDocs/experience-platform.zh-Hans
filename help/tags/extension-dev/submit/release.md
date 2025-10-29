---
title: 发布扩展
description: 了解如何在Adobe Experience Platform中私密或公开发布标记扩展。
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 25%

---

# 发布扩展

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

测试和文档记录完成后，扩展即可发布。 当前，可执行两种类型的发布：

- **私有版本**：完成的扩展可用于贵公司内的所有资产，但不能用于Adobe Experience Platform中的任何其他公司。
- **公开发布**：完成的扩展可在公共商城中提供给所有Adobe Experience Platform用户。

>[!NOTE]
>
>扩展一经发布，您将无法再对其进行更改，并且也无法取消发布。  发布扩展后，可通过 `POST` 发布扩展包的新版本并对新版本执行上述测试和发布步骤，来修复错误和添加功能。

您必须先以私有扩展的形式发布扩展，然后才能公开发布。

## 私密发布

私密发布扩展的最简单方法是使用[标记扩展发布器](https://www.npmjs.com/package/@adobe/reactor-releaser)。

```bash
npx @adobe/reactor-releaser
```

`npx`允许您下载和运行npm包，而无需将其实际安装到计算机上。 这是管理发布者的最简单方法。

>[!NOTE]
> 默认情况下，发布者需要服务器到服务器Oauth流的Adobe I/O凭据。 旧版`jwt-auth`凭据
> > 通过运行`npx @adobe/reactor-releaser@v3.1.3`一直使用到2025年1月1日弃用。 所需的参数
> > `jwt-auth`此处[找到](https://github.com/adobe/reactor-releaser/tree/9ea66aa2c683fe7da0cca50ff5c9b9372f183bb5)版本以运行。

发行商仅要求您输入几条信息。 可以从Adobe I/O控制台检索`clientId`和`clientSecret`。 导航到I/O控制台中的[集成页面](https://console.adobe.io/integrations)。 从下拉列表中选择正确的组织，找到正确的集成，然后选择&#x200B;**[!UICONTROL View]**。

- 您的`clientId`是什么？ 请从I/O控制台复制并粘贴此项。
- 您的`clientSecret`是什么？ 请从I/O控制台复制并粘贴此项。

发布者将从扩展清单中读取`name`和`platform`字段，并在Development Availability中查询API以查找匹配的扩展包。
然后，发布者将要求您确认它是否找到了要发布到私密可用环境的正确扩展包。

如果您希望直接使用API以私密方式发布扩展，请参阅API文档中[私密发布扩展包](/help/tags/api/endpoints/extension-packages.md#private-release)的示例调用，以获取更多详细信息。

## 公开发布

完成私密发布后，您可以请求 Adobe 公开发布扩展。这会使您的扩展出现在Public目录中。 任何数据收集用户都可以将您的扩展安装到任何资产。

请填写[公开发布申请表单](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest)，以开始完成发布流程。
