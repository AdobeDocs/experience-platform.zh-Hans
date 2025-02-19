---
title: Google Ads增强型转化扩展
description: 了解Adobe Experience Platform中用于事件转发的Google Ads增强型转化扩展。
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 0d98183838125fac66768b94bc1993bde9a374b5
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 1%

---

# [!DNL Google Ads]增强型转化扩展

使用[!DNL Google Ads] API，您可以通过以转化调整的形式发送第一方客户数据来利用[增强型转化](https://support.google.com/google-ads/answer/9888656)。 Google使用这些附加数据来改进由广告交互驱动的在线转化报表。

[[!DNL Google Ads] Enhanced Conversions事件转发扩展](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions)（以前称为[!DNL Enhanced Conversions]扩展）提供了一个用户友好的模板，可轻松实现[!DNL Google Ads] API的增强转化。

>[!IMPORTANT]
>
>增强型转化仅适用于存在客户数据的转化类型，例如订阅、注册和购买。 以下一段或多段客户数据必须可用，因为在[为事件转发规则配置转换操作](#conversion-action-event-forwarding)时需要这些数据：
>
>* 电子邮件地址（首选）
>* 名称和家庭地址（街道地址、城市、州/地区和邮政编码）
>* 电话号码（除了以上另外两则信息之一外，还必须提供）

## 实施概述

增强型转化利用[!DNL Google Ads] API将第一方数据添加到客户端设备（通常是网站）上发生的转化。 这意味着需要分两步来实施增强的转化：

1. 从客户端发送转换。
1. 使用事件转发来发送其他第一方数据，这会增强从客户端发送的转换数据。

>[!TIP]
>
>要将客户端转化事件与从事件转发发送的第一方数据关联，两个调用中的`transaction_ID`必须相同。 有关必须在何处为每个服务提供此值的更多信息，请分别参阅有关为[标记](#conversion-action-tags)和[事件转发](#conversion-action-event-forwarding)配置转换操作的章节。

由于发送转换事件涉及客户端和服务器端实施，因此，除了用于事件转发的[!DNL Enhanced Conversions]扩展之外，本文档还介绍了设置客户端[[!DNL Google Global Site Tag] (gtag)扩展](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag)的先决步骤。

以下视频介绍了[!DNL Enhanced Conversions]扩展并大致介绍了实施步骤：

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## 使用标记发送转化

若要从网站上发送转化事件，必须部署[!DNL Google Global Site Tag] (gtag)。 您可以通过配置和安装[!DNL Google Global Site Tag] (gtag)扩展来使用标记实现此目标。

### 配置并安装[!DNL Google Global Site Tag]扩展

导航到[!UICONTROL 数据收集]用户界面或Experience Platform用户界面，然后在左侧导航中选择&#x200B;**[!UICONTROL 标记]**。 选择要在其上安装扩展的标记属性，然后在左侧导航中选择&#x200B;**[!UICONTROL 扩展]**。 在&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡下，找到[!UICONTROL Google全局站点标签(gtag)]扩展并选择&#x200B;**[!UICONTROL 安装]**。

![在[!UICONTROL 数据收集] UI中的[!UICONTROL 扩展]视图下选择[!UICONTROL Google全局站点标记(gtag)]扩展。](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

此时将显示安装对话框。 从此处选择&#x200B;**[!UICONTROL 添加帐户]**，并在出现提示时提供以下值：

| 帐户属性 | 描述 |
| --- | --- |
| 帐户名称 | 帐户的唯一名称。 此名称仅在标记UI中使用。 |
| 帐户 ID | 您的[!DNL Google Ads]帐户ID。 要查找此值，请登录[!DNL Google Ads]并导航到： **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**。 帐户ID字符串可在以`AW-`或`d`开头的代码片段窗口中找到。 |
| 产品 | 选择&#x200B;**[!UICONTROL Google广告(AdWords)]**。 |

{style="table-layout:auto"}

完成后，选择&#x200B;**[!UICONTROL 添加帐户]**，然后选择&#x200B;**[!UICONTROL 保存]**。

### 添加发送转换操作 {#conversion-action-tags}

安装该扩展后，您可以开始将转化操作包含在标记规则中。 创建或编辑监听要增强的转化的规则时，在[!UICONTROL 操作]下选择&#x200B;**[!UICONTROL 添加]**。 在下一个对话框中，从[!UICONTROL 扩展]下拉列表中选择&#x200B;**[!UICONTROL Google全局站点标记(gtag)]**，然后在[!UICONTROL 操作类型]下选择&#x200B;**[!UICONTROL 发送事件]**。

![在规则编辑工作流的操作配置视图中选择的[!UICONTROL 发送事件]操作类型。](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

显示的其他控件允许您配置[!DNL gtag]事件。 至少必须填写以下字段：

1. **[!UICONTROL 事件名称（操作）]**：输入`conversion`作为值。
1. 添加键为`transaction_id`且值为包含[交易ID](https://support.google.com/google-ads/answer/6386790)值的[数据元素](../../../ui/managing-resources/data-elements.md)的新字段。
1. **[!UICONTROL 转化标签]**：输入您的[!DNL Google Ads]帐户中相应的转化标签。 要查找此值，请登录Google广告并导航到&#x200B;**[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**。 可以在[!DNL Instructions]下找到转换标签。

   >[!IMPORTANT]
   >
   >当您处于[!DNL Google Ads]帐户的标记设置区域时，请确保已启用增强型转化。 为此，请查看并接受服务条款，然后选择&#x200B;**[!DNL Turn on enhanced conversions]**&#x200B;和&#x200B;**[!DNL API]**&#x200B;作为实施方法。

配置操作后，选择&#x200B;**[!UICONTROL Keep Changes]**&#x200B;以将该操作添加到规则配置。 如果对规则满意，请选择&#x200B;**[!UICONTROL 保存到库]**。

最后，发布新的[内部版本](../../../ui/publishing/builds.md)以启用对库的更改。

## 使用事件转发发送第一方数据

一旦能够从客户端发送转化事件，您就可以使用[!DNL Enhanced Conversions]事件转发扩展来增强这些转化。

### 创建Google OAuth 2密码和数据元素 {#create-secret-data-element}

在配置扩展之前，必须在事件转发中创建访问令牌以向[!DNL Google Ads] API进行身份验证。

有关详细步骤，请参阅[创建事件转发密钥](../../../ui/event-forwarding/secrets.md)指南。 确保选择&#x200B;**[!UICONTROL Google OAuth 2]**&#x200B;作为密钥类型。 继续按照提示操作，并在系统要求您选择Google帐户配置文件时，选择有权访问您配置的转换操作的帐户。

创建密码后，[创建新的数据元素](../../../ui/managing-resources/data-elements.md#create-a-data-element)并为数据元素类型选择&#x200B;**[!UICONTROL 密码]**。 为每个环境选择相应的Google OAuth 2密码，然后选择&#x200B;**[!UICONTROL 保存到库]**。

### 配置并安装[!DNL Enhanced Conversions]扩展 {#install-enhanced-conversions}

在事件转发目录中找到[!UICONTROL Google Ads增强型转化]扩展并选择&#x200B;**[!UICONTROL 安装]**。

![在[!UICONTROL 数据收集] UI的[!UICONTROL 扩展]视图下选择[!UICONTROL Google Ads增强型转化]扩展。](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

要配置扩展，必须填充两个必填字段：

1. **[!UICONTROL 客户ID]**：唯一标识您的[!DNL Google Ads]帐户的ID。 要查找此值，请登录[!DNL Google Ads]并导航到&#x200B;**[!DNL Help]** > **[!DNL Customer ID]**。
2. **[!UICONTROL 访问令牌数据元素]**：选择数据元素图标（![数据元素图标](/help/images/icons/database.png)）并从菜单中选择您[在上一步骤](#create-secret-data-element)中配置的Google OAuth 2机密数据元素。

完成后，选择&#x200B;**[!UICONTROL 保存]**&#x200B;以安装扩展。

### 将[!UICONTROL 发送转换]操作添加到规则 {#conversion-action-event-forwarding}

安装扩展后，您可以开始将[!UICONTROL 发送转换]操作包含在事件转发规则中。 创建或编辑监听要增强的转化的规则时，在[!UICONTROL 操作]下选择&#x200B;**[!UICONTROL 添加]**。 在下一个对话框中，从[!UICONTROL 扩展]下拉列表中选择&#x200B;**[!UICONTROL Google Ads增强型转化]**，然后在[!UICONTROL 操作类型]下选择&#x200B;**[!UICONTROL 发送转化]**。

![在规则编辑工作流的操作配置视图中选择的[!UICONTROL 发送转换]操作类型。](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

新的控件显示在右侧面板中，允许您配置转化。 至少必须填写以下字段：

**转换信息**

| 输入 | 描述 |
| --- | --- |
| 客户ID | 您的[!DNL Google Ads]客户ID。 默认为您在[安装扩展](#install-enhanced-conversions)时输入的客户ID。 |
| 转换ID或转换标签 | 设置转化跟踪时从[!DNL Google Ads]获得的跟踪值。 值以`AW-`开头。<br><br>有关如何查找这些值的详细信息，请参阅[[!DNL Google Ads] 文档](https://support.google.com/tagmanager/answer/6105160?hl=en)。 |
| Transaction ID | 选择与使用[!DNL Google Global Site Tag]扩展从客户端](#conversion-action-tags)发送的交易ID值为[的数据元素。 |

**用户标识**

* 必须至少包括三个用户标识符中的一个：
   * 电子邮件
   * 电话号码
   * 完整地址

>[!TIP]
>
>在将用户标识数据发送到Google之前，必须对其进行哈希处理。 如果在事件转发收到数据时未对其进行哈希处理，请选择给定字段上的&#x200B;**[!UICONTROL 规范化和哈希]**&#x200B;切换开关以指示扩展对该值进行哈希处理。
>
>![已在[!UICONTROL 发送转换]操作配置表单中为[!UICONTROL 电子邮件]输入启用[!UICONTROL 规范化和哈希]切换。](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

完成后，选择&#x200B;**[!UICONTROL Keep Changes]**&#x200B;以将该操作添加到规则配置中。 如果对规则满意，请选择&#x200B;**[!UICONTROL 保存到库]**。

最后，发布新的事件转发[生成](../../../ui/publishing/builds.md)以启用对库的更改。

## 后续步骤

本指南介绍了如何使用[!DNL Enhanced Conversions]事件转发扩展将转化事件发送到[!DNL Google Ads]。 有关Experience Platform中事件转发功能的更多信息，请参阅[事件转发概述](../../../ui/event-forwarding/overview.md)。
