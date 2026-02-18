---
solution: Experience Platform
title: 忽略年度时间约束更新
description: 了解如何解决忽略年份时间限制的问题。
hidefromtoc: true
exl-id: 44bb8817-e32d-4806-ad4e-b1840313e768
source-git-commit: c7d71113ddcef6aca8b2637814b46e589a6b7fdf
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 8%

---

# 忽略年份时间限制更新 {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="忽略年份更新"
>abstract="忽略年份时间限制已更新。请重新保存您的受众。"

>[!IMPORTANT]
>
>在使用&#x200B;**批处理分段**&#x200B;评估的区段定义中，只能使用“忽略年份”时间限制。 将“忽略年份”时间限制添加到区段定义将使生成的受众&#x200B;**不符合流式或边缘分段条件**。

Adobe Experience Platform 2024年2月版对Adobe Experience Platform分段服务进行了更改，解决了受众创建和评估中“忽略年份”选项的问题。

“忽略年份”选项旨在执行受众评估时忽略日期的年份组成部分。 在不同事件之间的临时关系重要但特定年份不重要的情况下（例如出生日期字段），可以使用此选项。

但是，在像2024这样的闰年，底层系统未能正确处理此选项，导致受众评估不准确。 因此，如果在闰年启用“忽略年份”，则受众评估将错过一天。

如果在发布此修复之前创建受众，则只需在区段生成器中重新保存受众即可应用此修复。 如果您不确定受众是否受此解决方案的影响，那么如果现有受众受此问题影响，区段生成器将会提示用户。
