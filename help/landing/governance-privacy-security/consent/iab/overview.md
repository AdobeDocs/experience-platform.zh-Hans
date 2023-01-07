---
keywords: Experience Platform；主页；IAB;IAB 2.0；同意；同意
solution: Experience Platform
title: IAB TCF 2.0支持Experience Platform
description: 了解在Adobe Experience Platform中将区段激活到目标时，如何配置数据操作和模式以传达客户同意选择。
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 1%

---

# IAB TCF 2.0支持Experience Platform

的 [!DNL Transparency & Consent Framework] (TCF)，如 [!DNL Interactive Advertising Bureau] (IAB)是一个开放标准的技术框架，旨在使组织能够根据欧盟的 [!DNL General Data Protection Regulation] (GDPR)。 该框架的第二个迭代版本TCF 2.0为消费者如何提供或拒绝同意提供了更大的灵活性，包括供应商是否以及如何使用数据处理的某些功能，如精确地理位置。

>[!NOTE]
>
>有关TCF 2.0的更多信息，请访问 [IAB欧洲网站](https://iabeurope.eu/tcf-2-0/)，包括支持材料和技术规范。

Adobe Experience Platform是 [IAB TCF 2.0供应商列表](https://iabeurope.eu/vendor-list-tcf-v2-0/)，在ID下 **565**. 根据TCF 2.0要求，Platform允许您收集客户同意数据并将其集成到存储的客户配置文件中。 然后，可以根据用户档案的用例，将此同意数据纳入是否将用户档案包含在导出的受众区段中。

>[!IMPORTANT]
>
>平台只能符合TCF版本2.0（或更高版本）。 不支持TCF的先前版本。

本文档概述了如何配置数据操作和配置文件架构以接受由CMP生成的客户同意数据，以及Platform在导出区段时如何传达用户同意选项。

## 先决条件

要遵循本指南，您必须使用与IAB TCF集成并符合的同意管理平台(CMP)，无论是商业版还是您自己的版本。 请参阅 [符合CMP的列表](https://iabeurope.eu/cmp-list/) 以了解更多信息。

>[!IMPORTANT]
>
>如果CMP的ID无效，平台将继续按原样处理您的数据。 要强制实施TCF 2.0，您必须先确认CMP具有已在IAB TCF 2.0中注册的有效ID，然后再将数据发送到Platform。

本指南还要求您对以下平台服务有一定的了解：

* [体验数据模型(XDM)](../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md):通过跨设备和系统桥接身份，解决客户体验数据碎片化所带来的根本难题。
* [实时客户资料](../../../../profile/home.md):利用 [!DNL Identity Service] 从数据集实时创建详细的客户用户档案。 [!DNL Real-Time Customer Profile] 从数据湖中提取数据，并将客户配置文件保留在其自己的单独数据存储中。
* [Adobe Experience Platform Web SDK](../../../../edge/home.md):客户端JavaScript库，允许您将各种平台服务集成到面向客户的网站中。
   * [SDK同意命令](../../../../edge/consent/supporting-consent.md):本指南中显示的与同意相关的SDK命令的用例概述。
* [Adobe Experience Platform Segmentation Service](../../../../segmentation/home.md):允许您划分 [!DNL Real-Time Customer Profile] 数据会分组到具有相似特征且响应方式与营销策略类似的个人组中。

除了上面列出的平台服务之外，您还应该熟悉 [目标](../../../../data-governance/home.md) 以及他们在平台生态系统中的角色。

## 客户同意流程摘要 {#summary}

以下各节介绍在正确配置系统后如何收集和强制执行同意数据。

### 同意数据收集

平台允许您通过以下流程收集客户同意数据：

1. 客户通过网站上的对话框为数据收集提供其同意首选项。
1. 您的CMP会检测同意首选项更改，并相应地生成TCF同意数据。
1. 使用Platform Web SDK，生成的同意数据（由CMP返回）将发送到Adobe Experience Platform。
1. 收集的同意数据将被摄取到 [!DNL Profile] — 已启用的数据集，其架构包含TCF同意字段。

除了由CMP同意更改挂钩触发的SDK命令外，同意数据还可以通过任何由客户生成的XDM数据流入Experience Platform，这些数据会直接上传到 [!DNL Profile] — 已启用的数据集。

由Adobe Audience Manager与Platform共享的任何区段(通过 [!DNL Audience Manager] 源连接器或其他方式)也可能包含同意数据，但前提是已通过 [!DNL Experience Cloud Identity Service]. 有关在中收集同意数据的更多信息 [!DNL Audience Manager]，请参阅 [适用于IAB TCF的Adobe Audience Manager插件](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=zh-Hans).

### 下游同意强制

成功摄取TCF同意数据后，将在下游Platform服务中进行以下流程：

1. [!DNL Real-Time Customer Profile] 更新存储的客户用户档案同意数据。
1. 仅当为群集中的每个ID提供了平台(565)的供应商权限时，Platform才会处理客户ID。
1. 在将区段导出到属于TCF 2.0供应商列表成员的目标时，仅当两个平台(565)的供应商权限均为时，Platform才包含用户档案 *和* 集群中的每个ID都会提供单个目标。

本文档的其余部分就如何配置平台和您的数据操作以满足上述收集和执行要求提供了指导。

## 确定如何在CMP中生成客户同意数据 {#consent-data}

由于每个CMP系统都是唯一的，因此您必须确定在客户与您的服务进行交互时允许其提供同意的最佳方式。 实现此目的的常见方法是使用Cookie同意对话框，如下例所示：

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

此对话框必须允许客户选择启用或禁用以下选项：

| 同意选项 | 描述 |
| --- | --- |
| **目的** | 目的可定义品牌可将客户数据用于哪些广告技术目的。 为了使Platform能够处理客户ID，必须选择以下目的： <ul><li>**用途1**:在设备上存储和/或访问信息</li><li>**用途10**:开发和改进产品</li></ul> |
| **供应商权限** | 除了广告技术目的之外，该对话框还必须允许客户选择加入或退出由特定供应商使用其数据，包括Adobe Experience Platform(565)。 |

### 同意字符串 {#consent-strings}

无论您使用何种方法收集数据，目标都是根据客户选择的同意选项（称为同意字符串）生成字符串值。

在TCF规范中，同意字符串用于根据策略和供应商定义的特定营销目的，对有关客户同意设置的相关详细信息进行编码。 Platform会利用这些字符串来存储每个客户的同意设置，因此，每当这些设置发生更改时，都必须生成一个新的同意字符串。

同意字符串只能由在IAB TCF中注册的CMP创建。 有关如何使用特定CMP生成同意字符串的更多信息，请参阅 [同意字符串格式化指南](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) 在IAB TCF GitHub存储库中。

## 创建包含TCF同意字段的数据集 {#datasets}

必须将客户同意数据发送到架构中包含TCF同意字段的数据集。 请参阅 [创建用于捕获TCF 2.0同意的数据集](./dataset.md) ，以了解在继续阅读本指南之前，如何创建所需的用户档案数据集（和可选的体验事件数据集）。

## 更新 [!DNL Profile] 合并策略以包含同意数据 {#merge-policies}

创建 [!DNL Profile] — 启用了用于收集同意数据的数据集，您必须确保将合并策略配置为始终在客户配置文件中包含TCF同意字段。 这包括设置数据集优先级，以便同意数据集优先于其他可能存在冲突的数据集。

有关如何使用合并策略的更多信息，请参阅 [合并策略概述](../../../../profile/merge-policies/overview.md). 在设置合并策略时，必须确保区段包含 [XDM隐私架构字段组](./dataset.md#privacy-field-group)，如数据集准备指南中所述。

## 集成Experience PlatformWeb SDK以收集客户同意数据 {#sdk}

>[!NOTE]
>
>要直接在Adobe Experience Platform中处理同意数据，需要使用Experience PlatformWeb SDK。 [!DNL Experience Cloud Identity Service] 当前不支持。
>
>[!DNL Experience Cloud Identity Service] 但是，Adobe Audience Manager中仍支持进行同意处理，并且符合TCF 2.0仅要求将库更新为 [版本5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

将CMP配置为生成同意字符串后，必须集成Experience PlatformWeb SDK以收集这些字符串并将它们发送到平台。 Platform SDK提供了两个命令，可用于将TCF同意数据发送到Platform（如以下子部分所述），当客户首次提供同意信息以及随后同意更改时，应使用这两个命令。

**SDK不会与任何现成的CMP进行接口**. 至于如何将SDK集成到您的网站，如何监听CMP中的同意更改，以及如何调用相应的命令，这将由您来决定。

### 创建新数据流

为了使SDK将数据发送到Experience Platform，您必须先为Platform创建新的数据流。 有关如何创建新数据流的具体步骤，请参阅 [SDK文档](../../../../edge/datastreams/overview.md).

为数据流提供唯一名称后，选择旁边的切换按钮 **[!UICONTROL Adobe Experience Platform]**. 接下来，使用以下值完成表单的其余部分：

| 数据流字段 | 值 |
| --- | --- |
| [!UICONTROL 沙盒] | 平台的名称 [沙盒](../../../../sandboxes/home.md) 包含设置数据流所需的流连接和数据集。 |
| [!UICONTROL 流入口] | 有效的流连接，用于Experience Platform。 请参阅 [创建流连接](../../../../ingestion/tutorials/create-streaming-connection-ui.md) 如果您没有现有的流入口。 |
| [!UICONTROL 事件数据集] | 选择 [!DNL XDM ExperienceEvent] 在中创建的数据集 [上一步](#datasets). 如果您将 [[!UICONTROL IAB TCF 2.0同意] 字段组](../../../../xdm/field-groups/event/iab.md) 在此数据集的架构中，您可以使用 [`sendEvent`](#sendEvent) 命令，将该数据存储到此数据集中。 请记住，存储在此数据集中的同意值是 **not** 在自动执行工作流中使用。 |
| [!UICONTROL 配置文件数据集] | 选择 [!DNL XDM Individual Profile] 在中创建的数据集 [上一步](#datasets). 在使用响应CMP同意更改挂接时 [`setConsent`](#setConsent) 命令，则收集的数据将存储在此数据集中。 由于此数据集启用了配置文件，因此在自动执行工作流中会遵循存储在此数据集中的同意值。 |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

完成后，选择 **[!UICONTROL 保存]** ，并继续按照任何其他提示完成配置。

### 发出同意更改命令

创建上一节中所述的数据流后，您可以开始使用SDK命令将同意数据发送到平台。 以下部分提供了如何在不同情景中使用每个SDK命令的示例。

>[!NOTE]
>
>有关所有Platform SDK命令的常用语法，请参阅 [执行命令](../../../../edge/fundamentals/executing-commands.md).

#### 使用CMP同意更改挂接 {#setConsent}

许多CMP提供了可监听同意更改事件的现成挂钩。 当发生这些事件时，您可以使用 `setConsent` 命令来更新客户的同意数据。

的 `setConsent` 命令需要两个参数：(1)指示命令类型（在本例中为“setConsent”）的字符串，以及(2)包含 `consent` 数组，其中必须至少包含一个提供必需同意字段的对象，如下所示：

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

| 负载属性 | 描述 |
| --- | --- |
| `standard` | 使用的同意标准。 此值必须设置为 `IAB` 用于TCF 2.0同意处理。 |
| `version` | 表示同意标准的版本号，如下所示 `standard`. 此值必须设置为 `2.0` 用于TCF 2.0同意处理。 |
| `value` | 由CMP生成的基于64编码的同意字符串。 |
| `gdprApplies` | 一个布尔值，指示GDPR是否适用于当前已登录的客户。 要为此客户强制实施TCF 2.0，必须将值设置为 `true`. 默认为 `true` 如果未定义。 |

的 `setConsent` 命令应用作检测同意设置更改的CMP挂接的一部分。 以下JavaScript提供了如何 `setConsent` 命令可用于OneTrust的 `OnConsentChanged` 钩：

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

#### 使用事件 {#sendEvent}

您还可以使用 `sendEvent` 命令。

>[!NOTE]
>
>要使用此方法，您必须已将体验事件隐私字段组添加到 [!DNL Profile]已启用 [!DNL XDM ExperienceEvent] 架构。 请参阅 [更新ExperienceEvent架构](./dataset.md#event-schema) 有关如何配置数据集准备指南中的步骤。

的 `sendEvent` 命令应用作您网站上相应事件侦听器的回调。 该命令需要两个参数：(1)指示命令类型的字符串(在本例中， `sendEvent`)和(2)包含 `xdm` 将必需同意字段提供为JSON的对象：

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

| 负载属性 | 描述 |
| --- | --- |
| `xdm.consentStrings` | 一个数组，必须至少包含一个提供必需同意字段的对象。 |
| `consentStandard` | 使用的同意标准。 此值必须设置为 `IAB` 用于TCF 2.0同意处理。 |
| `consentStandardVersion` | 表示同意标准的版本号，如下所示 `standard`. 此值必须设置为 `2.0` 用于TCF 2.0同意处理。 |
| `consentStringValue` | 由CMP生成的基于64编码的同意字符串。 |
| `gdprApplies` | 一个布尔值，指示GDPR是否适用于当前已登录的客户。 要为此客户强制实施TCF 2.0，必须将值设置为 `true`. 默认为 `true` 如果未定义。 |

### 处理SDK响应

全部 [!DNL Platform SDK] 命令返回指示调用是成功还是失败的promise。 然后，您可以将这些响应用于其他逻辑，如向客户显示确认消息。 请参阅 [处理成功或失败](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) 中有关执行SDK命令的指南，以了解特定示例。

## 导出区段 {#export}

>[!NOTE]
>
>在开始导出区段之前，必须确保区段包含所有必需的同意字段。 请参阅 [配置合并策略](#merge-policies) 以了解更多信息。

收集客户同意数据并创建包含所需同意属性的受众区段后，您便可以在将这些区段导出到下游目标时强制实施TCF 2.0合规性。

但前提是同意设置 `gdprApplies` 设置为 `true` 对于一组客户配置文件，将根据每个配置文件的TCF同意首选项过滤这些配置文件中导出到下游目标的任何数据。 在导出过程中会跳过任何不符合所需同意首选项的配置文件。

客户必须同意以下目的(如 [TCF 2.0政策](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions))，以便将其用户档案包含在导出到目标的区段中：

* **用途1**:在设备上存储和/或访问信息
* **用途10**:开发和改进产品

TCF 2.0还要求数据源必须先检查目标的供应商权限，然后才能向该目标发送数据。 因此，在包括绑定到该目标的数据之前，Platform会检查目标的供应商权限是否针对群集中的所有ID选择了。

>[!NOTE]
>
>与Adobe Audience Manager共享的任何区段将包含与其Platform对应的相同的TCF 2.0同意值。 自 [!DNL Audience Manager] 与平台(565)共享相同的供应商ID，需要相同的目的和供应商权限。 请参阅 [适用于IAB TCF的Adobe Audience Manager插件](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=zh-Hans) 以了解更多信息。

## 测试实施 {#test-implementation}

配置TCF 2.0实施并将区段导出到目标后，任何不符合同意要求的数据都将不会导出。 但是，为了查看在导出期间是否过滤了正确的客户配置文件，您必须手动检查目标上的数据存储区，以查看是否正确强制了同意。

请务必注意，如果群集中包含多个ID，并且TCF 2.0适用，则即使单个ID不包含正确目的和供应商权限，也会排除整个群集。

## 后续步骤

本文档介绍了配置平台数据操作以履行TCF 2.0所概述的业务义务的过程。请参阅 [管理、隐私和安全](../../overview.md) 有关更多信息，请参阅Platform的隐私相关功能。
