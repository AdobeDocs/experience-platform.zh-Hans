---
title: 使用Adobe Experience Platform Web SDK处理客户同意数据
topic-legacy: getting started
description: 了解如何集成Adobe Experience Platform Web SDK以在Adobe Experience Platform中处理客户同意数据。
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: 79bc41c713425e14bb3c12646b9b71b2c630618b
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 0%

---

# 集成Platform Web SDK以处理客户同意数据

利用Adobe Experience Platform Web SDK，可检索由同意管理平台(CMP)生成的客户同意信号，并在发生同意更改事件时将其发送到Adobe Experience Platform。

**SDK不会与任何现成的CMP进行接口**. 至于如何将SDK集成到您的网站，如何监听CMP中的同意更改，以及如何调用相应的命令，这将由您来决定。 本文档提供了有关如何将CMP与Platform Web SDK集成的一般指导。

## 先决条件 {#prerequisites}

本教程假定您已确定如何在CMP中生成同意数据，并已创建一个数据集，其中包含符合Adobe标准或IAB透明度与同意框架(TCF)2.0标准的同意字段。 如果您尚未创建此数据集，请先参阅以下教程，然后再返回到本指南：

* [使用Adobe标准创建数据集](./adobe/dataset.md)
* [使用TCF 2.0标准创建数据集](./iab/dataset.md)

本指南遵循使用数据收集UI中的标记扩展设置SDK的工作流程。 如果您不想使用该扩展，并且希望在网站上直接嵌入SDK的独立版本，请参阅以下文档，而不是本指南：

* [配置数据流](../../../edge/datastreams/overview.md)
* [安装SDK](../../../edge/fundamentals/installing-the-sdk.md)
* [为同意命令配置SDK](../../../edge/consent/supporting-consent.md)

本指南中的安装步骤需要对标记扩展以及它们在Web应用程序中的安装方式有一定的了解。 有关更多信息，请参阅以下文档：

* [标记概述](../../../tags/home.md)
* [快速入门指南](../../../tags/quick-start/quick-start.md)
* [发布概述](../../../tags/ui/publishing/overview.md)

## 设置数据流

为了使SDK将数据发送到Experience Platform，您必须首先配置数据流。 在数据收集UI中，选择 **[!UICONTROL 数据流]** 中。

创建新数据流或选择要编辑的现有数据流后，选择旁边的切换按钮 **[!UICONTROL Adobe Experience Platform]**. 接下来，使用下面列出的值填写表单。

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| 数据流字段 | 值 |
| --- | --- |
| [!UICONTROL 沙盒] | 平台的名称 [沙盒](../../../sandboxes/home.md) 包含设置数据流所需的流连接和数据集。 |
| [!UICONTROL 流入口] | 有效的流连接，用于Experience Platform。 请参阅 [创建流连接](../../../ingestion/tutorials/create-streaming-connection-ui.md) 如果您没有现有的流入口。 |
| [!UICONTROL 事件数据集] | 安 [!DNL XDM ExperienceEvent] 您计划使用SDK将事件数据发送到的数据集。 虽然您需要提供事件数据集才能创建Platform数据流，但请注意，下游实施工作流中不接受通过事件发送的同意数据。 |
| [!UICONTROL 配置文件数据集] | 的 [!DNL Profile] — 启用了数据集且已创建客户同意字段 [更早](#prerequisites). |

完成后，选择 **[!UICONTROL 保存]** ，并继续按照任何其他提示完成配置。

## 安装和配置平台Web SDK

按照上一节所述创建数据流后，必须配置最终将在您的网站上部署的Platform Web SDK扩展。 如果您的标记资产上未安装SDK扩展，请选择 **[!UICONTROL 扩展]** 在左侧导航中，接下来是 **[!UICONTROL 目录]** 选项卡。 然后，选择 **[!UICONTROL 安装]** 在可用扩展列表中的Platform SDK扩展下。

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

配置SDK时，在 **[!UICONTROL 边缘配置]**，选择在上一步中创建的数据流。

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

选择 **[!UICONTROL 保存]** 以安装扩展。

### 创建数据元素以设置默认同意

安装SDK扩展后，您可以选择创建一个数据元素来表示默认的数据收集同意值(`collect.val`)。 如果您想要根据用户的不同来使用不同的默认值，例如 `pending` 适用于欧盟用户和 `in` 北美用户。

在此用例中，您可以实施以下内容，以根据用户的区域设置默认同意：

1. 确定Web服务器上的用户区域。
1. 在 `script` 标记（嵌入代码），则会呈现单独的 `script` 标记 `adobeDefaultConsent` 变量。
1. 设置使用 `adobeDefaultConsent` JavaScript变量，并将此数据元素用作用户的默认同意值。

如果用户的区域由CMP确定，则可以改用以下步骤：

1. 处理页面上的“CMP loaded”事件。
1. 在事件处理程序中，设置 `adobeDefaultConsent` 变量，然后使用JavaScript加载标记库脚本。
1. 设置使用 `adobeDefaultConsent` JavaScript变量，并将此数据元素用作用户的默认同意值。

要在数据收集UI中创建数据元素，请选择 **[!UICONTROL 数据元素]** 在左侧导航中，选择 **[!UICONTROL 添加数据元素]** 导航到数据元素创建对话框。

在此，您必须创建 [!UICONTROL JavaScript变量] 数据元素基于 `adobeDefaultConsent`. 选择 **[!UICONTROL 保存]** 完成。

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

创建数据元素后，导航回Web SDK扩展配置页面。 在 [!UICONTROL 隐私] 选择 **[!UICONTROL 由数据元素提供]**，然后使用提供的对话框选择之前创建的默认同意数据元素。

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### 在您的网站上部署扩展

配置完该扩展后，即可将其集成到您的网站中。 请参阅 [发布指南](../../../tags/ui/publishing/overview.md) 有关如何部署更新的库内部版本的详细信息，请参阅标记文档。

## 发出同意更改命令 {#commands}

将SDK扩展集成到网站后，即可开始使用Platform Web SDK `setConsent` 命令将同意数据发送到Platform。

的 `setConsent` 命令执行两个操作：

1. 直接在配置文件存储区中更新用户的配置文件属性。 这不会向数据湖发送任何数据。
1. 创建 [体验事件](../../../xdm/classes/experienceevent.md) 会记录同意更改事件的加盖时间戳的帐户。 此数据将直接发送到数据湖，并可用于跟踪同意首选项随时间的变化。

### 何时调用 `setConsent`

有两种情况 `setConsent` 应在您的网站上调用：

1. 在页面上（换言之，在每次加载页面时）加载同意时
1. 作为检测同意设置更改的CMP挂接或事件侦听器的一部分

### `setConsent` 语法

>[!NOTE]
>
>有关Platform SDK命令的常见语法，请参阅 [执行命令](../../../edge/fundamentals/executing-commands.md).

的 `setConsent` 命令需要两个参数：

1. 表示命令类型的字符串(在本例中为 `"setConsent"`)
1. 包含单个数组类型属性的有效负荷对象： `consent`. 的 `consent` 数组必须至少包含一个为Adobe标准提供必需同意字段的对象。

以下示例显示了Adobe标准的必需同意字段 `setConsent` 调用：

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

| 负载属性 | 描述 |
| --- | --- |
| `standard` | 使用的同意标准。 对于Adobe标准，必须将此值设置为 `Adobe`. |
| `version` | 表示同意标准的版本号，如下所示 `standard`. 此值必须设置为 `2.0` 用于Adobe标准同意处理。 |
| `value` | 客户更新的同意信息，作为XDM对象提供，该对象符合启用了用户档案的数据集同意字段的结构。 |

>[!NOTE]
>
>如果您将其他同意标准与 `Adobe` (例如 `IAB TCF`)，则可以向 `consent` 数组。 每个对象必须包含 `standard`, `version`和 `value` 表示的同意标准。

以下JavaScript提供了一个函数示例，该函数用于处理网站上的同意首选项更改，该函数可用作事件侦听器或CMP挂接中的回调：

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

全部 [!DNL Platform SDK] 命令返回指示调用是成功还是失败的promise。 然后，您可以将这些响应用于其他逻辑，如向客户显示确认消息。 请参阅 [处理成功或失败](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) 中有关执行SDK命令的指南，以了解特定示例。

成功创建后 `setConsent` 调用时，您可以使用平台UI中的配置文件查看器来验证数据是否登录到配置文件存储区。 请参阅 [按身份浏览用户档案](../../../profile/ui/user-guide.md#browse-identity) 以了解更多信息。

## 后续步骤

按照本指南，您已将Platform Web SDK扩展配置为将同意数据发送到Experience Platform。 有关测试实施的指导，请参阅要实施的同意标准文档：

* [Adobe标准](./adobe/overview.md#test)
* [TCF 2.0标准](./iab/overview.md#test)
