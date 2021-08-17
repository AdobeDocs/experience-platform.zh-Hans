---
title: 使用Adobe Experience Platform Web SDK处理客户同意数据
topic-legacy: getting started
description: 了解如何使用Adobe Experience Platform 2.0标准集成Adobe Experience Platform Web SDK以在Adobe中处理客户同意数据。
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: 272cf2906b44ccfeca041d9620ac0780e24ad1ae
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 0%

---

# 集成Platform Web SDK以使用Adobe2.0标准处理客户同意数据

利用Adobe Experience Platform Web SDK，可检索由同意管理平台(CMP)生成的客户同意信号，并在发生同意更改事件时将其发送到Adobe Experience Platform。

**SDK不会与任何现成的CMP进行接口**。至于如何将SDK集成到您的网站，如何监听CMP中的同意更改，以及如何调用相应的命令，这将由您来决定。 本文档提供了有关如何将CMP与Platform Web SDK集成的一般指导。

>[!NOTE]
>
>本指南将指导您完成在数据收集UI中通过标记扩展集成SDK的步骤。 如果您想改用独立版本的SDK，请参阅以下文档：
>
>* [配置数据流](../../../../edge/fundamentals/datastreams.md)
* [安装SDK](../../../../edge/fundamentals/installing-the-sdk.md)
* [为同意命令配置SDK](../../../../edge/consent/supporting-consent.md)


## 先决条件

本教程假定您已确定如何在CMP中生成同意数据，并已创建一个包含已为实时客户资料启用同意字段的数据集。 要进一步了解这些步骤，请在返回本指南之前，参阅Experience Platform](./overview.md)中的[同意处理概述。

此外，本指南还要求您对标记扩展及其在Web应用程序中的安装方式有一定的了解。 有关更多信息，请参阅以下文档：

* [标记概述](../../../../tags/home.md)
* [快速入门指南](../../../../tags/quick-start/quick-start.md)
* [发布概述](../../../../tags/ui/publishing/overview.md)

## 设置数据流

要使SDK将数据发送到Experience Platform，您必须在数据收集UI中设置适用于平台的现有数据流。 此外，您为配置选择的[!UICONTROL 配置文件数据集]必须包含标准化的同意字段。

创建新配置或选择要编辑的现有配置后，选择&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;旁边的切换按钮。 接下来，使用下面列出的值填写表单。

![](../../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| 数据流字段 | 值 |
| --- | --- |
| [!UICONTROL 沙盒] | 平台[sandbox](../../../../sandboxes/home.md)的名称，其中包含设置数据流所需的流连接和数据集。 |
| [!UICONTROL 流入口] | 有效的流连接，用于Experience Platform。 如果您没有现有的流入口，请参阅有关创建流连接](../../../../ingestion/tutorials/create-streaming-connection-ui.md)的教程。[ |
| [!UICONTROL 事件数据集] | 您计划使用SDK将事件数据发送到的[!DNL XDM ExperienceEvent]数据集。 虽然您需要提供事件数据集才能创建Platform数据流，但请注意，当前不支持直接通过事件发送同意数据。 |
| [!UICONTROL 配置文件数据集] | 启用了[!DNL Profile]且之前已创建客户同意字段的数据集。 |

完成后，选择屏幕底部的&#x200B;**[!UICONTROL Save]**，然后继续按任何其他提示完成配置。


## 安装和配置平台Web SDK

按照上一节所述创建数据流后，必须配置最终将在您的网站上部署的Platform Web SDK扩展。 如果您的标记资产上未安装SDK扩展，请在左侧导航中选择&#x200B;**[!UICONTROL Extensions]**，然后选择&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡。 然后，在可用扩展列表的Platform SDK扩展下选择&#x200B;**[!UICONTROL Install]**。

![](../../../images/governance-privacy-security/consent/adobe/sdk/install.png)

配置SDK时，在&#x200B;**[!UICONTROL 边缘配置]**&#x200B;下，选择您在上一步中创建的数据流。

![](../../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

选择&#x200B;**[!UICONTROL Save]**&#x200B;以安装该扩展。

### 创建数据元素以设置默认同意

安装SDK扩展后，您可以选择创建一个数据元素来表示用户的默认数据收集同意值(`collect.val`)。 如果您希望根据用户使用不同的默认值，例如`pending`（欧盟用户）和`in`（北美用户），则此选项会很有用。

在此用例中，您可以实施以下内容，以根据用户的区域设置默认同意：

1. 确定Web服务器上的用户区域。
1. 在网页上的`script`标记（嵌入代码）之前，渲染一个单独的`script`标记，该标记会根据用户的区域设置一个`adobeDefaultConsent`变量。
1. 设置一个使用`adobeDefaultConsent` JavaScript变量的数据元素，并将此数据元素用作用户的默认同意值。

如果用户的区域由CMP确定，则可以改用以下步骤：

1. 处理页面上的“CMP loaded”事件。
1. 在事件处理程序中，根据用户区域设置一个`adobeDefaultConsent`变量，然后使用JavaScript加载标记库脚本。
1. 设置一个使用`adobeDefaultConsent` JavaScript变量的数据元素，并将此数据元素用作用户的默认同意值。

要在数据收集UI中创建数据元素，请在左侧导航中选择&#x200B;**[!UICONTROL 数据元素]**，然后选择&#x200B;**[!UICONTROL 添加数据元素]**&#x200B;以导航到数据元素创建对话框。

在此，必须基于`adobeDefaultConsent`创建[!UICONTROL JavaScript变量]数据元素。 完成后，选择&#x200B;**[!UICONTROL 保存]**。

![](../../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

创建数据元素后，导航回Web SDK扩展配置页面。 在[!UICONTROL Privacy]部分下，选择&#x200B;**[!UICONTROL 由数据元素提供]**，然后使用提供的对话框选择之前创建的默认同意数据元素。

![](../../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### 在您的网站上部署扩展

配置完该扩展后，即可将其集成到您的网站中。 有关如何部署更新的库内部版本的详细信息，请参阅标记文档中的[发布指南](../../../../tags/ui/publishing/overview.md)。

## 发出同意更改命令 {#commands}

将SDK扩展集成到网站后，您可以开始使用Platform Web SDK `setConsent`命令将同意数据发送到Platform。

在以下两种情况下，应在您的网站上调用`setConsent`:

1. 在页面上（换言之，在每次加载页面时）加载同意时
1. 作为检测同意设置更改的CMP挂接或事件侦听器的一部分

>[!NOTE]
有关Platform SDK命令的常见语法的介绍，请参阅[正在执行命令](../../../../edge/fundamentals/executing-commands.md)的文档。

`setConsent`命令需要两个参数：

1. 指示命令类型的字符串（在本例中为`"setConsent"`）
1. 包含单个数组类型属性的有效负荷对象：`consent`。 `consent`数组必须至少包含一个对象，该对象为Adobe标准提供必需的同意字段。

以下示例`setConsent`调用中显示了Adobe标准的必需同意字段：

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
| `standard` | 使用的同意标准。 对于Adobe标准，此值必须设置为`Adobe`。 |
| `version` | `standard`下所示的同意标准的版本号。 要进行Adobe标准同意处理，必须将此值设置为`2.0`。 |
| `value` | 客户更新的同意信息，作为XDM对象提供，该对象符合启用了用户档案的数据集同意字段的结构。 |

>[!NOTE]
如果您将其他同意标准与`Adobe`（例如`IAB TCF`）结合使用，则可以为每个标准向`consent`数组添加其他对象。 每个对象必须包含`standard`、`version`和`value`的相应值，以表示同意标准。

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

所有[!DNL Platform SDK]命令都返回指示调用是成功还是失败的承诺。 然后，您可以将这些响应用于其他逻辑，如向客户显示确认消息。 有关特定示例，请参阅执行SDK命令指南中[处理成功或失败](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure)的部分。

## 后续步骤

按照本指南，您已将Platform Web SDK扩展配置为将同意数据发送到Experience Platform。 现在，您可以返回同意处理概述以了解有关如何[测试实施](./overview.md#test-implementation)的步骤。
