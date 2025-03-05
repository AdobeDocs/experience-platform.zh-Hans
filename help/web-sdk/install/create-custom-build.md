---
title: 使用NPM包创建自定义Web SDK内部版本
description: 创建一个仅包含所需模块的自定义Web SDK内部版本。
source-git-commit: 0f77023b07102ac2bc812034afacb1522ef209e5
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 6%

---


# 创建自定义Web SDK内部版本

Experience Platform Web SDK库包含多个模块，用于提供各种功能，如个性化、身份识别、链接跟踪等。 根据您的用例，您可能只需要特定功能，而无需整个库。 通过创建自定义Web SDK内部版本，您可以仅选择所需的模块，从而减小库大小并提高性能。

## 用例 {#use-case}

创建自定义Web SDK内部版本有助于减小库大小并提高性能。 以下是一些示例：

### 移除Media Analytics {#media-analytics-removal}

如果您的网站没有媒体内容，则可以从内部版本中排除[!DNL Media Analytics]和[!DNL Streaming Media]模块。 这可以将Web SDK内部版本大小最多减少50%，并提高加载速度。

### Personalization移除 {#personalization}

如果只需要收集用户量度并且不计划使用Adobe Target或Journey Optimizer进行个性化，则可以排除[!DNL Personalization]模块。 这样可减小库大小，同时仍允许您收集必要的量度。

## 先决条件 {#prerequisites}

要创建自定义Web SDK内部版本，您需要Web SDK NPM包。 确保您的计算机上安装了[Node.js](https://nodejs.org/en/download/package-manager/all)。 有关更多详细信息，请参阅有关如何使用NPM包[安装Web SDK](npm.md)的文档。

## 组件和依赖关系 {#components-dependencies}

在创建自定义Web SDK内部版本之前，请定义您计划使用的Web SDK组件和命令。 某些命令取决于内部版本中包含的特定模块。

下表显示了Web SDK模块及其包含的命令之间的关系：

| 模块依赖关系 | 配置参数 | 命令 | 大小类别 |
|---------|----------|---------|---------|
| 活动收集器 | [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) | 不适用 | 媒介 |
| 受众 | 不适用 | 不适用 | 小 |
| 上下文 | [`context`](../commands/configure/context.md) | 不适用 | 小 |
| 规则引擎 | `personalizationStorageEnabled` | | <ul><li>`evaluateRulesets`</li><li>[`subscribeRulesetItems`](../commands/subscriberulesetitems.md)</li></ul> | 媒介 |
| 事件合并 | 不适用 | `createEventMergeId` | 小 |
| Media Analytics Bridge | 不适用 | [`getMediaAnalyticsTracker`](../commands/getmediaanalyticstracker.md) | 大 |
| 个性化 | <ul><li>[`prehidingStyle`](../commands/configure/prehidingstyle.md)</li><li>[`targetMigrationEnabled`](../commands/configure/targetmigrationenabled.md)</li><li>[`autoCollectPropositionInteractions`](../commands/configure/autocollectpropositioninteractions.md)</li></ul> | 不适用 | 大 |
| 同意 | [`defaultConsent`](../commands/configure/defaultconsent.md) | [`setConsent`](../commands/setconsent.md) | 小 |
| 流媒体 | [`streamingMedia`](../commands/configure/streamingmedia.md) | <ul><li>[`createMediaSession`](../commands/createmediasession.md)</li><li>[`sendMediaEvent`](../commands/sendmediaevent.md)</li></ul> | 大 |

## 使用NPM包创建自定义Web SDK内部版本 {#create-custom-build}

1. 打开您的终端并运行`npx @adobe/alloy`。 您需要选择希望自定义内部版本包含的Web SDK组件。

   ![显示自定义生成模块选择的终端图像。](../assets/custom-build/npx.png)

   使用箭头键在模块列表中上下移动。

   * 按&#x200B;**共享空间**&#x200B;启用或禁用所选模块。
   * 按`A`启用或禁用所有模块。
   * 按`I`反转您的选择。
   * 按`Enter`确认您的选择，然后转到下一步。

1. 选择要包含在自定义内部版本中的模块后，您可以选择保存自定义Web SDK库内部版本的缩小版本或未缩小版本。 选择所需的选项，然后按`Enter`。

   ![显示自定义生成精简选择的终端图像。](../assets/custom-build/minify.png)

1. 接下来，将询问您要将内部版本保存在本地计算机上的什么位置。 按`Enter`确认预选位置或输入新位置。

   ![显示自定义生成保存选项的终端图像。](../assets/custom-build/save.png)

1. 确认位置后，将生成并保存您的自定义内部版本。

   ![显示自定义生成保存位置的终端图像。](../assets/custom-build/saved.png)

