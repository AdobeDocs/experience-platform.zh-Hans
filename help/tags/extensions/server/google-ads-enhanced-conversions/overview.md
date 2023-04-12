---
title: Google Ads增强转化扩展
description: 了解用于Adobe Experience Platform中事件转发的Google广告增强转化扩展。
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 1%

---

# [!DNL Google Ads] 增强的转化扩展

使用 [!DNL Google Ads] API，您可以利用 [增强转化](https://support.google.com/google-ads/answer/9888656) 以转化调整的形式发送第一方客户数据。 Google使用这些附加数据来改进由广告交互驱动的在线转化报表。

的 [[!DNL Google Ads] 增强的转化事件转发扩展](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (前称 [!DNL Enhanced Conversions] 扩展)提供了一个用户友好的模板，以便轻松地为 [!DNL Google Ads] API。

>[!IMPORTANT]
>
>增强的转化仅适用于存在客户数据的转化类型，例如订阅、注册和购买。 以下一个或多个客户数据必须可用，因为在 [配置转化操作](#conversion-action-event-forwarding) 对于事件转发规则：
>
>* 电子邮件地址（首选）
>* 姓名和住址（街道地址、城市、州/地区和邮政编码）
>* 电话号码（除上述另外两个信息之一外，还必须提供）


## 实施概述

增强的转化利用 [!DNL Google Ads] 用于将第一方数据添加到客户端设备（通常是网站）上发生的转化的API。 这意味着要实施增强的转化，需分两个步骤：

1. 从客户端发送转化。
1. 使用事件转发发送其他第一方数据，以增强从客户端发送的转化数据。

>[!TIP]
>
>要将客户端转化事件与从事件转发发送的第一方数据关联，请 `transaction_ID` 在两个调用中必须相同。 有关必须在何处为每项服务提供此值的更多信息，请参阅有关为 [标记](#conversion-action-tags) 和 [事件转发](#conversion-action-event-forwarding)，分别为。

由于发送转化事件涉及客户端和服务器端实施，因此本文档介绍了设置客户端的先决条件步骤 [[!DNL Google Global Site Tag] (gtag)扩展](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) 除 [!DNL Enhanced Conversions] 用于事件转发的扩展。

以下视频介绍 [!DNL Enhanced Conversions] 扩展和逐步完成高级实施步骤：

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## 使用标记发送转化

要从网站上的发送转化事件， [!DNL Google Global Site Tag] (gtag)。 您可以通过配置和安装 [!DNL Google Global Site Tag] (gtag)扩展。

### 配置和安装 [!DNL Google Global Site Tag] 扩展

导航到 [!UICONTROL 数据收集] UI或Experience PlatformUI，然后选择 **[!UICONTROL 标记]** 中。 选择要在上安装扩展的标记资产，然后选择 **[!UICONTROL 扩展]** 中。 在 **[!UICONTROL 目录]** ，找到 [!UICONTROL Google全局网站标记(gtag)] 扩展和选择 **[!UICONTROL 安装]**.

![的 [!UICONTROL Google全局网站标记(gtag)] 正在下选择的扩展 [!UICONTROL 扩展] 视图 [!UICONTROL 数据收集] UI。](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

出现安装对话框。 从此处选择 **[!UICONTROL 添加帐户]** 和会在出现提示时提供以下值：

| 帐户属性 | 描述 |
| --- | --- |
| 帐户名称 | 帐户的唯一名称。 此名称仅在标记UI中使用。 |
| 帐户 ID | 您的 [!DNL Google Ads] 帐户ID。 要查找此值，请登录 [!DNL Google Ads] 并导航到： **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. 帐户ID字符串可在以开头的代码段窗口中找到 `AW-` 或 `d`. |
| 产品 | 选择 **[!UICONTROL Google Ads(AdWords)]**. |

{style="table-layout:auto"}

完成后，选择 **[!UICONTROL 添加帐户]**，然后选择 **[!UICONTROL 保存]**.

### 添加发送转化操作 {#conversion-action-tags}

安装扩展后，您可以开始在标记规则中包含转化操作。 创建或编辑监听要增强的转化的规则时，请选择 **[!UICONTROL 添加]** 在 [!UICONTROL 操作]. 在下一个对话框中，选择 **[!UICONTROL Google全局网站标记(gtag)]** 从 [!UICONTROL 扩展] 下拉列表，然后选择 **[!UICONTROL 发送事件]** 在 [!UICONTROL 操作类型].

![的 [!UICONTROL 发送事件] 操作类型。](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

此时会显示允许您配置 [!DNL gtag] 事件。 必须至少填写以下字段：

1. **[!UICONTROL 事件名称（操作）]**:输入 `conversion` 作为值。
1. 添加键为 `transaction_id` 值是 [数据元素](../../../ui/managing-resources/data-elements.md) 包含 [交易ID](https://support.google.com/google-ads/answer/6386790) 值。
1. **[!UICONTROL 转化标签]**:从 [!DNL Google Ads] 帐户。 要查找此值，请登录Google Ads，然后导航到 **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. 转换标签位于 [!DNL Instructions].
   >[!IMPORTANT]
   >
   >当您位于 [!DNL Google Ads] 帐户，请确保启用增强的转化。 要执行此操作，请查看并接受服务条款，然后选择 **[!DNL Turn on enhanced conversions]** 和 **[!DNL API]** 作为实现方法。

配置操作后，选择 **[!UICONTROL 保留更改]** 将操作添加到规则配置。 如果您对规则满意，请选择 **[!UICONTROL 保存到库]**.

最后，发布新 [构建](../../../ui/publishing/builds.md) 以启用对库的更改。

## 使用事件转发发送第一方数据

从客户端发送转化事件后，您可以使用 [!DNL Enhanced Conversions] 事件转发扩展。

### 创建Google OAuth 2密钥和数据元素 {#create-secret-data-element}

在配置扩展之前，必须在事件转发中创建访问令牌以验证到 [!DNL Google Ads] API。

请参阅 [创建事件转发密钥](../../../ui/event-forwarding/secrets.md) 以了解详细步骤。 确保您选择 **[!UICONTROL Google OAuth 2]** 作为密钥类型。 继续按照提示操作，当要求选择Google帐户配置文件时，请选择有权访问要配置的转换操作的帐户。

一旦秘密被创造， [创建新数据元素](../../../ui/managing-resources/data-elements.md#create-a-data-element) 选择 **[!UICONTROL 密码]** （对于数据元素类型）。 为每个环境选择相应的Google OAuth 2密钥，然后选择 **[!UICONTROL 保存到库]**.

### 配置和安装 [!DNL Enhanced Conversions] 扩展 {#install-enhanced-conversions}

查找 [!UICONTROL Google Ads增强的转化] 扩展，然后选择 **[!UICONTROL 安装]**.

![的 [!UICONTROL Google Ads增强的转化] 正在下选择的扩展 [!UICONTROL 扩展] 视图 [!UICONTROL 数据收集] UI。](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

要配置扩展，必须填充以下两个必填字段：

1. **[!UICONTROL 客户ID]**:唯一标识您的 [!DNL Google Ads] 帐户。 要查找此值，请登录 [!DNL Google Ads] 并导航到 **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL 访问令牌数据元素]**:选择数据元素图标(![数据元素图标](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png))，然后选择您的Google OAuth 2密钥数据元素 [在上一步中配置](#create-secret-data-element) 中。

完成后，选择 **[!UICONTROL 保存]** 以安装扩展。

### 添加 [!UICONTROL 发送转化] 对规则的操作 {#conversion-action-event-forwarding}

安装扩展后，您可以开始包含 [!UICONTROL 发送转化] 事件转发规则中的操作。 创建或编辑监听要增强的转化的规则时，请选择 **[!UICONTROL 添加]** 在 [!UICONTROL 操作]. 在下一个对话框中，选择 **[!UICONTROL Google Ads增强的转化]** 从 [!UICONTROL 扩展] 下拉列表，然后选择 **[!UICONTROL 发送转化]** 在 [!UICONTROL 操作类型].

![的 [!UICONTROL 发送转化] 操作类型。](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

右侧面板中会显示允许您配置转化的新控件。 必须至少填写以下字段：

**转化信息**

| 输入 | 描述 |
| --- | --- |
| 客户 ID | 您的 [!DNL Google Ads] 客户ID。 默认为您在 [安装扩展](#install-enhanced-conversions). |
| 转化ID或转化标签 | 从获取的跟踪值 [!DNL Google Ads] 设置转化跟踪时。 值以 `AW-`.<br><br>有关如何查找这些值的详细信息，请参阅 [[!DNL Google Ads] 文档](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| Transaction ID | 选择具有与 [从客户端发送](#conversion-action-tags) 使用 [!DNL Google Global Site Tag] 扩展。 |

**用户标识**

* 必须至少包含三个用户标识符之一：
   * 电子邮件
   * 电话号码
   * 完整地址

>[!TIP]
>
>用户标识数据在发送到Google之前必须经过哈希处理。 如果数据在事件转发收到时没有经过哈希处理，请选择 **[!UICONTROL 标准化和哈希]** 打开给定字段，以指示扩展对值进行哈希处理。
>
>![的 [!UICONTROL 标准化和哈希] 为 [!UICONTROL 电子邮件] 输入 [!UICONTROL 发送转化] 操作配置表单。](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

完成后，选择 **[!UICONTROL 保留更改]** 将操作添加到规则配置。 如果您对规则满意，请选择 **[!UICONTROL 保存到库]**.

最后，发布新的事件转发 [构建](../../../ui/publishing/builds.md) 以启用对库的更改。

## 后续步骤

本指南介绍如何将转化事件发送到 [!DNL Google Ads] 使用 [!DNL Enhanced Conversions] 事件转发扩展。 有关Experience Platform中事件转发功能的更多信息，请参阅 [事件转发概述](../../../ui/event-forwarding/overview.md).
