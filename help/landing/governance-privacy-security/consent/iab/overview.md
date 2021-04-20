---
keywords: Experience Platform；主页；IAB;IAB 2.0；同意；同意
solution: Experience Platform
title: IAB TCF 2.0在Experience Platform中支持
topic: privacy events
description: 了解如何配置数据操作和模式，以在将区段激活到Adobe Experience Platform中的目标时传达客户同意选择。
translation-type: tm+mt
source-git-commit: a845ade0fc1e6e18c36b5f837fe7673a976f01c7
workflow-type: tm+mt
source-wordcount: '2472'
ht-degree: 0%

---


# IAB TCF 2.0在Experience Platform中支持

[!DNL Transparency & Consent Framework](TCF)是[!DNL Interactive Advertising Bureau](IAB)概述的一个开放标准技术框架，旨在使组织能够根据欧洲合并的[!DNL General Data Protection Regulation](GDPR)获得、记录和更新消费者对处理其个人数据的同意。 该框架的第二次迭代 — TCF 2.0 — 为消费者如何提供或拒绝同意提供了更大的灵活性，包括供应商是否和如何使用数据处理的某些特性，如精确地理定位。

>[!NOTE]
>
>有关TCF 2.0的更多信息，可在[IAB欧洲网站](https://iabeurope.eu/tcf-2-0/)上找到，包括支持材料和技术规范。

Adobe Experience Platform是已注册的[IAB TCF 2.0供应商列表](https://iabeurope.eu/vendor-list-tcf-v2-0/)的一部分，位于ID **565**&#x200B;下。 根据TCF 2.0要求，平台允许您收集客户同意数据并将其集成到存储的客户用户档案中。 然后，可以根据用户档案的用例，将此同意数据纳入导出的受众区段中。

>[!IMPORTANT]
>
>平台只能符合TCF的2.0版（或更高版本）。 不支持旧版TCF。

本文档概述了如何配置数据操作和用户档案模式以接受由您的CMP生成的客户同意数据，以及平台在导出区段时如何传达用户同意选择。

## 先决条件

要遵循本指南，您必须使用商业或您自己的、集成并符合IAB TCF的同意管理平台(CMP)。 有关详细信息，请参见兼容CMP的[列表。](https://iabeurope.eu/cmp-list/)

>[!IMPORTANT]
>
>如果CMP的ID无效，平台将按原样处理您的数据。 为了强制实施TCF 2.0，您必须先确认您的CMP具有已向IAB TCF 2.0注册的有效ID，然后再将数据发送到平台。

本指南还要求对以下平台服务有有效的了解：

* [体验数据模型(XDM)](../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md):通过跨设备和系统桥接身份，解决客户体验数据碎片化带来的根本挑战。
* [实时客户用户档案](../../../../profile/home.md):利 [!DNL Identity Service] 用数据集实时创建详细的客户用户档案。[!DNL Real-time Customer Profile] 从Data Lake中提取数据，并将客户用户档案保留在其自己的单独数据存储中。
* [Adobe Experience Platform Web SDK](../../../../edge/home.md):客户端JavaScript库，允许您将各种平台服务集成到面向客户的网站中。
   * [SDK同意命令](../../../../edge/consent/supporting-consent.md):本指南中所示的同意相关SDK命令的用例概述。
* [Adobe Experience Platform Segmentation Service](../../../../segmentation/home.md):允许您将数据分 [!DNL Real-time Customer Profile] 为具有相似特征且对营销策略做出类似反应的群体。

除了上述平台服务之外，您还应熟悉[目标](../../../../data-governance/home.md)及其在平台生态系统中的角色。

## 客户同意流程摘要{#summary}

以下各节介绍了在正确配置系统后如何收集和实施同意数据。

### 同意数据收集

平台允许您通过以下流程收集客户同意数据：

1. 客户通过网站上的对话框提供数据收集的同意偏好。
1. 您的CMP检测同意偏好更改，并相应地生成TCF同意数据。
1. 使用Platform Web SDK，生成的同意数据（由CMP返回）将发送到Adobe Experience Platform。
1. 收集的同意数据被引入[!DNL Profile]启用的数据集，其模式包含TCF同意字段。

除了由CMP同意 — 更改挂接触发的SDK命令外，同意数据还可以通过任何客户生成的XDM数据流入Experience Platform，这些数据直接上传到支持[!DNL Profile]的数据集。

Adobe Audience Manager与平台共享的任何区段（通过[!DNL Audience Manager]源连接器或其他方式）也可能包含同意数据，前提是已通过[!DNL Experience Cloud Identity Service]将这些区段应用了相应的字段。 有关在[!DNL Audience Manager]中收集同意数据的详细信息，请参阅[用于IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html)的Adobe Audience Manager插件上的文档。

### 下游同意强制

成功摄取TCF同意数据后，下游平台服务中将进行以下过程：

1. [!DNL Real-time Customer Profile] 更新该客户用户档案存储的同意数据。
1. 仅当为群集中的每个ID提供了平台的供应商权限(565)时，平台才会处理客户ID。
1. 当将区段导出到属于TCF 2.0供应商列表成员的目标时，只有在为群集中的每个ID提供平台(565)*和*&#x200B;的供应商权限时，平台才包括用户档案。

本文档的其余部分提供有关如何配置平台和数据操作以满足上述收集和执行要求的指导。

## 确定如何在您的CMP {#consent-data}中生成客户同意数据

由于每个CMP系统都是独一无二的，因此您必须确定允许客户在与您的服务交互时提供同意的最佳方式。 实现这一点的常见方法是使用cookie同意对话框，类似于以下示例：

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

此对话框必须允许客选择加入户执行以下操作：

| 同意选项 | 描述 |
| --- | --- |
| **用途** | 用途定义品牌可以使用客户数据的广告技术用途。 为了平台处理客户ID，必须选择以下用途： <ul><li>**目的一**:在设备上存储和/或访问信息</li><li>**目的十**:开发和改进产品</li></ul> |
| **供应商权限** | 除了广告技术用途外，对话框还必须允许客选择加入户使用或停止特定供应商使用其数据，包括Adobe Experience Platform(565)。 |

### 同意字符串{#consent-strings}

无论您使用何种方法收集数据，目标都是根据客户选择的同意选项（称为同意字符串）生成字符串值。

在TCF规范中，同意字符串用于根据政策和供应商定义的特定营销目的，对有关客户同意设置的相关详细信息进行编码。 平台利用这些字符串存储每个客户的同意设置，因此，每次这些设置发生更改时都必须生成一个新的同意字符串。

同意字符串只能由向IAB TCF注册的CMP创建。 有关如何使用您的特定CMP生成同意字符串的详细信息，请参阅IAB TCF GitHub回购协议中的[同意字符串格式指南](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md)。

## 使用TCF同意字段{#datasets}创建数据集

客户同意数据必须发送到模式包含TCF同意字段的数据集。 请参阅[上的教程，创建用于捕获TCF 2.0 connence](./dataset.md)的数据集，了解如何在继续使用本指南之前创建两个必需的数据集。

## 更新[!DNL Profile]合并策略以包含同意数据{#merge-policies}

创建启用[!DNL Profile]的数据集以收集同意数据后，必须确保将合并策略配置为始终在客户用户档案中包含TCF同意字段。 这包括设置数据集优先级，以便您的同意数据集优先于其他可能冲突的数据集。

有关如何使用合并策略的详细信息，请参阅[合并策略用户指南](../../../../profile/ui/merge-policies.md)。 在设置合并策略时，您必须确保您的区段包含[XDM隐私混音](./dataset.md#privacy-mixin)提供的所有必需同意属性，如数据集准备指南中所述。

## 集成Experience Platform Web SDK以收集客户同意数据{#sdk}

>[!NOTE]
>
>要直接在Adobe Experience Platform中处理同意数据，需要使用Experience Platform Web SDK。 [!DNL Experience Cloud Identity Service] 当前不支持。
>
>[!DNL Experience Cloud Identity Service] 但是，仍支持在Adobe Audience Manager中进行同意处理，而符合TCF 2.0仅要求将库更新为 [版本5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases)。

一旦您将CMP配置为生成同意字符串，您必须集成Experience Platform Web SDK以收集这些字符串并将它们发送到平台。 Platform SDK提供两个命令，可用于将TCF同意数据发送到平台（如下子部分所述），当客户首次提供同意信息时以及此后任何时间的同意更改时，应使用这些命令。

**SDK不与任何现成的CMP建立接口**。由您决定如何将SDK集成到您的网站中、侦听CMP中的同意更改并调用相应的命令。

### 创建新的边缘配置

要使SDK将数据发送到Experience Platform，您必须首先在[!DNL Adobe Experience Platform Launch]中为平台创建新的边缘配置。 有关如何创建新配置的具体步骤在[SDK文档](../../../../edge/fundamentals/edge-configuration.md)中提供。

为配置提供唯一名称后，选择&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;旁边的切换按钮。 接下来，使用以下值完成表单的其余部分：

| 边缘配置字段 | 值 |
| --- | --- |
| [!UICONTROL 沙箱] | 平台[沙箱](../../../../sandboxes/home.md)的名称，其中包含设置边缘配置所需的流连接和数据集。 |
| [!UICONTROL Streaming Inlet] | Experience Platform的有效流连接。 如果您没有现有的流入口，请参阅有关创建流连接的教程[。](../../../../ingestion/tutorials/create-streaming-connection-ui.md) |
| [!UICONTROL 事件数据集] | 选择在上一步[中创建的[!DNL XDM ExperienceEvent]数据集。](#datasets) |
| [!UICONTROL 用户档案数据集] | 选择在上一步[中创建的[!DNL XDM Individual Profile]数据集。](#datasets) |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

完成后，选择屏幕底部的&#x200B;**[!UICONTROL 保存]**，然后继续按照任何其他提示完成配置。

### 发出同意更改命令

在创建上一节所述的边缘配置后，您可以使用SDK命令进行开始，以将同意数据发送到平台。 以下各节提供了如何在不同情况下使用每个SDK命令的示例。

>[!NOTE]
>
>有关所有Platform SDK命令的常见语法的介绍，请参阅[执行命令](../../../../edge/fundamentals/executing-commands.md)的文档。

#### 使用CMP同意更改挂接

许多CMP提供了开箱即用的挂钩，用于监听同意更改事件。 发生这些事件时，您可以使用`setConsent`命令更新该客户的同意数据。

`setConsent`命令需要两个参数：(1)指示命令类型的字符串（本例中为“setConnence”），以及(2)包含`consent`数组的有效负荷，该数组必须包含至少一个提供必需同意字段的对象，如下所示：

```js
alloy("setConsent", {
  consent: [{
    standard: "IAB TCF",
    version: "2.0",
    value: "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
    gdprApplies: "true"
  }]
});
```

| 有效负荷属性 | 描述 |
| --- | --- |
| `standard` | 使用的同意标准。 对于TCF 2.0同意处理，此值必须设置为`IAB`。 |
| `version` | `standard`下指示的同意标准版本号。 对于TCF 2.0同意处理，此值必须设置为`2.0`。 |
| `value` | 由CMP生成的基64编码的同意字符串。 |
| `gdprApplies` | 一个布尔值，指示GDPR是否适用于当前登录的客户。 要为此客户强制实施TCF 2.0，必须将值设置为`true`。 如果未定义，则默认为`true`。 |

`setConsent`命令应用作检测同意设置更改的CMP挂接的一部分。 以下JavaScript提供了一个示例，说明如何将`setConsent`命令用于OneTrust的`OnConsentChanged`挂接：

```js
OneTrust.OnConsentChanged(function () {
  // Retrieve the TCF 2.0 consent data generated by the CMP, and pass it to Alloy. 
  __tcfapi("getTCData", 2, function (data, success) {
    if (success) {
      var tcString = data.tcString;
      var gdpr = data.gdprApplies;

      alloy("setConsent", {
        consent: [{
          standard: "IAB TCF",
          version: "2.0",
          value: tcString,
          gdprApplies: gdpr
        }]
      });
    }
  });
});
```

#### 使用事件

您还可以使用`sendEvent`命令收集平台中触发的每个事件的TCF 2.0同意数据。

>[!NOTE]
>
>要使用此方法，您必须将[!DNL Experience Event Privacy mixin]添加到[!DNL Profile]已启用的[!DNL XDM ExperienceEvent]模式。 有关如何配置此模式的步骤，请参阅数据集准备指南中关于[更新ExperienceEvent](./dataset.md#event-schema)的部分。

`sendEvent`命令应用作网站上相应的事件侦听器中的回调。 该命令需要两个参数：(1)指示命令类型（本例中为`sendEvent`）的字符串，以及(2)包含`xdm`对象的有效负荷，该对象将必需的同意字段作为JSON提供：

```js
alloy("sendEvent", {
  xdm: {
    "consentStrings": [{
      "consentStandard": "IAB TCF",
      "consentStandardVersion": "2.0",
      "consentStringValue": "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
      "gdprApplies": true
    }]
  }
});
```

| 有效负荷属性 | 描述 |
| --- | --- |
| `xdm.consentStrings` | 一个数组，它必须包含至少一个提供必需同意字段的对象。 |
| `consentStandard` | 使用的同意标准。 对于TCF 2.0同意处理，此值必须设置为`IAB`。 |
| `consentStandardVersion` | `standard`下指示的同意标准版本号。 对于TCF 2.0同意处理，此值必须设置为`2.0`。 |
| `consentStringValue` | 由CMP生成的基64编码的同意字符串。 |
| `gdprApplies` | 一个布尔值，指示GDPR是否适用于当前登录的客户。 要为此客户强制实施TCF 2.0，必须将值设置为`true`。 如果未定义，则默认为`true`。 |

### 处理SDK响应

所有[!DNL Platform SDK]命令都返回指示调用是成功还是失败的承诺。 然后，您可以使用这些响应获取其他逻辑，如向客户显示确认消息。 有关特定示例，请参见有关执行SDK命令的指南中关于[处理成功或失败](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure)的部分。

## 导出区段{#export}

>[!NOTE]
>
>在开始导出区段之前，您必须确保您的区段包含所有必需的同意字段。 有关详细信息，请参阅[配置合并策略](#merge-policies)一节。

在您收集了受众同意数据并创建了包含必需同意属性的客户细分后，您就可以在将这些细分导出到下游目标时强制实施TCF 2.0规范。

如果对一组客户用户档案将同意设置`gdprApplies`设置为`true`，则根据每个用户档案的TCF同意偏好过滤从这些用户档案导出到下游目标的任何数据。 在导出过程中，将跳过任何不符合所需同意首选项的用户档案。

客户必须同意以下目的（如[TCF 2.0策略](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)所述），以便将其用户档案包括在导出到目标的区段中：

* **目的一**:在设备上存储和/或访问信息
* **目的十**:开发和改进产品

TCF 2.0还要求数据源必须在将数据发送到该目标之前检查目标的供应商权限。 因此，在包括绑定到该目标的数据之前，平台会检查是否为群集中的所有ID选择了目标的供应商权限。

>[!NOTE]
>
>与Adobe Audience Manager共享的任何细分都将包含与其平台对应部分相同的TCF 2.0同意值。 由于[!DNL Audience Manager]与平台(565)共享相同的供应商ID，因此需要相同的用途和供应商权限。 有关详细信息，请参阅[用于IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html)的Adobe Audience Manager插件的文档。

## 测试实施{#test-implementation}

配置TCF 2.0实施并将区段导出到目标后，任何不满足同意要求的数据将不会导出。 但是，为了查看导出过程中是否筛选了正确的客户用户档案，您必须手动检查目标上的数据存储，以查看是否正确执行了同意。

请务必注意，如果群集中有多个ID，并且TCF 2.0适用，则即使单个ID不包含正确的用途和供应商权限，也会排除整个群集。

## 后续步骤

本文档涵盖配置平台数据操作以履行TCF 2.0中概述的业务义务的过程。有关平台隐私相关功能的详细信息，请参阅[治理、隐私和安全](../../overview.md)概述。