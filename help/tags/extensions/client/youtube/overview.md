---
title: YouTube视频跟踪扩展概述
description: 了解Adobe Experience Platform中的YouTube视频跟踪标记扩展。
exl-id: 703f7b04-f72f-415f-80d6-45583fa661bc
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 32%

---

# YouTube视频跟踪扩展概述

**先决条件**

Adobe Experience Platform中的每个标记属性都要求从“扩展”屏幕安装和配置以下扩展：

* Adobe Analytics
* Experience Cloud 访客 ID 服务
* 核心扩展

在要呈现视频播放器的每个网页的HTML中，使用Google开发人员文档中的[“使用\&lt;iframe\>标记嵌入播放器”](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds)代码段。

此扩展版本2.0.1支持在单个Web页面上嵌入一个或多个YouTube视频，方法是在iframe脚本标记中插入具有唯一值的`id`属性，并将`enablejsapi=1`和`rel=0`附加到`src`属性值的末尾（如果尚未包含）。 例如：

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

此扩展还设计为动态检查唯一ID属性值，如`player1`，而不管`enablejsapi`和`rel`查询字符串参数是否存在，以及它们的预期值是否正确。 因此，可以将YouTube脚本标记添加到具有`id`属性或不具有`enablejsapi`和`rel`查询字符串参数的网页。

>[!NOTE]
>
>在具有多个视频的页面上，每个视频使用在该页面上执行的标记规则中设置的相同配置。 例如，如果创建的规则规定在视频播放完 50% 时触发某个事件，则页面上的每个视频都将在 50% 提示点触发该规则。

扩展依赖以下逻辑来重写iFrame：

```javascript
document.onreadystatechange = function () {
 if (document.readyState === 'complete') {
```

因此，页面加载后会出现轻微闪烁。 此行为是符合预期的。

## 数据元素

该扩展中有六个可用的数据元素，这些数据元素都不需要进行配置。

* **播放头位置：**&#x200B;当在标记规则中调用播放头位置时，会以秒为单位记录播放头在视频时间轴上的位置。
* **视频 ID：**&#x200B;指定与视频关联的 YouTube ID。
* **视频名称：**&#x200B;指定视频的描述性或友好名称。
* **视频 URL：**&#x200B;返回当前已加载/正在播放视频的 YouTube.com URL。
* **视频持续时间：**&#x200B;记录视频内容的总持续时间（以秒为单位）。
* **扩展版本：**&#x200B;此数据元素记录YouTube跟踪扩展版本，例如“Video Tracking_YouTube_2.0.0”。

## 事件

扩展中有八个可用事件，只有“自定义提示点跟踪”需要配置。

* **视频就绪：**&#x200B;提示并准备播放视频时触发。
* **视频开始：**&#x200B;视频首次开始播放，并且 `player.getCurrentTime() === 0` 时触发。
* **视频重播：**&#x200B;提示并在初始开始后重播视频时触发。此触发器将在每次重播视频时触发。
* **视频暂停：**&#x200B;视频暂停时触发。
* **视频恢复：**&#x200B;视频恢复，并且 `player.getCurrentTime() !== 0` 时触发。
* **自定义提示跟踪：**&#x200B;当视频达到指定的视频阈值百分比时触发。 例如，如果视频时长为60秒，而指定的提示点为50%，则播放头位置等于30秒时将触发该事件。 提示点跟踪适用于初次播放和重播。请注意，如果用户试图越过提示点，则不会触发事件。 只有在播放头穿过时间轴上计算的提示点位置，并且视频播放器正在播放时，才会触发提示点事件。
* **视频缓冲：**&#x200B;当播放器在开始播放视频之前下载一定数量的数据时触发。
* **视频结束：**&#x200B;视频完全结束时触发。

## 使用情况

可以为每个视频事件（上面列出的七个事件）设置一个标记规则。 为要跟踪的每个事件创建特定的标记规则。 如果您不想跟踪事件，只需忽略以为其创建规则即可。

规则包含三个操作：

* **设置变量：**&#x200B;设置 Adobe Analytics 变量（映射到所有或部分包含的数据元素）。
* **发送信标：**&#x200B;作为自定义链接跟踪调用发送Adobe Analytics信标，并提供“链接名称”值。
* **清除变量：**&#x200B;清除 Adobe Analytics 变量。

## “视频开始”的标记规则示例

将包括以下视频扩展对象。

* **事件**：“视频开始”(此事件将在访客开始播放YouTube视频时触发规则。)

* **条件**：无

* **操作**：使用&#x200B;**Analytics扩展**&#x200B;进行“设置变量”操作，以映射：

   * “视频开始”事件，
   * 视频持续时间数据元素的 prop/eVar
   * 视频 ID 数据元素的 prop/eVar
   * 视频名称数据元素的 prop/eVar
   * 视频 URL 数据元素的 prop/eVar

  然后，包括链接名称为“视频开始”的“发送信标”操作(`s.tl`)，最后是“清除变量”操作。

>[!TIP]
> 
>对于无法对每个视频元素使用多个eVar或prop的实施，可在Experience Platform中连接数据元素值，使用分类规则生成器工具解析为分类报表(如[https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html)中所述)，然后在Analysis Workspace中作为区段应用。

要连接视频信息值，请创建一个名为“视频Meta数据”的新数据元素，然后对其进行编程以拉入所有视频数据元素（上面所列）并将它们组合在一起。 例如：

```javascript
var r = [];

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));
r.push(_satellite.getVar('Extension Version'));

return r.join('|');
```

有关如何在Experience Platform中有效创建和使用数据元素的更多信息，请阅读[数据元素](../../../ui/managing-resources/data-elements.md)文档。
