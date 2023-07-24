---
title: 使用Adobe Experience Platform Web SDK处理客户同意数据
description: 了解如何在Adobe Experience Platform中集成Adobe Experience Platform Web SDK以处理客户同意数据。
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 1%

---

# 集成Platform Web SDK以处理客户同意数据

Adobe Experience Platform Web SDK允许您检索同意管理平台(CMP)生成的客户同意信号，并在发生同意更改事件时将其发送到Adobe Experience Platform。

**SDK不会与任何开箱即用的CMP接口**. 您可以自行决定如何将SDK集成到您的网站中，监听CMP中的同意更改，并调用相应的命令。 本文档提供了有关如何将CMP与Platform Web SDK集成的一般指导。

## 先决条件 {#prerequisites}

本教程假定您已经确定了如何在CMP中生成同意数据，并创建了一个数据集，其中包含符合Adobe标准或IAB透明度和同意框架(TCF) 2.0标准的同意字段。 如果尚未创建此数据集，请在返回本指南之前参阅以下教程：

* [使用Adobe标准创建数据集](./adobe/dataset.md)
* [使用TCF 2.0标准创建数据集](./iab/dataset.md)

本指南遵循使用UI中的标记扩展设置SDK的工作流。 如果您不想使用扩展，并且希望直接在您的网站上嵌入SDK的独立版本，请参阅以下文档而不是本指南：

* [配置数据流](../../../datastreams/overview.md)
* [安装SDK](../../../edge/fundamentals/installing-the-sdk.md)
* [为同意命令配置SDK](../../../edge/consent/supporting-consent.md)

本指南中的安装步骤需要实际了解标记扩展及其在Web应用程序中的安装方式。 有关更多信息，请参阅以下文档：

* [标记概述](../../../tags/home.md)
* [快速入门指南](../../../tags/quick-start/quick-start.md)
* [发布概述](../../../tags/ui/publishing/overview.md)

## 设置数据流

为了使SDK将数据发送到Experience Platform，您必须首先配置数据流。 在数据收集UI或Experience PlatformUI中，选择 **[!UICONTROL 数据流]** 左侧导航栏中。

创建新数据流或选择要编辑的现有数据流后，选择旁边的切换按钮 **[!UICONTROL Adobe Experience Platform]**. 接下来，使用下面列出的值完成表单。

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| 数据流字段 | 值 |
| --- | --- |
| [!UICONTROL 沙盒] | 平台的名称 [沙盒](../../../sandboxes/home.md) 包含设置数据流所需的流连接和数据集。 |
| [!UICONTROL 事件数据集] | An [!DNL XDM ExperienceEvent] 您计划使用SDK将事件数据发送到的数据集。 虽然您需要提供事件数据集才能创建Platform数据流，但请注意，下游实施工作流中不遵循通过事件发送的同意数据。 |
| [!UICONTROL 配置文件数据集] | 此 [!DNL Profile] — 启用的数据集包含您创建的客户同意字段 [更早](#prerequisites). |

完成后，选择 **[!UICONTROL 保存]** 继续按照任何其他提示完成配置。

## 安装和配置平台Web SDK

创建数据流（如上一节所述）后，必须配置最终将在网站上部署的Platform Web SDK扩展。 如果您的标记资产上未安装SDK扩展，请选择 **[!UICONTROL 扩展]** 在左侧导航中，其后是 **[!UICONTROL 目录]** 选项卡。 然后，选择 **[!UICONTROL 安装]** 在可用扩展列表中的Platform SDK扩展下。

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

配置SDK时，位于 **[!UICONTROL Edge配置]**&#x200B;中，选择您在上一步中创建的数据流。

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

选择 **[!UICONTROL 保存]** 以安装扩展。

### 创建数据元素以设置默认同意

安装SDK扩展后，您可以选择创建一个数据元素来表示默认的数据收集同意值(`collect.val`)。 如果您希望根据用户的不同使用不同的默认值，例如 `pending` 适用于欧盟用户和 `in` 北美用户。

在此使用案例中，您可以实施以下内容以根据用户所在的地区设置默认同意：

1. 确定Web服务器上的用户区域。
1. 早于 `script` 标记（嵌入代码）时，呈现单独的 `script` 标记设置 `adobeDefaultConsent` 变量相同的过期时间。
1. 设置数据元素，该数据元素使用 `adobeDefaultConsent` 变量，并使用此数据元素作为用户的默认同意值。

如果用户的区域由CMP确定，则可以改用以下步骤：

1. 处理页面上的“CMP loaded”事件。
1. 在事件处理程序中，设置 `adobeDefaultConsent` 变量，然后使用JavaScript加载标记库脚本。
1. 设置数据元素，该数据元素使用 `adobeDefaultConsent` 变量，并使用此数据元素作为用户的默认同意值。

要在UI中创建数据元素，请选择 **[!UICONTROL 数据元素]** 在左侧导航中，然后选择 **[!UICONTROL 添加数据元素]** 导航到数据元素创建对话框。

从此处，您必须创建 [!UICONTROL JavaScript变量] 数据元素基于 `adobeDefaultConsent`. 选择 **[!UICONTROL 保存]** 完成后。

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

创建数据元素后，导航回Web SDK扩展配置页面。 在 [!UICONTROL 隐私] 部分，选择 **[!UICONTROL 由数据元素提供]**，并使用提供的对话框选择您之前创建的默认同意数据元素。

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### 在您的网站上部署该扩展

配置完该扩展后，可以将其集成到您的网站中。 请参阅 [发布指南](../../../tags/ui/publishing/overview.md) 标记文档中的库，了解有关如何部署已更新的库内部版本的详细信息。

## 发出consent-change命令 {#commands}

将SDK扩展集成到网站中后，您就可以开始使用Platform Web SDK `setConsent` 命令以将同意数据发送到Platform。

此 `setConsent` 命令执行两个操作：

1. 直接在配置文件存储区中更新用户的配置文件属性。 这不会向数据湖发送任何数据。
1. 创建 [体验事件](../../../xdm/classes/experienceevent.md) 记录带有时间戳的同意更改事件帐户。 此数据将直接发送到数据湖，并可用于跟踪同意首选项随时间发生的变化。

### 何时调用 `setConsent`

在以下两种情况下 `setConsent` 应在您的网站上调用：

1. 在页面上加载同意时（换句话说，在每个页面加载时）
1. 作为CMP挂接或事件侦听器的一部分，可检测同意设置中的更改

### `setConsent` 语法

>[!NOTE]
>
>有关Platform SDK命令的常用语法的介绍，请参阅以下文档： [执行命令](../../../edge/fundamentals/executing-commands.md).

此 `setConsent` 命令需要两个参数：

1. 指示命令类型的字符串(在本例中， `"setConsent"`)
1. 包含单个数组类型属性的有效负荷对象： `consent`. 此 `consent` 数组必须至少包含一个对象，该对象为Adobe标准提供所需的同意字段。

以下示例显示了Adobe标准所需的同意字段 `setConsent` 调用：

```js
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: {
        val: "y"
      },
      share: {
        val: "y"
      },
      personalize: {
        content: {
          val: "y"
        }
      },
      metadata: {
        time: "2020-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| 有效负载属性 | 描述 |
| --- | --- |
| `standard` | 使用的同意标准。 对于Adobe标准，该值必须设置为 `Adobe`. |
| `version` | 下所示的同意标准的版本号 `standard`. 此值必须设置为 `2.0` 用于Adobe标准同意处理。 |
| `value` | 客户的更新同意信息，作为XDM对象提供，符合启用配置文件的数据集同意字段的结构。 |

>[!NOTE]
>
>如果您要将其他同意标准与 `Adobe` (例如 `IAB TCF`)，您可以将其他对象添加到 `consent` 每个标准的数组。 每个对象必须包含适当的值 `standard`， `version`、和 `value` 他们代表的同意标准。

以下JavaScript提供了一个函数示例，该函数处理网站上的同意首选项更改，可用作事件侦听器或CMP挂接中的回调：

```js
var setConsent = function () {

  // Retrieve the current consent data.
  var categories = getConsentData();

  // If the script is running on a consent change, generate a new timestamp.
  // If the script is running on page load, set the timestamp to when the consent values last changed.
  var now = new Date();
  var collectedAt = consentChanged ? now.toISOString() : categories.collectedAt;

  //  Map the consent values and timestamp to XDM
  var consentXDM = {
    collect: {
      val: categories.collect !== -1 ? "y" : "n"
    },
    personalize: {
      content: {
        val: categories.personalizeContent !== -1 ? "y" : "n"
      }
    },
    share: {
      val: categories.share !== -1 ? "y" : "n"
    },
    metadata: {
      time: collectedAt
    }
  };

  // Pass the XDM object to the Platform Web SDK
  alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: consentXDM
    }]
  });
});
```

## 处理SDK响应

全部 [!DNL Platform SDK] 命令会返回指示调用是成功还是失败的promise。 然后，您可以将这些响应用于其他逻辑，例如向客户显示确认消息。 请参阅以下部分： [处理成功或失败](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) 有关特定示例，请参阅执行SDK命令指南。

一旦您成功完成 `setConsent` 通过SDK进行调用，您可以在Platform UI中使用配置文件查看器，验证数据是否登陆配置文件存储区。 请参阅以下部分： [按身份浏览配置文件](../../../profile/ui/user-guide.md#browse-identity) 了解更多信息。

## 后续步骤

按照本指南，您已将Platform Web SDK扩展配置为将同意数据发送到Experience Platform。 有关测试实施的指导，请参阅要实施的同意标准的文档：

* [Adobe标准](./adobe/overview.md#test)
* [TCF 2.0标准](./iab/overview.md#test)
