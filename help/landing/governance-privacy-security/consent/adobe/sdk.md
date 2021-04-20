---
title: 使用Adobe Experience Platform Web SDK处理客户同意数据
topic: getting started
description: 了解如何使用Adobe 2.0标准集成Adobe Experience Platform Web SDK以在Adobe Experience Platform中处理客户同意数据。
translation-type: tm+mt
source-git-commit: fee3f005ca3679f8639cea45c16150090b2a1e0f
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 0%

---


# 集成Platform Web SDK以使用Adobe 2.0标准处理客户同意数据

Adobe Experience Platform Web SDK允许您检索由同意管理平台(CMP)生成的客户同意信号，并在出现同意更改事件时将它们发送到Adobe Experience Platform。

**SDK不与任何现成的CMP建立接口**。由您决定如何将SDK集成到您的网站中、侦听CMP中的同意更改并调用相应的命令。 本文档提供有关如何将CMP与Platform Web SDK集成的一般指导。

## 先决条件

本教程假定您已经确定了如何在您的CMP中生成同意数据，并且已创建了一个包含已启用“实时客户”用户档案的同意字段的数据集。 要进一步了解这些步骤，请在返回本指南之前参阅Experience Platform](./overview.md)中的[同意处理概述。

此外，本指南要求您能够深入了解Adobe Experience Platform Launch扩展以及它们如何安装在Web应用程序中。 有关更多信息，请参阅以下文档：

* [platform launch概述](https://experienceleague.adobe.com/docs/launch/using/home.html)
* [快速入门指南](https://experienceleague.adobe.com/docs/launch/using/get-started/quick-start.html)
* [发布概述](https://experienceleague.adobe.com/docs/launch/using/publish/overview.html)

## 设置边缘配置

要使SDK将数据发送到Experience Platform，您必须具有在Adobe Experience Platform Launch中设置的平台的现有边缘配置。 此外，您为配置选择的[!UICONTROL Profile Dataset]必须包含标准化的同意字段。

创建新配置或选择要编辑的现有配置后，选择&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;旁边的切换按钮。 接下来，使用下面列出的值完成表单。

![](../../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| 边缘配置字段 | 值 |
| --- | --- |
| [!UICONTROL Sandbox] | 平台[沙箱](../../../../sandboxes/home.md)的名称，其中包含设置边缘配置所需的流连接和数据集。 |
| [!UICONTROL Streaming Inlet] | Experience Platform的有效流连接。 如果您没有现有的流入口，请参阅有关创建流连接的教程[。](../../../../ingestion/tutorials/create-streaming-connection-ui.md) |
| [!UICONTROL Event Dataset] | 您计划使用SDK将事件数据发送到的[!DNL XDM ExperienceEvent]数据集。 虽然您需要提供事件数据集才能创建平台边缘配置，但请注意，目前不支持直接通过事件发送同意数据。 |
| [!UICONTROL Profile Dataset] | 已启用[!DNL Profile]且包含您之前创建的客户同意字段的数据集。 |

完成后，选择屏幕底部的&#x200B;**[!UICONTROL Save]**&#x200B;并继续按照任何其他提示完成配置。


## 安装和配置平台Web SDK扩展

创建上一部分所述的边缘配置后，您必须配置最终将部署到您站点的平台Web SDK扩展。 如果您的Platform launch属性中未安装SDK扩展，请在左侧导航中选择&#x200B;**[!UICONTROL Extensions]**，然后选择&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡。 然后，在可用扩展的列表中，选择“平台SDK扩展”下的&#x200B;**[!UICONTROL Install]**。

![](../../../images/governance-privacy-security/consent/adobe/sdk/install.png)

配置SDK时，在&#x200B;**[!UICONTROL Edge Configurations]**&#x200B;下，选择您在上一步中创建的配置。

![](../../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

选择&#x200B;**[!UICONTROL Save]**&#x200B;以安装扩展。

### 创建数据元素以设置默认同意

安装SDK扩展后，您可以选择创建一个数据元素来表示用户的默认数据收集同意值(`collect.val`)。 如果您希望根据用户设置不同的默认值，例如`pending`(欧洲合并用户)和`in`（北美用户），则此选项非常有用。

在此用例中，您可以实施以下内容以根据用户区域设置默认同意：

1. 确定Web服务器上的用户区域。
1. 在网页上的Platform launch脚本标签（嵌入代码）之前，渲染一个单独的脚本标签，该标签根据用户的区域设置`adobeDefaultConsent`变量。
1. 设置一个使用`adobeDefaultConsent` JavaScript变量的数据元素，并将此数据元素用作用户的默认同意值。

如果用户的区域由CMP确定，则可以改用以下步骤：

1. 处理页面上的“CMP加载”事件。
1. 在事件处理函数中，根据用户区域设置`adobeDefaultConsent`变量，然后使用JavaScript加载Platform launch库脚本。
1. 设置一个使用`adobeDefaultConsent` JavaScript变量的数据元素，并将此数据元素用作用户的默认同意值。

要在Platform launchUI中创建数据元素，请在左侧导航中选择&#x200B;**[!UICONTROL Data Elements]**，然后选择&#x200B;**[!UICONTROL Add Data Element]**&#x200B;以导航到数据元素创建对话框。

从此处，必须创建基于`adobeDefaultConsent`的[!UICONTROL JavaScript Variable]数据元素。 完成后，选择 **[!UICONTROL Save]**。

![](../../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

创建数据元素后，导航回Web SDK扩展配置页。 在[!UICONTROL Privacy]部分下，选择&#x200B;**[!UICONTROL Provided by data element]**，然后使用提供的对话框选择您之前创建的默认同意数据元素。

![](../../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### 在您的网站上部署扩展

配置完扩展后，该扩展便可集成到您的网站中。 有关如何部署更新的库构建的详细信息，请参阅Platform launch文档中的[发布指南](https://experienceleague.adobe.com/docs/launch/using/publish/overview.html)。

## 发出同意更改命令

将SDK扩展集成到您的网站后，您可以使用Platform Web SDK `setConsent`命令进行开始，以将同意数据发送到平台。

在您的站点上应调用`setConsent`的两种情况：

1. 当同意在页面上加载时（换句话说，在每次页面加载时）
1. 作为检测同意设置更改的CMP挂接或事件侦听器的一部分

>[!NOTE]
>
>有关Platform SDK命令的常见语法的介绍，请参见[执行命令](../../../../edge/fundamentals/executing-commands.md)的文档。

`setConsent`命令需要两个参数：

1. 指示命令类型的字符串（在本例中为`"setConsent"`）
1. 包含单个数组类型属性的负载对象：`consent`。 `consent`数组必须至少包含一个为Adobe标准提供必需同意字段的对象。

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

| 有效负荷属性 | 描述 |
| --- | --- |
| `standard` | 使用的同意标准。 对于Adobe标准，此值必须设置为`Adobe`。 |
| `version` | `standard`下指示的同意标准版本号。 此值必须设置为`2.0`才能进行Adobe标准同意处理。 |
| `value` | 客户的更新同意信息，作为符合启用用户档案的数据集同意字段结构的XDM对象提供。 |

>[!NOTE]
>
>如果您正在将其他同意标准与`Adobe`（如`IAB TCF`）结合使用，则可以为每个标准向`consent`数组添加其他对象。 每个对象必须包含`standard`、`version`和`value`的相应值，以表示它们所代表的同意标准。

以下JavaScript提供了一个用于处理网站上的同意首选项更改的函数示例，该函数可用作事件侦听器或CMP挂接中的回调：

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

所有[!DNL Platform SDK]命令都返回指示调用是成功还是失败的承诺。 然后，您可以使用这些响应获取其他逻辑，如向客户显示确认消息。 有关特定示例，请参见有关执行SDK命令的指南中关于[处理成功或失败](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure)的部分。

## 后续步骤

按照本指南，您已配置Platform Web SDK扩展以向Experience Platform发送同意数据。 现在，您可以返回到同意处理概述，了解有关如何[测试实施](./overview.md#test-implementation)的步骤。