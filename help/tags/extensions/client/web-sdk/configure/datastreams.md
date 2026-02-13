---
title: 数据流配置设置
description: 使用Web SDK标记扩展配置数据流以将数据发送到。
exl-id: 2d2504c6-b3f9-4e7b-aff4-a8d8d6c4e3dd
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 1%

---

# 数据流配置设置 {#datastreams}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_datastreams"
>title="数据流"
>abstract="必需。在Edge Network中设置要将数据发送到的数据流。"

此配置部分允许您确定要将数据发送到哪个[数据流](/help/datastreams/overview.md)。 **发送到Edge Network的所有数据都需要数据流ID。**

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Extensions]**，然后在&#x200B;**[!UICONTROL Configure]**&#x200B;信息卡上选择[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下滚动到&#x200B;**[!UICONTROL Datastreams]**&#x200B;部分。

![在标记UI中显示Web SDK标记扩展的数据流设置的图像](../assets/web-sdk-ext-datastreams.png)

选择数据流时，您可以为每个[环境](/help/tags/ui/publishing/environments.md) （[!UICONTROL Development]、[!UICONTROL Staging]和[!UICONTROL Production]）执行此操作。 当您想要分开在开发、暂存和生产环境之间发送的数据时，这些字段很有价值。 它提供了一种方便的工作流，在该工作流中，只要在每个相应的环境中安装正确的标记加载器，您就无需担心将数据发送到错误的数据流。

您可以使用以下方法之一填充数据流ID：

* **[!UICONTROL Choose from list]**：每个环境都包含两个下拉菜单，允许您为所选环境选择沙盒和数据流。 每个下拉菜单中的值取决于您在每个[沙盒](/help/datastreams/overview.md)中配置的[数据流](/help/sandboxes/ui/overview.md)。

* **[!UICONTROL Enter values]**：作为使用下拉菜单选择所需数据流的替代方法，您可以直接手动指定所需的数据流ID。 每个环境都允许您直接输入数据流ID，或使用[数据元素](/help/tags/ui/managing-resources/data-elements.md)填充此字段。
