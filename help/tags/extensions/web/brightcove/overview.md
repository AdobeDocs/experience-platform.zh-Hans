---
title: BrightCove视频跟踪扩展概述
description: 了解Adobe Experience Platform中的BrightCove视频跟踪标记扩展。
exl-id: d27eff21-2abf-4495-8382-08cab32742e0
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 37%

---

# BrightCove视频跟踪扩展概述

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

## 先决条件

Adobe Experience Platform中的每个标记属性都需要在“扩展”屏幕中安装和配置以下扩展：

* Adobe Analytics
* Experience Cloud 访客 ID 服务
* 已安装的核心扩展

在要呈现视频播放器的每个网页的HTML中，使用“页面内嵌入代码（高级）”代码片段。 可以在 [Brightcove文档](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage). 以下链接提供了有关 [如何为预览和发布的视频播放器生成嵌入代码](https://studio.support.brightcove.com/players/generating-player-embed-code.html).

此扩展版本1.1.0支持在单个网页上嵌入多个BrightCove视频。 如果存在多个 `id` 属性，请确保它们各自具有唯一值。 例如， `player1`, `player2`，等等。

>[!NOTE]
>
>在具有多个视频的页面上，每个视频使用在该页面上执行的标记规则中设置的相同配置。 例如，如果创建的规则规定在视频播放完 50% 时触发某个事件，则页面上的每个视频都将在 50% 提示点触发该规则。

如果使用此扩展的网页在相关脚本完全加载之前与视频交互，则可以采取两个操作来解决此问题。 首先可以同步加载标签库，其次，将标签库 `<script type="text/javascript">\_satellite.pageBottom();\</script\>` 元素。

请参阅 [BrightCove API文档](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer) 有关此扩展中使用的组件方法和事件的更多信息。

## 数据元素

该扩展中有七个可用的数据元素，这些数据元素都不需要进行配置。

* **播放头位置：** 当在标记规则中调用此数据元素时，它会以秒为单位记录播放头在视频时间轴上的位置。
* **视频帐户 ID：**&#x200B;此数据元素记录发布视频的 BrightCove 帐户 ID。
* **视频持续时间：**&#x200B;此数据元素记录视频内容的总持续时间（以秒为单位）。此外，可在 Analytics 内创建一个计算量度，将以秒为单位的数字转换为以分钟或小时为单位。
* **视频广告支持：** 此数据元素指定视频中是否支持广告。
* **视频 ID：**&#x200B;此数据元素指定与视频关联的 BrightCove ID。
* **视频名称：**&#x200B;此数据元素指定视频的描述性或友好名称。
* **视频标记：** 此数据元素指定与视频关联的特定脚本。

## 事件

扩展中有七个可用事件，只有“自定义提示点跟踪”需要配置。

* **自定义提示点跟踪：**&#x200B;当视频达到指定的视频阈值百分比时，将触发此事件。例如，如果视频的长度为60秒，而指定的提示点为50%，则事件将在30秒标记处触发。

>[!NOTE]
>
>请注意，每次达到此提示点时，都会触发此事件。例如，如果用户达到 50% 标记，在 50% 标记之前搜索视频，然后再次达到 50% 标记，则触发器将再次触发。

* **视频已完成：** 当视频播放完时，将触发此事件。
* **视频加载的元数据：** 当播放器收到初始持续时间和维度信息时，将触发此事件。
* **视频暂停：**&#x200B;当视频暂停时，将触发此事件。
* **视频恢复：**&#x200B;在暂停事件后恢复视频内容时，将触发此事件。
* **视频屏幕更改：** 当视频切换到全屏模式或从全屏模式切换到其他模式时，将触发该事件。
* **视频开始：**&#x200B;当视频内容首次启动时，将触发此事件。

## 使用情况

可以为每个视频事件（上面列出的七个事件）设置一个标记规则。 为要跟踪的每个事件创建特定的标记规则。 如果不想跟踪事件，则只需省略以为其创建规则。

规则包含三个操作：

1. 设置 Adobe Analytics 变量。（为上面列出的所有或部分数据元素创建数据元素。）
1. 发送 Adobe Analytics 信标。
1. 清除 Adobe Analytics 变量。

## “视频开始”的标记规则示例

将包含以下视频扩展对象：

* **事件**

   1. “视频开始”：此事件将在访客开始播放 BrightCove 视频时触发规则。

* **条件**

   1. None

* **操作**

   1. 在 Analytics“设置变量”操作中，设置：

      * **视频开始**&#x200B;事件（示例：event17）
      * 的prop/eVar **视频名称** 数据元素(示例：eVar10)
      * 的prop/eVar **视频持续时间** 数据元素(示例：eVar11)
      * 的prop/eVar **当前视频位置** 数据元素(示例：eVar12)
   1. Analytics“发送信标”操作 (`s.tl`)
   1. Analytics“清除变量”操作


>[!TIP]
>
>对于那些可能不希望为每个视频元素配置多个eVar或prop的用户，数据元素值会连接为替代方法。 接下来，使用分类规则生成器工具将它们解析到分类报表中。 请参阅 [分类规则生成器工具](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html) 文档以了解更多信息。 最后，它们将作为区段在Analysis Workspace中应用。
>
>为此，请创建一个名为类似“Video MetaData”的新数据元素，然后对其进行编程以提取所有视频数据元素（上面列出），并将它们连接在一起。

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
