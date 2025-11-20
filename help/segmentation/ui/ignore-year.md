---
solution: Experience Platform
title: Ignore Year Time Constraint Update
description: Learn how to resolve an issue with the ignore year time constraint.
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
>You can only use the &quot;ignore year&quot; time constraint in a segment definition evaluated using **batch segmentation**. Adding the &quot;ignore year&quot; time constraint to your segment definition will make the resulting audience **ineligible** for streaming or edge segmentation.

The February 2024 release for Adobe Experience Platform has introduced changes to Adobe Experience Platform Segmentation Service which resolves an issue with the &quot;ignore year&quot; option in audience creation and evaluation.

The &quot;ignore year&quot; option is designed to disregard the year component of a date when performing audience evaluations. You can use this option in situations where the temporal relationship between different events is important but the specific year is unimportant, such as a birth date field.

However, during leap years such as 2024, the underlying system failed to properly handle this option, resulting in inaccurate audience evaluations. As a result if &quot;ignore year&quot; is enabled in a leap year, the audience evaluation would miss one day.

If you created an audience before this fix was released, you just need to re-save the audience in the Segment Builder in order to apply the fix. If you&#39;re unsure if your audience is affected by this resolution, the Segment Builder will prompt the user if the existing audience is affected by this issue.
