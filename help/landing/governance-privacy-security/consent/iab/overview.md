---
keywords: Experience Platform；主页；IAB;IAB 2.0；同意；同意
solution: Experience Platform
title: IAB TCF 2.0在Experience Platform中支持
topic: privacy events
description: 了解如何配置模式操作和数据，以在将区段激活到Adobe Experience Platform的目标时传达用户同意选择。
translation-type: tm+mt
source-git-commit: b2d3e4608dc0640472966edccd3fb5a612d7583c
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 0%

---


# IAB TCF 2.0在Experience Platform中支持

[!DNL Transparency & Consent Framework](IAB)概述的[!DNL Interactive Advertising Bureau](TCF)是一个开放标准技术框架，旨在使组织能够根据欧洲合并的[!DNL General Data Protection Regulation](GDPR)获得、记录和更新消费者对处理其个人数据的同意。 该框架的第二次迭代TCF 2.0为消费者如何提供或拒绝同意提供了更大的灵活性，包括供应商是否以及如何使用数据处理的某些特征，如精确的地理定位。

>[!NOTE]
>
>有关TCF 2.0的更多信息，请访问[IAB欧洲网站](https://iabeurope.eu/tcf-2-0/)，包括支持材料和技术规范。

Adobe Experience Platform是已注册的[IAB TCF 2.0供应商列表](https://iabeurope.eu/vendor-list-tcf-v2-0/)的一部分，该供应商的标识为&#x200B;**565**。 根据TCF 2.0要求，平台允许您收集客户同意数据并将其集成到存储的客户用户档案中。 此同意数据随后可以纳入导出的用户档案区段中，具体取决于受众的使用情况。

>[!IMPORTANT]
>
>平台只能符合TCF的2.0版（或更高版本）。 不支持旧版TCF。

本文档概述了如何配置数据操作和用户档案模式以接受由您的CMP生成的客户同意数据，以及平台如何在导出区段时传达用户同意选择。

## 先决条件

要遵循本指南，您必须使用商业或您自己的、集成并符合IAB TCF的同意管理平台(CMP)。 有关详细信息，请参见符合规范的CMP的[列表。](https://iabeurope.eu/cmp-list/)

>[!IMPORTANT]
>
>如果CMP的ID无效，平台将按原样继续处理您的数据。 为了强制实施TCF 2.0，您必须先确认您的CMP具有已向IAB TCF 2.0注册的有效ID，然后再将数据发送到平台。

本指南还要求对以下平台服务有有效的了解：

* [体验数据模型(XDM)](../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
* [Adobe Experience Platform身份服务](../../../../identity-service/home.md):通过跨设备和系统桥接身份，解决客户体验数据碎片化带来的根本挑战。
* [实时客户用户档案](../../../../profile/home.md):利 [!DNL Identity Service] 用数据集实时创建详细的客户用户档案。[!DNL Real-time Customer Profile] 从Data Lake中提取数据，并将客户用户档案保留在其自己的单独数据存储中。
* [Adobe Experience PlatformWeb SDK](../../../../edge/home.md):客户端JavaScript库，允许您将各种平台服务集成到面向客户的网站中。
   * [SDK同意命令](../../../../edge/consent/supporting-consent.md):本指南中所示的同意相关SDK命令的用例概述。
* [Adobe Experience Platform细分服务](../../../../segmentation/home.md):允许您将数据分 [!DNL Real-time Customer Profile] 为具有相似特征并将响应类似于营销策略的个人组。

除了上面列出的平台服务，您还应熟悉[目标](../../../../data-governance/home.md)及其在平台生态系统中的作用。

## 客户同意流程摘要{#summary}

以下各节介绍了在正确配置系统后如何收集和实施同意数据。

### 同意数据收集

平台允许您通过以下流程收集客户同意数据：

1. 客户通过网站上的对话框提供其数据收集的同意偏好。
1. 您的CMP检测同意偏好更改，并相应地生成TCF同意数据。
1. 使用Platform Web SDK，生成的同意数据（由CMP返回）将发送到Adobe Experience Platform。
1. 收集的同意数据被引入[!DNL Profile]启用的数据集中，该数据集的模式包含TCF同意字段。

除了由CMP同意更改挂接触发的SDK命令外，同意数据还可以通过任何由客户生成的XDM数据流入Experience Platform，这些数据直接上传到支持[!DNL Profile]的数据集。

Adobe Audience Manager（通过[!DNL Audience Manager]源连接器或其他方式）与平台共享的任何区段也可能包含同意数据，前提是已通过[!DNL Experience Cloud Identity Service]将这些区段应用了相应的字段。 有关在[!DNL Audience Manager]中收集同意数据的详细信息，请参阅[Adobe Audience ManagerIAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html)插件上的文档。

### 下游同意执行

成功摄取TCF同意数据后，下游平台服务中将进行以下过程：

1. [!DNL Real-time Customer Profile] 更新该客户用户档案的已存储同意数据。
1. 仅当为群集中的每个ID提供了平台的供应商权限(565)时，平台才处理客户ID。
1. 当将区段导出到属于TCF 2.0供应商列表成员的目标时，仅当为群集中的每个ID提供平台(565)*和*&#x200B;的各个目标的供应商权限时，平台才包括用户档案。

本文档的其余部分提供有关如何配置平台和数据操作以满足上述收集和执行要求的指导。

## 确定如何在您的CMP{#consent-data}中生成客户同意数据

由于每个CMP系统都是独一无二的，您必须确定在客户与您的服务交互时允许其提供同意的最佳方式。 实现此目的的常见方法是使用cookie同意对话框，与以下示例类似：

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

此对话框必须允许客选择加入户执行以下操作：

| 同意选项 | 描述 |
| --- | --- |
| **用途** | 用途定义品牌可以使用客户数据用于哪些广告技术用途。 为了平台处理客户ID，必须选择以下用途： <ul><li>**目的1**:在设备上存储和／或访问信息</li><li>**目的十**:开发和改进产品</li></ul> |
| **供应商权限** | 除了广告技术用途外，对话还必须允许客选择加入户使用其数据，包括Adobe Experience Platform(565)。 |

### 同意字符串{#consent-strings}

无论您使用何种方法收集数据，目标都是根据客户选择的同意选项（称为同意字符串）生成字符串值。

在TCF规范中，同意字符串用于根据策略和供应商定义的特定营销目的对有关客户同意设置的相关详细信息进行编码。 平台利用这些字符串存储每个客户的同意设置，因此每次这些设置发生更改时都必须生成新的同意字符串。

同意字符串只能由注册到IAB TCF的CMP创建。 有关如何使用您的特定CMP生成同意字符串的详细信息，请参阅IAB TCF GitHub回购协议中的[同意字符串格式指南](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md)。

## 创建具有TCF同意字段{#datasets}的数据集

客户同意数据必须发送到模式包含TCF同意字段的数据集。 有关如何在继续使用本指南之前创建两个必需数据集，请参阅[上的教程，创建用于捕获TCF 2.0同意](./dataset.md)的数据集。

## 更新[!DNL Profile]合并策略以包含同意数据{#merge-policies}

创建启用[!DNL Profile]的数据集以收集同意数据后，必须确保将合并策略配置为始终在客户用户档案中包含TCF同意字段。 这涉及设置数据集的优先级，以便您的同意数据集优先于其他可能冲突的数据集。

有关如何使用合并策略的详细信息，请参阅[合并策略用户指南](../../../../profile/ui/merge-policies.md)。 在设置合并策略时，您必须确保您的细分包含[XDM隐私混合](./dataset.md#privacy-mixin)提供的所有必需同意属性，如数据集准备指南中所述。

## 集成Experience PlatformWeb SDK以收集客户同意数据{#sdk}

>[!NOTE]
>
>要直接在Adobe Experience Platform处理同意Experience Platform，必须使用Web SDK。 [!DNL Experience Cloud Identity Service] 当前不支持。
>
>[!DNL Experience Cloud Identity Service] 但是，在Adobe Audience Manager仍支持同意处理，而且遵守TCF 2.0仅要求将库更新 [为5.0版](https://github.com/Adobe-Marketing-Cloud/id-service/releases)。

将CMP配置为生成同意字符串后，必须集成Experience PlatformWeb SDK以收集这些字符串并将其发送到平台。 Platform SDK提供两个命令，可用于将TCF同意数据发送到Platform（如下子部分所述），当客户首次提供同意信息时以及此后任何同意更改时，应使用这些命令。

**SDK不与任何现成的CMP建立接口**。由您决定如何将SDK集成到您的网站中，倾听CMP中的同意更改并调用相应的命令。

### 创建新的边缘配置

要使SDK将数据发送到Experience Platform，您必须首先在[!DNL Adobe Experience Platform Launch]中为平台创建新的边缘配置。 有关如何创建新配置的具体步骤，请参见[SDK文档](../../../../edge/fundamentals/edge-configuration.md)。

为配置提供唯一名称后，选择&#x200B;**[!UICONTROL Adobe Experience Platform]**&#x200B;旁边的切换按钮。 接下来，使用以下值完成表单的其余部分：

| 边缘配置字段 | 值 |
| --- | --- |
| [!UICONTROL 沙箱] | 平台[沙箱](../../../../sandboxes/home.md)的名称，该平台包含设置边缘配置所需的流连接和数据集。 |
| [!UICONTROL Streaming Inlet] | Experience Platform的有效流连接。 如果没有现有流入口，请参阅有关创建流连接的教程[。](../../../../ingestion/tutorials/create-streaming-connection-ui.md) |
| [!UICONTROL 事件数据集] | 选择在上一步[中创建的[!DNL XDM ExperienceEvent]数据集。](#datasets) |
| [!UICONTROL 用户档案数据集] | 选择在上一步[中创建的[!DNL XDM Individual Profile]数据集。](#datasets) |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

完成后，选择屏幕底部的&#x200B;**[!UICONTROL 保存]**，然后继续按照任何其他提示完成配置。

### 发出同意——更改命令

在创建上一节所述的边缘配置后，您可以使用SDK命令开始，将同意数据发送到平台。 以下各节提供了如何在不同情况下使用每个SDK命令的示例。

>[!NOTE]
>
>有关所有Platform SDK命令的常见语法的介绍，请参见[执行命令](../../../../edge/fundamentals/executing-commands.md)的文档。

#### 使用CMP同意更改挂接

许多CMP提供开箱即用的挂钩，用于倾听同意更改事件。 当发生这些事件时，您可以使用`setConsent`命令更新客户的同意数据。

`setConsent`命令需要两个参数：(1)一个字符串，它指示命令类型（本例中为“setConnence”），和(2)一个包含`consent`数组的有效负荷，该数组必须包含至少一个提供必需同意字段的对象，如下所示：

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
| `standard` | 正在使用的同意标准。 对于TCF 2.0同意处理，此值必须设置为`IAB`。 |
| `version` | `standard`下所示的同意标准的版本号。 对于TCF 2.0同意处理，此值必须设置为`2.0`。 |
| `value` | 由CMP生成的基于64编码的同意字符串。 |
| `gdprApplies` | 一个布尔值，它指示GDPR是否适用于当前登录的客户。 要为此客户强制实施TCF 2.0，必须将值设置为`true`。 |

`setConsent`命令应作为CMP挂接的一部分使用，该挂接检测同意设置中的更改。 以下JavaScript提供了一个示例，说明如何将`setConsent`命令用于OneTrust的`OnConsentChanged`挂接：

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
>要使用此方法，您必须将[!DNL Experience Event Privacy mixin]添加到启用[!DNL Profile]的[!DNL XDM ExperienceEvent]模式。 有关如何配置此模式的步骤，请参阅数据集准备指南中有关[更新ExperienceEvent](./dataset.md#event-schema)的部分。

`sendEvent`命令应用作网站上相应的事件监听器中的回调。 该命令需要两个参数：(1)指示命令类型的字符串（本例中为`sendEvent`），以及(2)包含`xdm`对象的有效负荷，该对象将必需的同意字段作为JSON提供：

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
| `xdm.consentStrings` | 必须包含至少一个提供必需同意字段的对象的数组。 |
| `consentStandard` | 正在使用的同意标准。 对于TCF 2.0同意处理，此值必须设置为`IAB`。 |
| `consentStandardVersion` | `standard`下所示的同意标准的版本号。 对于TCF 2.0同意处理，此值必须设置为`2.0`。 |
| `consentStringValue` | 由CMP生成的基于64编码的同意字符串。 |
| `gdprApplies` | 一个布尔值，它指示GDPR是否适用于当前登录的客户。 要为此客户强制实施TCF 2.0，必须将值设置为`true`。 |

### 处理SDK响应

所有[!DNL Platform SDK]命令都返回指示调用是成功还是失败的承诺。 然后，您可以使用这些响应获取其他逻辑，如向客户显示确认消息。 有关特定示例，请参见有关执行SDK命令的指南中关于[处理成功或失败](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure)的部分。

## 导出区段{#export}

>[!NOTE]
>
>在开始导出区段之前，您必须确保区段包含所有必需的同意字段。 有关详细信息，请参见[配置合并策略](#merge-policies)一节。

一旦您收集了受众同意数据并创建了包含必需同意属性的客户细分，您便可以在将这些细分导出到下游目标时强制实施TCF 2.0合规性。

如果对于一组客户用户档案将同意设置`gdprApplies`设置为`true`，则根据每个用户档案的同意偏好过滤那些用户档案中导出到下游目的地的任何数据。 在导出过程中，将跳过任何不符合要求的同意首选项的用户档案。

客户必须同意以下目的（如[TCF 2.0策略](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)所述），以便将其用户档案包含在导出到目标的区段中：

* **目的1**:在设备上存储和／或访问信息
* **目的十**:开发和改进产品

TCF 2.0还要求数据源在将数据发送到该目标之前必须检查目标的供应商权限。 因此，平台在包括绑定到该目标的数据之前，会检查该目标的供应商权限是否已选择用于群集中的所有ID。

>[!NOTE]
>
>与Adobe Audience Manager共享的任何细分都将包含与其平台对应部分相同的TCF 2.0同意值。 由于[!DNL Audience Manager]与平台(565)共享相同的供应商ID，因此需要相同的用途和供应商权限。 有关详细信息，请参见[IAB TCF的Adobe Audience Manager插件](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html)上的文档。

## 测试实施{#test-implementation}

配置TCF 2.0实施并将区段导出到目标后，任何不符合同意要求的数据将不会导出。 但是，为了查看导出过程中是否筛选了正确的客户用户档案，您必须手动检查目标上的数据存储，以查看是否正确执行了同意。

请务必注意，如果群集中包含多个ID并且应用了TCF 2.0，则即使单个ID不包含正确的用途和供应商权限，也会排除整个群集。

## 后续步骤

本文档涵盖配置平台数据操作以履行TCF 2.0概述的业务义务的过程。有关平台隐私相关功能的详细信息，请参阅[治理、隐私和安全](../../overview.md)概述。