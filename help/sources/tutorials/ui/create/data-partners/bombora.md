---
title: 使用UI将Bombora的意图连接到Experience Platform
description: 了解如何将Bombora Intent连接到Experience Platform
hide: true
hidefromtoc: true
exl-id: 76a4fed5-b2d5-46d5-9245-b52792a7d323
source-git-commit: 911aad600dd2618ba98d2ccee737aaedea4f2735
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 36%

---

# 使用UI将[!DNL Bombora Intent]连接到Experience Platform

阅读本指南，了解如何使用用户界面将您的[!DNL Bombora Intent]帐户连接到Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [Real-Time CDP B2B edition](../../../../../rtcdp/b2b-overview.md)： Real-Time CDP B2B edition专为以B2B服务模式运营的营销人员而构建。 它将来自多个来源的数据汇集在一起&#x200B;，并将其组合成人员和帐户轮廓的单一视图。这种统一的数据使营销人员能够精确锁定特定受众，并通过所有可用渠道吸引这些受众。
* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 导航源目录

在Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;*[!UICONTROL B2B]*&#x200B;类别下选择&#x200B;**[!DNL Bombora Intent]**，然后选择&#x200B;**[!UICONTROL 设置]**。

>[!TIP]
>
>当给定的源尚未具有经过身份验证的帐户时，源目录中的源会显示&#x200B;**[!UICONTROL 设置]**&#x200B;选项。 一旦存在经过身份验证的帐户，此选项将更改为&#x200B;**[!UICONTROL 添加数据]**。



## 使用现有帐户 {#existing}

## 创建新帐户 {#create}

## 提供数据流详细信息 {#provide-dataflow-details}

>[!CONTEXTUALHELP]
>id="platform_sources_bombora_domain"
>title="域来源"
>abstract="虽然 Adobe 使用 XDM accountOrganization.website，但可能有些客户会在其各自的网站上使用自定义字段。因此，您必须确保您的域来源是将您的 Bombora 帐户记录与 Experience Platform 帐户匹配的域/网站字段。"

## 计划数据流 {#schedule-dataflow}

>[!CONTEXTUALHELP]
>id="platform_sources_bombora_schedule"
>title="计划您的数据流"
>abstract="Bombora 每周一早上 UTC 时间下午 5:00 投放一次数据。因此，您必须将摄取开始时间配置为 UTC 时间下午 5:00 之后。此外，您必须与 Bombora 确认摄取时间，因为他们可能会在将文件发送到 Adobe 时更改其计划。"


## 查看数据流 {#review-dataflow}
