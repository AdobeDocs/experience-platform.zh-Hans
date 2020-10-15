---
keywords: Experience Platform;home;IAB;IAB 2.0;consent;Consent
solution: Experience Platform
title: 实时客户数据平台中的IAB TCF 2.0支持
topic: privacy events
translation-type: tm+mt
source-git-commit: b24c624df188be3cbe7f71dcdf8a23d2478c287c
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 1%

---


# 中的IAB TCF 2.0支持 [!DNL Real-time Customer Data Platform]

( [!DNL Transparency & Consent Framework] IAB)概述的(TCF)是一个开放标准的技术框架，旨在使组织能够根据欧洲合并(GDPR)获得、记录和更新消费者对处理其个人数据的 [!DNL Interactive Advertising Bureau][!DNL General Data Protection Regulation] 同意。 该框架的第二次迭代TCF 2.0为消费者如何提供或拒绝同意提供了更大的灵活性，包括供应商是否以及如何使用数据处理的某些特征，如精确的地理定位。

>[!NOTE]
>
>有关TCF 2.0的更多信息，请访 [问IAB欧洲网站](https://iabeurope.eu/tcf-2-0/)，包括支持材料和技术规范。

[!DNL Real-time Customer Data Platform (Real-time CDP)] 是ID 565下注 [册的IAB TCF 2.0供应商列表](https://iabeurope.eu/vendor-list-tcf-v2-0/)的一 **部分**。 根据TCF 2.0要求，您可 [!DNL Real-time CDP] 以收集客户同意数据并将其集成到存储的客户用户档案中。 此同意数据随后可以纳入导出的用户档案区段中，具体取决于受众的使用情况。

>[!IMPORTANT]
>
>[!DNL Real-time CDP] 只能符合TCF的2.0版（或更高版本）。 不支持旧版TCF。

本文档概述了如何配置数据操作和用户档案模式以接受由您的CMP生成的客户同意数据，以及如何在导出区段 [!DNL Real-time CDP] 时传达用户同意选择。

## 先决条件

要遵循本指南，您必须使用商业或您自己的、集成并符合IAB TCF的同意管理平台(CMP)。 有关更 [多信息，请参见合规](https://iabeurope.eu/cmp-list/) CMP的列表。

>[!IMPORTANT]
>
>如果CMP的ID无效， [!DNL Real-time CDP] 将按原样处理数据。 为了强制实施TCF 2.0，您必须先确认您的CMP具有已向IAB TCF 2.0注册的有效ID，然后再将数据发送到 [!DNL Experience Platform]。

本指南还要求对下列Adobe Experience Platform服务有工作上的理解：

* [体验数据模型(XDM)](../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
* [Adobe Experience Platform身份服务](../../../identity-service/home.md):通过跨设备和系统桥接身份，解决客户体验数据碎片化带来的根本挑战。
* [实时客户用户档案](../../../profile/home.md):利 [!DNL Identity Service] 用数据集实时创建详细的客户用户档案。 [!DNL Real-time Customer Profile] 从Data Lake中提取数据，并将客户用户档案保留在其自己的单独数据存储中。
* [Adobe Experience PlatformWeb SDK](../../../edge/home.md):客户端JavaScript库，允许您将各种服务集 [!DNL Platform] 成到面向客户的网站中。
   * [SDK同意命令](../../../edge/consent/supporting-consent.md):本指南中所示的同意相关SDK命令的用例概述。
* [Adobe Experience Platform细分服务](../../../segmentation/home.md):允许您将数据分 [!DNL Real-time Customer Profile] 为具有相似特征并将对营销策略做出类似响应的个人组。

除了上面列 [!DNL Platform] 出的服务，您还应熟悉目 [的地](../../destinations/destinations-overview.md) 及其使用情况 [!DNL Real-time CDP]。

## 客户同意流程摘要 {#summary}

以下各节介绍了在正确配置系统后如何收集和实施同意数据。

### 同意数据收集

[!DNL Real-time CDP] 允许您通过以下流程收集客户同意数据：

1. 客户通过网站上的对话框提供其数据收集的同意偏好。
1. 您的CMP检测同意偏好更改，并相应地生成IAB同意数据。
1. 使用该 [!DNL Experience Platform Web SDK]方法，生成的同意数据（由《议定书》/《公约》缔约方会议返回）被发送到Adobe Experience Platform。
1. 所收集的同意数据被引入其模式 [!DNL Profile]包含IAB同意字段的启用数据集中。

除了由CMP同意更改挂接触发的SDK命令外，同意数据还可以通过客户生 [!DNL Experience Platform] 成的任何XDM数据流入，这些数据直接上传到启用 [!DNL Profile]了数据集。

Adobe Audience Manager(通过源连 [!DNL Platform] 接器或其他方式)共享的任 [!DNL Audience Manager] 何细分也可能包含同意数据，但前提是已通过将适当的字段应用到这些细分 [!DNL Experience Cloud Identity Service]。 有关在中收集同意数据的 [!DNL Audience Manager]更多信息，请参 [阅IAB TCF的Adobe Audience Manager插件文档](https://docs.adobe.com/help/zh-Hans/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html)。

### 下游同意执行

成功摄取IAB同意数据后，下游服务中将进行以下 [!DNL Real-time CDP] 过程：

1. [!DNL Real-time Customer Profile] 更新该客户用户档案的已存储同意数据。
1. [!DNL Real-time CDP] 仅当为群集中的每个ID提 [!DNL Real-time CDP] 供了(565)的供应商权限时，才处理客户ID。
1. 当将区段导出到属于TCF 2.0供应商列表成员的目标时， [!DNL Real-time CDP] 仅当为群集中的每个ID提供了供应商 [!DNL Real-time CDP] ( *565)和目* 标的用户档案权限时，才包括。

本文档的其余部分提供有关如何配置和数据操 [!DNL Real-time CDP] 作以满足上述收集和执行要求的指导。

## 确定如何在您的CMP中生成客户同意数据 {#consent-data}

由于每个CMP系统都是独一无二的，您必须确定在客户与您的服务交互时允许其提供同意的最佳方式。 实现此目的的常见方法是使用cookie同意对话框，与以下示例类似：

![](../assets/iab/cmp-dialog.png)

此对话框必须允许客选择加入户执行以下操作：

| 同意选项 | 描述 |
| --- | --- |
| **用途** | 用途定义品牌可以使用客户数据用于哪些广告技术用途。 要处理客户ID，必须选择 [!DNL Real-time CDP] 以下用途： <ul><li>**目的1**:在设备上存储和／或访问信息</li><li>**目的十**:开发和改进产品</li></ul> |
| **供应商权限** | 除了广告技术用途外，该对话还必须允许客选择加入户使用或停止特定供应商使用其数据，包括(565 [!DNL  Real-time CDP] )。 |

### 同意字符串 {#consent-strings}

无论您使用何种方法收集数据，目标都是根据客户选择的同意选项（称为同意字符串）生成字符串值。

在TCF规范中，同意字符串用于根据策略和供应商定义的特定营销目的对有关客户同意设置的相关详细信息进行编码。 [!DNL Real-time CDP] 利用这些字符串存储每个客户的同意设置，因此每次这些设置发生更改时必须生成新的同意字符串。

同意字符串只能由注册到IAB TCF的CMP创建。 有关如何使用您的特定CMP生成同意字符串的更多信息，请参 [阅IAB TCF GitHub回购](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) 中的同意字符串格式指南。

## 创建包含IAB同意字段的数据集 {#datasets}

客户同意数据必须发送到模式包含IAB同意字段的数据集。 请参阅有关如何创 [建数据集以获取TCF 2.0同意的教程](./dataset-preparation.md) ，以了解如何创建两个必需的数据集，然后继续阅读本指南。

## 更新 [!DNL Profile] 合并策略以包含同意数据 {#merge-policies}

在创建了用于收 [!DNL Profile]集同意数据的启用数据集后，您必须确保将合并策略配置为始终在客户用户档案中包含IAB同意字段。 这涉及设置数据集的优先级，以便您的同意数据集优先于其他可能冲突的数据集。

有关如何使用合并策略的详细信息，请参阅合 [并策略用户指南](../../../profile/ui/merge-policies.md)。 在设置合并策略时，您必须确保您的细分包含XDM隐私混合提供的所有必 [需同意属性](./dataset-preparation.md#privacy-mixin)，如数据集准备指南中所述。

## 集成Web [!DNL Experience Platform] SDK以收集客户同意数据 {#sdk}

>[!NOTE]
>
>要直接在Adobe Experience Platform [!DNL Experience Platform] 处理同意数据，必须使用Web SDK。 [!DNL Experience Cloud Identity Service] 当前不支持。
>
>[!DNL Experience Cloud Identity Service] 但是，在Adobe Audience Manager仍支持同意处理，而且遵守TCF 2.0仅要求将库更新 [为5.0版](https://github.com/Adobe-Marketing-Cloud/id-service/releases)。

将CMP配置为生成同意字符串后，必须集成Web [!DNL Experience Platform] SDK来收集这些字符串并将其发送 [!DNL Platform]到。 SDK提 [!DNL Platform] 供两个命令，可用于向平台发送IAB同意数据（如下各小节所述），当客户首次提供同意信息时，以及此后任何同意更改时，应使用这些命令。

**SDK不与任何现成的CMP建立接口**。 由您决定如何将SDK集成到您的网站中，倾听CMP中的同意更改并调用相应的命令。

### 创建新的边缘配置

要使SDK向其发送数据，您 [!DNL Experience Platform]必须首先为中创建新的边缘 [!DNL Platform] 配置 [!DNL Adobe Experience Platform Launch]。 SDK文档中提供了如何创建新配置的特 [定步骤](../../../edge/fundamentals/edge-configuration.md)。

为配置提供唯一名称后，选择Adobe Experience Platform旁的切换按 **[!UICONTROL 钮]**。 接下来，使用以下值完成表单的其余部分：

| 边缘配置字段 | 值 |
| --- | --- |
| [!UICONTROL 沙箱] | 沙箱的名 [!DNL Platform] 称 [](../../../sandboxes/home.md) ，沙箱包含设置边缘配置所需的流连接和数据集。 |
| [!UICONTROL Streaming Inlet] | 有效的流连接 [!DNL Experience Platform]。 如果您没有现 [有的流入口](../../../ingestion/tutorials/create-streaming-connection-ui.md) ，请参阅有关创建流连接的教程。 |
| [!UICONTROL 事件数据集] | 选择在上 [!DNL XDM ExperienceEvent] 一步中创建 [的数据集](#datasets)。 |
| [!UICONTROL 用户档案数据集] | 选择在上 [!DNL XDM Individual Profile] 一步中创建 [的数据集](#datasets)。 |

![](../assets/iab/edge-config.png)

完成后，单 **[!UICONTROL 击屏]** 幕底部的“保存”，然后继续按照任何其他提示完成配置。

### 发出同意——更改命令

在创建上一节所述的边缘配置后，您可以使用SDK命令开始，将同意数据发送到 [!DNL Platform]。 以下各节提供了如何在不同情况下使用每个SDK命令的示例。

>[!NOTE]
>
>有关所有SDK命令的常见语法 [!DNL Platform] 的介绍，请参阅执行命 [令的文档](../../../edge/fundamentals/executing-commands.md)。

#### 使用CMP同意更改挂接

许多CMP提供开箱即用的挂钩，用于倾听同意更改事件。 当发生这些事件时，您可以 `setConsent` 使用命令更新该客户的同意数据。

该命 `setConsent` 令需要两个参数：(1)一个字符串，它指示命令类型（本例中为“setConnence”），和(2)包含数组的有效负荷，该数组必须至少包含一个提供必需同意字段的对象，如下所示： `consent`

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
| `standard` | 正在使用的同意标准。 对于TCF 2.0同意处理，此值必须设置为“IAB”。 |
| `version` | 下所示的同意标准的版本号 `standard`。 对于TCF 2.0同意处理，此值必须设置为“2.0”。 |
| `value` | 由CMP生成的基于64编码的同意字符串。 |
| `gdprApplies` | 一个布尔值，它指示GDPR是否适用于当前登录的客户。 要为此客户强制实施TCF 2.0，必须将值设置为“true”。 |

该 `setConsent` 命令应作为检测同意设置更改的CMP挂接的一部分使用。 以下JavaScript提供了如何将该命 `setConsent` 令用于OneTrust挂接的示 `OnConsentChanged` 例：

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

您还可以使用命令收集在中触发的每个事件的TCF 2. [!DNL Platform] 0同意 `sendEvent` 数据。

>[!NOTE]
>
>要使用此方法，您必须已将添加到启 [!DNL Experience Event Privacy mixin] 用的 [!DNL Profile]模式 [!DNL XDM ExperienceEvent] 中。 有关如何配置 [ExperienceEvent模式](./dataset-preparation.md#event-schema) ，请参阅数据集准备指南中有关更新ExperienceEvent的部分。

该命 `sendEvent` 令应用作网站上相应的事件监听器中的回调。 该命令需要两个参数：(1)一个字符串，它指示命令类型（本例中为“sendEvent”），以及(2)一个有效负荷，它包含一个 `xdm` 将必需的同意字段作为JSON提供的对象：

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
| `consentStandard` | 正在使用的同意标准。 对于TCF 2.0同意处理，此值必须设置为“IAB”。 |
| `consentStandardVersion` | 下所示的同意标准的版本号 `standard`。 对于TCF 2.0同意处理，此值必须设置为“2.0”。 |
| `consentStringValue` | 由CMP生成的基于64编码的同意字符串。 |
| `gdprApplies` | 一个布尔值，它指示GDPR是否适用于当前登录的客户。 要为此客户强制实施TCF 2.0，必须将值设置为“true”。 |

### 处理SDK响应

所有 [!DNL Platform SDK] 命令都返回指示调用是成功还是失败的承诺。 然后，您可以使用这些响应获取其他逻辑，如向客户显示确认消息。 有关特定示例，请 [参阅执行SDK](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) 命令指南中有关处理成功或失败的部分。

## 导出区段 {#export}

>[!NOTE]
>
>在开始导出区段之前，您必须确保区段包含所有必需的同意字段。 有关详细信息，请参 [阅有关配置合并策](#merge-policies) 略的部分。

一旦您收集了受众同意数据并创建了包含必需同意属性的客户细分，您便可以在将这些细分导出到下游目标时强制实施TCF 2.0合规性。

如果同意设置被 `gdprApplies` 设置为 `true` 一组客户用户档案，则根据每个用户档案的同意偏好过滤从那些用户档案导出到下游目的地的任何数据。 在导出过程中，将跳过任何不符合要求的同意首选项的用户档案。

客户必须同意以下目的(如 [TCF 2.0策略所概述](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions))，以便将用户档案包括在导出到目标的区段中：

* **目的1**:在设备上存储和／或访问信息
* **目的十**:开发和改进产品

TCF 2.0还要求数据源在将数据发送到该目标之前必须检查目标的供应商权限。 因此， [!DNL Real-time CDP] 在包括绑定到该目标的数据之前，检查该目标的供应商权限是否已选择用于群集中的所有ID。

>[!NOTE]
>
>与Adobe Audience Manager共享的任何细分都将包含与其对应的TCF 2.0同意值相 [!DNL Platform] 同的。 由于 [!DNL Audience Manager] 与(565)共享同 [!DNL Real-time CDP] 一供应商ID，因此需要相同的用途和供应商权限。 有关更多信息， [请参阅IAB TCF的Adobe Audience Manager插件文档](https://docs.adobe.com/help/zh-Hans/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) 。

## Test your implementation {#test-implementation}

配置TCF 2.0实施并将区段导出到目标后，任何不符合同意要求的数据将不会导出。 但是，为了查看导出过程中是否筛选了正确的客户用户档案，您必须手动检查目标上的数据存储，以查看是否正确执行了同意。

请务必注意，如果群集中包含多个ID并且应用了TCF 2.0，则即使单个ID不包含正确的用途和供应商权限，也会排除整个群集。

## 后续步骤

本文档涵盖配置数据操作以符 [!DNL Real-time CDP] 合TCF 2.0的过程。有关提供的其他隐私功能的详细信息，请参 [!DNL Real-time CDP]阅以下文档：

* [实时CDP中的隐私保护](../privacy-overview.md)
* [实时CDP中的数据管理](../data-governance-overview.md)