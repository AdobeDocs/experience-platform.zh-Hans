---
title: Google Ads增强型转化扩展
description: 了解Adobe Experience Platform中用于事件转发的Google Ads增强型转化扩展。
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 1%

---

# [!DNL Google Ads] 增强的转化扩展

使用 [!DNL Google Ads] API，您可以利用 [增强型转化](https://support.google.com/google-ads/answer/9888656) 以转换调整的形式发送第一方客户数据。 Google使用这些附加数据来改进由广告交互驱动的在线转化报表。

此 [[!DNL Google Ads] 增强的转化事件转发扩展](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (在此称为 [!DNL Enhanced Conversions] extension)提供了一个用户友好的模板，可轻松实现的增强型转化 [!DNL Google Ads] API。

>[!IMPORTANT]
>
>增强型转化仅适用于存在客户数据的转化类型，例如订阅、注册和购买。 以下一段或多段客户数据必须可用，因为符合以下要求时 [配置转换操作](#conversion-action-event-forwarding) 对于事件转发规则：
>
>* 电子邮件地址（首选）
>* 名称和家庭地址（街道地址、城市、州/地区和邮政编码）
>* 电话号码（除了上面另外两个信息之一外，还必须提供）


## 实施概述

增强的转化利用 [!DNL Google Ads] 用于将第一方数据添加到在客户端设备（通常是网站）上发生的转换的API。 这意味着需要执行两个步骤来增强转化：

1. 从客户端发送转换。
1. 使用事件转发来发送其他第一方数据，以增强从客户端发送的转换数据。

>[!TIP]
>
>要将客户端转换事件与从事件转发发送的第一方数据关联，请 `transaction_ID` 两次调用中必须相同。 有关必须在何处为每个服务提供此值的更多信息，请参阅有关配置转换操作的部分 [标记](#conversion-action-tags) 和 [事件转发](#conversion-action-event-forwarding)，则不会显示任何内容。

由于发送转换事件涉及客户端和服务器端实施，因此本文档介绍了设置客户端的先决条件步骤 [[!DNL Google Global Site Tag] (gtag)扩展](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) 除了 [!DNL Enhanced Conversions] 用于事件转发的扩展。

以下视频介绍了 [!DNL Enhanced Conversions] 扩展并大致介绍实施步骤：

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## 使用标记发送转化

要从网站上发送转化事件，请执行以下操作： [!DNL Google Global Site Tag] (gtag)必须部署。 您可以通过配置和安装 [!DNL Google Global Site Tag] (gtag)扩展。

### 配置并安装 [!DNL Google Global Site Tag] 扩展

导航到 [!UICONTROL 数据收集] UI或Experience PlatformUI并选择 **[!UICONTROL 标记]** 左侧导航栏中。 选择要在其上安装扩展的标记属性，然后选择 **[!UICONTROL 扩展]** 左侧导航栏中。 在 **[!UICONTROL 目录]** 选项卡，找到 [!UICONTROL Google全局站点标记(gtag)] 扩展并选择 **[!UICONTROL 安装]**.

![此 [!UICONTROL Google全局站点标记(gtag)] 扩展被选择在 [!UICONTROL 扩展] 在中查看 [!UICONTROL 数据收集] UI。](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

此时将显示安装对话框。 从此处选择 **[!UICONTROL 添加帐户]** 并在出现提示时提供以下值：

| 帐户属性 | 描述 |
| --- | --- |
| 帐户名称 | 帐户的唯一名称。 此名称仅在标记UI中使用。 |
| 帐户 ID | 您的 [!DNL Google Ads] 帐户ID。 要查找此值，请登录 [!DNL Google Ads] 并导航到： **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. 帐户ID字符串可在以开头的代码片段窗口中找到 `AW-` 或 `d`. |
| 产品 | 选择 **[!UICONTROL Google Ads (AdWords)]**. |

{style="table-layout:auto"}

完成后，选择 **[!UICONTROL 添加帐户]**，然后选择 **[!UICONTROL 保存]**.

### 添加发送转换操作 {#conversion-action-tags}

安装扩展后，您可以开始将转化操作包含在标记规则中。 创建或编辑监听要增强的转化的规则时，选择 **[!UICONTROL 添加]** 下 [!UICONTROL 操作]. 在下一个对话框中，选择 **[!UICONTROL Google全局站点标记(gtag)]** 从 [!UICONTROL 扩展] 下拉列表，然后选择 **[!UICONTROL 发送事件]** 下 [!UICONTROL 操作类型].

![此 [!UICONTROL 发送事件] 在规则编辑工作流的操作配置视图中选择的操作类型。](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

显示的其他控件允许您配置 [!DNL gtag] 事件。 至少必须填写以下字段：

1. **[!UICONTROL 事件名称（操作）]**：输入 `conversion` 作为值。
1. 添加键为的新字段 `transaction_id` 其值是 [数据元素](../../../ui/managing-resources/data-elements.md) 包含 [交易ID](https://support.google.com/google-ads/answer/6386790) 值。
1. **[!UICONTROL 转化标签]**：输入适当的转化标签，该标签来自 [!DNL Google Ads] 帐户。 要查找此值，请登录Google Ads并导航到 **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. 转化标签位于 [!DNL Instructions].
   >[!IMPORTANT]
   >
   >当您处于的标记设置区域时 [!DNL Google Ads] 帐户，确保已启用增强型转化。 为此，请查看并接受服务条款，然后选择 **[!DNL Turn on enhanced conversions]** 和 **[!DNL API]** 作为实施方法。

配置操作后，选择 **[!UICONTROL 保留更改]** 以将操作添加到规则配置。 如果对规则满意，请选择 **[!UICONTROL 保存到库]**.

最后，发布新的 [生成](../../../ui/publishing/builds.md) 以启用对库的更改。

## 使用事件转发发送第一方数据

一旦能够从客户端发送转化事件，您就可以使用 [!DNL Enhanced Conversions] 事件转发扩展。

### 创建Google OAuth 2密码和数据元素 {#create-secret-data-element}

在配置扩展之前，必须在事件转发中创建访问令牌以对其进行身份验证 [!DNL Google Ads] API。

请参阅指南，网址为 [创建事件转发密钥](../../../ui/event-forwarding/secrets.md) 以了解详细步骤。 确保选择 **[!UICONTROL Google OAuth 2]** 作为机密类型。 继续按照提示操作，并在系统要求您选择Google帐户配置文件时，选择有权访问您配置的转换操作的帐户。

一旦密码被创建， [创建新数据元素](../../../ui/managing-resources/data-elements.md#create-a-data-element) 并选择 **[!UICONTROL 密码]** （数据元素类型）。 为每个环境选择相应的Google OAuth 2密码，然后选择 **[!UICONTROL 保存到库]**.

### 配置并安装 [!DNL Enhanced Conversions] 扩展 {#install-enhanced-conversions}

查找 [!UICONTROL Google Ads增强型转化] 扩展并选择 **[!UICONTROL 安装]**.

![此 [!UICONTROL Google Ads增强型转化] 扩展被选择在 [!UICONTROL 扩展] 在中查看 [!UICONTROL 数据收集] UI。](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

要配置该扩展，必须填充两个必填字段：

1. **[!UICONTROL 客户ID]**：唯一标识 [!DNL Google Ads] 帐户。 要查找此值，请登录 [!DNL Google Ads] 并导航到 **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL 访问令牌数据元素]**：选择数据元素图标(![数据元素图标](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png))，然后选择您指定的Google OAuth 2机密数据元素 [在上一步中配置](#create-secret-data-element) 从菜单中。

完成后，选择 **[!UICONTROL 保存]** 以安装扩展。

### 添加 [!UICONTROL 发送转换] 针对规则的操作 {#conversion-action-event-forwarding}

安装扩展后，您可以开始包含 [!UICONTROL 发送转换] 事件转发规则中的操作。 创建或编辑监听要增强的转化的规则时，选择 **[!UICONTROL 添加]** 下 [!UICONTROL 操作]. 在下一个对话框中，选择 **[!UICONTROL Google Ads增强型转化]** 从 [!UICONTROL 扩展] 下拉列表，然后选择 **[!UICONTROL 发送转换]** 下 [!UICONTROL 操作类型].

![此 [!UICONTROL 发送转换] 在规则编辑工作流的操作配置视图中选择的操作类型。](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

右侧面板中将显示新控件，允许您配置转换。 至少必须填写以下字段：

**转化信息**

| 输入 | 描述 |
| --- | --- |
| 客户 ID | 您的 [!DNL Google Ads] 客户ID。 默认使用您在以下情况下输入的客户ID： [安装扩展](#install-enhanced-conversions). |
| 转换ID或转换标签 | 跟踪值获取自 [!DNL Google Ads] 设置转化跟踪时。 值开头为 `AW-`.<br><br>有关如何查找这些值的详细信息，请参阅 [[!DNL Google Ads] 文档](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| Transaction ID | 选择具有相同交易ID值的数据元素，即 [从客户端发送](#conversion-action-tags) 使用 [!DNL Google Global Site Tag] 扩展。 |

**用户标识**

* 必须至少包含三个用户标识符中的一个：
   * 电子邮件
   * 电话号码
   * 完整地址

>[!TIP]
>
>在将用户标识数据发送到Google之前，必须对数据进行哈希处理。 如果在事件转发收到数据时未对其进行哈希处理，请选择 **[!UICONTROL 规范化和哈希]** 打开给定字段以指示扩展对值进行哈希处理。
>
>![此 [!UICONTROL 规范化和哈希] 已为以下项启用切换 [!UICONTROL 电子邮件] 内的输入 [!UICONTROL 发送转换] 操作配置表单。](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

完成后，选择 **[!UICONTROL 保留更改]** 以将操作添加到规则配置。 如果对规则满意，请选择 **[!UICONTROL 保存到库]**.

最后，发布新的事件转发 [生成](../../../ui/publishing/builds.md) 以启用对库的更改。

## 后续步骤

本指南介绍了如何将转化事件发送到 [!DNL Google Ads] 使用 [!DNL Enhanced Conversions] 事件转发扩展。 有关Experience Platform中事件转发功能的详细信息，请参阅 [事件转发概述](../../../ui/event-forwarding/overview.md).
