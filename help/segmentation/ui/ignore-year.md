---
solution: Experience Platform
title: 忽略年度时间约束更新
description: 了解如何解决忽略年份时间限制的问题。
source-git-commit: d0bd7990f0d77cd5f8d30da735b89c188e13c780
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# 忽略年份时间限制更新 {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="忽略年度更新"
>abstract="已更新忽略年份时间限制。 请重新保存您的受众。"

Adobe Experience Platform 2024年2月版对Adobe Experience Platform分段服务进行了更改，解决了受众创建和评估中“忽略年份”选项的问题。

“忽略年份”选项旨在执行受众评估时忽略日期的年份组成部分。 在不同事件之间的临时关系重要但特定年份不重要的情况下（例如出生日期字段），可以使用此选项。

但是，在像2024这样的闰年，底层系统未能正确处理此选项，导致受众评估不准确。 因此，如果在闰年启用“忽略年份”，则受众评估将错过一天。

如果在发布此修复之前创建受众，则只需在区段生成器中重新保存受众即可应用此修复。 如果您不确定受众是否受此解决方案的影响，那么如果现有受众受此问题影响，区段生成器将会提示用户。
