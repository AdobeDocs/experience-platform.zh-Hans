---
title: 配置设置概述
description: 了解配置Web SDK标记扩展时可用的选项。
source-git-commit: 5f0203cfff3cb5c8b892142ff9b1c121925c3c46
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# 配置设置概述

Adobe Experience Platform Web SDK标记扩展提供了多个可自定义的选项。 这些配置设置等效于使用JavaScript库中的[`configure`](/help/collection/js/commands/configure/overview.md)命令。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Extensions]**，然后在&#x200B;**[!UICONTROL Configure]**&#x200B;信息卡上选择[!UICONTROL Adobe Experience Platform Web SDK]。

## 自定义生成组件

如果优化内部版本大小是贵组织的优先事项，则可以禁用不用于减小扩展内部版本大小的特定功能。 有关详细信息，请参阅[自定义生成组件](custom-build-components.md)。

## SDK实例

大多数实施通常需要单个SDK实例。 但是，如果贵组织需要多个Web SDK跟踪实例，则可以使用&#x200B;**[!UICONTROL Add instance]**&#x200B;按钮。 配置每个Web SDK标记实例时，可以使用以下总体部分：

* [**[!UICONTROL SDK instance]**](general.md)：实例的常规设置。 此部分中的所有字段都是必填字段。
* [**[!UICONTROL Datastreams]**](datastreams.md)：您希望每个标记环境的数据传送到的位置。
* [**[!UICONTROL Consent]**](consent.md)：扩展的默认同意设置。
* [**[!UICONTROL Identity]**](identity.md)： Cookie和访客迁移设置。
* [**[!UICONTROL Personalization]**](personalization.md)：自定义单个级别的访客体验。
* [**[!UICONTROL Data collection]**](data-collection.md)：包含或忽略自动收集的内容。
* [**[!UICONTROL Streaming media]**](streaming-media.md)：特定于流媒体收藏集的设置。
* [**[!UICONTROL Datastream configuration overrides]**](configuration-overrides.md)：满足某些条件时修改配置设置。
* [**[!UICONTROL Advanced settings]**](advanced-settings.md)：指定Edge Network的基本路径。
