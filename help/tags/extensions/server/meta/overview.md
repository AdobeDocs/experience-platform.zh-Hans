---
title: 元转化API扩展概述
description: 了解用于Adobe Experience Platform中事件转发的元转化API扩展。
source-git-commit: a47e35a1b8c7ce2b0fa4ffe30fcdc7d22fc0f4c5
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---

# [!DNL Meta Conversions API] 扩展概述

的 [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) 允许您将服务器端营销数据连接到 [!DNL Meta] 技术，以优化广告定位、降低每项操作的成本并衡量结果。 事件与 [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID和的处理方式与客户端事件类似。

使用 [!DNL Meta Conversions API] 扩展，您可以在 [事件转发](../../../ui/event-forwarding/overview.md) 将数据发送到的规则 [!DNL Meta] 从Adobe Experience Platform边缘网络。 本文档介绍如何安装扩展并在事件转发中使用其功能 [规则](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>如果您尝试将事件发送到 [!DNL Meta] 从客户端（而非服务器端），使用 [[!DNL Meta Pixiel] 标记扩展](../../client/meta/overview.md) 中。

## 先决条件

要使用该扩展，您必须访问事件转发，并且拥有 [!DNL Meta] 有权访问的帐户 [!DNL Ad Manager] 和 [!DNL Event Manager]. 具体而言，您必须复制现有 [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (或 [新建 [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) )，以便可以将扩展配置到您的帐户。

## 安装扩展

安装 [!DNL Meta Conversions API] 扩展中，导航到数据收集UI或Experience PlatformUI，然后选择 **[!UICONTROL 事件转发]** 的上界。 从此处，选择要将扩展添加到的资产，或改为创建新资产。

选择或创建所需的资产后，请选择 **[!UICONTROL 扩展]** 在左侧导航中，选择 **[!UICONTROL 目录]** 选项卡。 搜索 [!UICONTROL 元转化API] 卡片，然后选择 **[!UICONTROL 安装]**.

![的 [!UICONTROL 安装] 按钮 [!UICONTROL 元转化API] 扩展。](../../../images/extensions/server/meta/install.png)

在显示的配置视图中，必须提供 [!DNL Pixel] 您之前复制的ID，用于将扩展关联到您的帐户。 您可以将ID直接粘贴到输入中，也可以改用数据元素。

您还需要提供访问令牌才能使用 [!DNL Conversions API] 具体而言。 请参阅 [!DNL Conversions API] 文档 [生成访问令牌](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) 以了解有关如何获取此值的步骤。

完成后，选择 **[!UICONTROL 保存]**

![的 [!DNL Pixel] 作为扩展配置视图中的数据元素提供的ID。](../../../images/extensions/server/meta/configure.png)

扩展已安装，您现在可以在标记规则中使用其功能。

## 配置事件转发规则 {#rule}

开始创建新的事件转发规则，并根据需要配置其条件。 为规则选择操作时，选择 **[!UICONTROL 元转化API扩展]** 对于扩展，选择 **[!UICONTROL 发送转化API事件]** （对于操作类型）。

![的 [!UICONTROL 发送页面查看] 在数据收集UI中为规则选择的操作类型。](../../../images/extensions/server/meta/select-action.png)

此时会显示允许您配置要发送到的事件数据的控件 [!DNL Meta] 通过 [!DNL Conversions API]. 这些选项可以直接输入到提供的输入中，或者您可以选择现有数据元素来表示值。 配置选项分为四个主要部分，如下所述。

| 配置部分 | 描述 |
| --- | --- |
| [!UICONTROL 服务器事件参数] | 有关事件的一般信息，包括事件发生的时间以及触发该事件的源操作。 请参阅 [[!DNL Conversions API] 文档](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) 以了解有关这些参数的详细信息。<br><br>您还可以选择 **[!UICONTROL 启用有限数据使用]** 以帮助遵守客户的选择退出。 请参阅 [!DNL Conversions API] 文档 [数据处理选项](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) 有关此功能的详细信息。 |
| [!UICONTROL 客户信息参数] | 用于将事件归因给客户的用户标识数据。 其中某些值必须先经过哈希处理，然后才能发送到API。 请参阅 [[!DNL Conversions API] 文档](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) 以了解有关这些参数的详细信息。 |
| [!UICONTROL 自定义数据] | 要用于广告投放优化的其他数据，以JSON对象的形式提供。 请参阅 [[!DNL Conversions API] 文档](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) 有关此对象已接受属性的详细信息。<br><br>如果您发送购买事件，则必须使用此部分提供所需的属性 `currency` 和 `value`. |
| [!UICONTROL 测试事件] | 此选项用于验证您的配置是否导致服务器事件被 [!DNL Meta] 如预期。 要使用此功能，请选择 **[!UICONTROL 作为测试事件发送]** 复选框，然后在以下输入中提供您选择的测试事件代码。 部署事件转发规则后，如果正确配置了扩展和操作，则应会在 **[!DNL Test Events]** 查看 [!DNL Meta Events Manager]. |

{style=&quot;table-layout:auto&quot;}

完成后，选择 **[!UICONTROL 保留更改]** 将操作添加到规则配置。

![[!UICONTROL 保留更改] 正在为操作配置选择。](../../../images/extensions/server/meta/keep-changes.png)

如果您对规则满意，请选择 **[!UICONTROL 保存到库]**. 最后，发布新的事件转发 [构建](../../../ui/publishing/builds.md) 以启用对库所做的更改。

## 后续步骤

本指南介绍了如何将服务器端事件数据发送到 [!DNL Meta] 使用 [!DNL Meta Conversions API] 扩展。 有关标记和事件转发的更多信息，请参阅 [标记概述](../../../home.md).
