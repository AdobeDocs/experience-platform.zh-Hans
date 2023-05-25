---
keywords: Experience Platform；主页；IAB；IAB 2.0；同意；同意
solution: Experience Platform
title: Experience Platform中的IAB TCF 2.0支持
description: 了解如何配置数据操作和架构，以在将区段激活到Adobe Experience Platform中的目标时传达客户同意选择。
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 1%

---

# Experience Platform中的IAB TCF 2.0支持

此 [!DNL Transparency & Consent Framework] (TCF)，如 [!DNL Interactive Advertising Bureau] (IAB)是一个开放标准的技术框架，旨在使各组织能够获取、记录和更新消费者对处理其个人数据的同意，以符合欧盟的 [!DNL General Data Protection Regulation] (GDPR)。 该框架的第二个版本TCF 2.0为消费者如何提供或拒绝同意提供了更大的灵活性，包括供应商是否以及如何使用某些数据处理功能，如精确的地理位置。

>[!NOTE]
>
>有关TCF 2.0的更多信息，请参阅 [IAB欧洲网站](https://iabeurope.eu/tcf-2-0/)，包括支持材料和技术规格。

Adobe Experience Platform是 [IAB TCF 2.0供应商列表](https://iabeurope.eu/vendor-list-tcf-v2-0/)，在ID下 **565**. 为符合TCF 2.0要求，Platform允许您收集客户同意数据并将其集成到存储的客户配置文件中。 然后，可根据用户档案的用例将这些同意数据纳入导出受众区段中是否包含用户档案。

>[!IMPORTANT]
>
>Platform只能符合TCF版本2.0（或更高版本）。 不支持TCF的早期版本。

本文档概述了如何配置数据操作和配置文件架构以接受CMP生成的客户同意数据，以及Platform在导出区段时如何传达用户同意选择。

## 先决条件

要遵循本指南，您必须使用与IAB TCF集成并兼容的商业同意管理平台或您自己的同意管理平台(CMP)。 请参阅 [兼容CMP列表](https://iabeurope.eu/cmp-list/) 了解更多信息。

>[!IMPORTANT]
>
>如果CMP的ID无效，平台将按原样继续处理您的数据。 要实施TCF 2.0，您必须先确认您的CMP具有已在IAB TCF 2.0中注册的有效ID，然后才能将数据发送到Platform。

本指南还需要深入了解以下Platform服务：

* [体验数据模型(XDM)](../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
* [Adobe Experience Platform Identity服务](../../../../identity-service/home.md)：通过跨设备和系统桥接身份，解决客户体验数据碎片化带来的根本挑战。
* [Real-time Customer Profile](../../../../profile/home.md)：利用 [!DNL Identity Service] 从您的数据集实时创建详细的客户配置文件。 [!DNL Real-Time Customer Profile] 从数据湖中提取数据并将客户配置文件保留在其自己的单独数据存储中。
* [Adobe Experience Platform Web SDK](../../../../edge/home.md)：客户端JavaScript库，用于将各种Platform服务集成到面向客户的网站上。
   * [SDK同意命令](../../../../edge/consent/supporting-consent.md)：本指南中显示的与同意相关的SDK命令的用例概述。
* [Adobe Experience Platform Segmentation Service](../../../../segmentation/home.md)：用于除 [!DNL Real-Time Customer Profile] 数据归入个人群组，这些个人群组具有相似的特征，并且对营销策略的响应也类似。

除了上面列出的Platform服务外，您还应熟悉 [目标](../../../../data-governance/home.md) 以及它们在Platform生态系统中的作用。

## 客户同意流程摘要 {#summary}

以下各节介绍了在正确配置系统后，如何收集和执行同意数据。

### 同意数据收集

Platform允许您通过以下过程收集客户同意数据：

1. 客户通过网站上的对话框提供其关于数据收集的同意首选项。
1. 您的CMP会检测同意首选项更改，并相应地生成TCF同意数据。
1. 使用Platform Web SDK，生成的同意数据（由CMP返回）将发送到Adobe Experience Platform。
1. 收集的同意数据将被摄取到 [!DNL Profile]启用了数据集，其架构包含TCF同意字段。

除了CMP同意更改挂接触发的SDK命令之外，同意数据还可以通过客户生成的任何直接上传到的XDM数据流入Experience Platform [!DNL Profile] — 启用的数据集。

Adobe Audience Manager与Platform共享的任何区段(通过 [!DNL Audience Manager] 源连接器或其他内容)也可以包含同意数据，但前提是已通过以下方式将相应的字段应用于这些区段 [!DNL Experience Cloud Identity Service]. 有关在中收集同意数据的更多信息 [!DNL Audience Manager]，请参阅 [适用于IAB TCF的Adobe Audience Manager插件](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=zh-Hans).

### 下游同意执行

成功摄取TCF同意数据后，下游Platform服务中将进行以下过程：

1. [!DNL Real-Time Customer Profile] 更新针对该客户个人资料存储的同意数据。
1. 只有在为群集中的每个ID提供了Platform (565)的供应商权限时，Platform才会处理客户ID。
1. 当将区段导出到属于TCF 2.0供应商列表成员的目标时，如果两个平台的供应商权限都是(565)，则平台仅包括配置文件 *和* 为群集中的每个ID提供单个目标。

本文档中的其余部分提供了有关如何配置Platform和数据操作以满足上述收集和执行要求的指导。

## 确定如何在CMP中生成客户同意数据 {#consent-data}

由于每个CMP系统都是唯一的，因此您必须确定允许客户在与您的服务交互时提供同意的最佳方式。 实现此目标的常见方法是使用Cookie同意对话框，类似于以下示例：

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

此对话框必须允许客户选择加入或退出以下内容：

| 同意选项 | 描述 |
| --- | --- |
| **目的** | 用途定义品牌可以将客户数据用于哪些广告技术目的。 为了使Platform能够处理客户ID，必须选择实现以下目的： <ul><li>**用途1**：在设备上存储和/或访问信息</li><li>**用途10**：开发和改进产品</li></ul> |
| **供应商权限** | 除了广告技术目的之外，该对话框还必须允许客户选择加入或退出让其数据由特定供应商使用，包括Adobe Experience Platform (565)。 |

### 同意字符串 {#consent-strings}

无论您使用何种方法收集数据，目的都是根据客户选择的同意选项生成一个字符串值，称为同意字符串。

在TCF规范中，根据策略和供应商定义的特定营销目的，同意字符串用于编码有关客户同意设置的相关详细信息。 Platform利用这些字符串存储每个客户的同意设置，因此每当这些设置发生更改时，都必须生成一个新的同意字符串。

同意字符串只能由在IAB TCF中注册的CMP创建。 有关如何使用特定CMP生成同意字符串的更多信息，请参阅 [同意字符串格式指南](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) 在IAB TCF GitHub存储库中。

## 使用TCF同意字段创建数据集 {#datasets}

客户同意数据必须发送到其架构包含TCF同意字段的数据集。 请参阅以下教程： [创建数据集以获取TCF 2.0同意](./dataset.md) 了解如何在继续本指南之前创建所需的配置文件数据集（以及可选的Experience Event数据集）。

## 更新 [!DNL Profile] 合并策略以包含同意数据 {#merge-policies}

创建 [!DNL Profile]启用用于收集同意数据的数据集，您必须确保合并策略已配置为始终在客户配置文件中包含TCF同意字段。 这涉及设置数据集优先级，以使您的同意数据集优先于其他潜在冲突的数据集。

有关如何使用合并策略的更多信息，请参阅 [合并策略概述](../../../../profile/merge-policies/overview.md). 在设置合并策略时，必须确保区段包含 [XDM隐私架构字段组](./dataset.md#privacy-field-group)，如数据集准备指南中所述。

## 集成Experience PlatformWeb SDK以收集客户同意数据 {#sdk}

>[!NOTE]
>
>需要使用Experience PlatformWeb SDK才能直接在Adobe Experience Platform中处理同意数据。 [!DNL Experience Cloud Identity Service] 当前不支持。
>
>[!DNL Experience Cloud Identity Service] 仍支持Adobe Audience Manager中的同意处理，但只需将库更新为 [版本5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

将CMP配置为生成同意字符串后，必须集成Experience PlatformWeb SDK以收集这些字符串并将它们发送到Platform。 Platform SDK提供了两个命令，可用于将TCF同意数据发送到Platform（下面各子部分中有说明），并且应在客户首次提供同意信息时以及随后同意发生更改的任何时间使用。

**SDK不会与任何开箱即用的CMP接口**. 您可以自行决定如何将SDK集成到您的网站中，监听CMP中的同意更改，并调用相应的命令。

### 创建新数据流

为了使SDK将数据发送到Experience Platform，您必须首先为Platform创建新的数据流。 有关如何创建新数据流的特定步骤，请参见 [SDK文档](../../../../edge/datastreams/overview.md).

为数据流提供唯一名称后，选择旁边的切换按钮 **[!UICONTROL Adobe Experience Platform]**. 接下来，使用以下值完成表单的其余部分：

| 数据流字段 | 值 |
| --- | --- |
| [!UICONTROL 沙盒] | 平台的名称 [沙盒](../../../../sandboxes/home.md) 包含设置数据流所需的流连接和数据集。 |
| [!UICONTROL 流式入口] | Experience Platform的有效流连接。 请参阅上的教程 [创建流连接](../../../../ingestion/tutorials/create-streaming-connection-ui.md) 如果您没有现有的流式入口。 |
| [!UICONTROL 事件数据集] | 选择 [!DNL XDM ExperienceEvent] 在中创建的数据集 [上一步](#datasets). 如果您包含 [[!UICONTROL IAB TCF 2.0同意] 字段组](../../../../xdm/field-groups/event/iab.md) 在此数据集的架构中，您可以使用 [`sendEvent`](#sendEvent) 命令，将数据存储在此数据集中。 请记住，存储在此数据集中的同意值为 **非** 在自动实施工作流中使用。 |
| [!UICONTROL 配置文件数据集] | 选择 [!DNL XDM Individual Profile] 在中创建的数据集 [上一步](#datasets). 使用响应CMP同意更改挂接时 [`setConsent`](#setConsent) 命令，收集的数据将存储在此数据集中。 由于此数据集启用了配置文件，因此，在自动实施工作流期间，将遵循存储在此数据集中的同意值。 |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

完成后，选择 **[!UICONTROL 保存]** 继续按照任何其他提示完成配置。

### 发出consent-change命令

创建上一部分所述的数据流后，您可以开始使用SDK命令将同意数据发送到Platform。 以下部分提供了如何在不同的场景中使用每个SDK命令的示例。

>[!NOTE]
>
>有关所有Platform SDK命令的通用语法的简介，请参阅以下文档： [执行命令](../../../../edge/fundamentals/executing-commands.md).

#### 使用CMP同意更改挂接 {#setConsent}

许多CMP提供开箱即用的挂接，用于监听同意更改事件。 当这些事件发生时，您可以使用 `setConsent` 命令以更新该客户的同意数据。

此 `setConsent` command需要两个参数：(1)指示命令类型的字符串（在本例中为“setConsent”），以及(2)包含 `consent` 数组，其中必须至少包含一个提供必需同意字段的对象，如下所示：

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

| 有效负载属性 | 描述 |
| --- | --- |
| `standard` | 使用的同意标准。 此值必须设置为 `IAB` 用于进行TCF 2.0同意处理。 |
| `version` | 下所示的同意标准的版本号 `standard`. 此值必须设置为 `2.0` 用于进行TCF 2.0同意处理。 |
| `value` | CMP生成的base-64编码的同意字符串。 |
| `gdprApplies` | 一个布尔值，指示GDPR是否适用于当前登录的客户。 为了为此客户强制实施TCF 2.0，必须将值设置为 `true`. 默认为 `true` 如果未定义。 |

此 `setConsent` 命令应该用作检测同意设置更改的CMP挂接的一部分。 以下JavaScript提供了一个示例，说明 `setConsent` 命令可用于OneTrust的 `OnConsentChanged` 挂钩：

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

您还可以通过使用收集在Platform中触发的每个事件的TCF 2.0同意数据 `sendEvent` 命令。

>[!NOTE]
>
>要使用此方法，您必须已将“体验事件隐私”字段组添加到 [!DNL Profile] — 已启用 [!DNL XDM ExperienceEvent] 架构。 请参阅以下部分： [更新ExperienceEvent架构](./dataset.md#event-schema) ，以了解如何配置此功能的步骤。

此 `sendEvent` 命令应用作网站上相应事件侦听器中的回调。 该命令需要两个参数： (1)指示命令类型的字符串(在本例中， `sendEvent`)，以及(2)包含 `xdm` 将必需的同意字段作为JSON提供的对象：

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

| 有效负载属性 | 描述 |
| --- | --- |
| `xdm.consentStrings` | 一个数组，必须至少包含一个提供必需同意字段的对象。 |
| `consentStandard` | 使用的同意标准。 此值必须设置为 `IAB` 用于进行TCF 2.0同意处理。 |
| `consentStandardVersion` | 下所示的同意标准的版本号 `standard`. 此值必须设置为 `2.0` 用于进行TCF 2.0同意处理。 |
| `consentStringValue` | CMP生成的base-64编码的同意字符串。 |
| `gdprApplies` | 一个布尔值，指示GDPR是否适用于当前登录的客户。 为了为此客户强制实施TCF 2.0，必须将值设置为 `true`. 默认为 `true` 如果未定义。 |

### 处理SDK响应

全部 [!DNL Platform SDK] 命令会返回指示调用是成功还是失败的promise。 然后，您可以将这些响应用于其他逻辑，例如向客户显示确认消息。 请参阅以下部分： [处理成功或失败](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) 有关特定示例，请参阅执行SDK命令指南。

## 导出区段 {#export}

>[!NOTE]
>
>在开始导出区段之前，必须确保区段包含所有必需的同意字段。 请参阅以下部分： [配置合并策略](#merge-policies) 了解更多信息。

收集客户同意数据并创建包含所需同意属性的受众区段后，您可以在将这些区段导出到下游目标时强制执行TCF 2.0合规性。

前提是同意设置 `gdprApplies` 设置为 `true` 对于一组客户用户档案，会根据每个用户档案的TCF同意首选项筛选这些用户档案中导出到下游目标的任何数据。 在导出过程中，将跳过任何不符合所需同意首选项的配置文件。

客户必须同意以下目的(如概述 [TCF 2.0策略](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions))，以便将其用户档案包含在导出到目标的区段中：

* **用途1**：在设备上存储和/或访问信息
* **用途10**：开发和改进产品

TCF 2.0还要求数据源在向目标发送数据之前必须检查目标的供应商权限。 因此，在包含绑定到该目标的数据之前，Platform会检查是否针对群集中的所有ID选择目标的供应商权限。

>[!NOTE]
>
>与Adobe Audience Manager共享的任何区段都将包含与其Platform对应区段相同的TCF 2.0同意值。 从 [!DNL Audience Manager] 共享与Platform (565)相同的供应商ID，需要相同的用途和供应商权限。 查看文档 [适用于IAB TCF的Adobe Audience Manager插件](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=zh-Hans) 了解更多信息。

## 测试实施 {#test-implementation}

配置TCF 2.0实施并将区段导出到目标后，任何不符合同意要求的数据都不会导出。 但是，要查看在导出期间是否筛选了正确的客户配置文件，您必须手动检查目标上的数据存储区，以查看是否正确执行了同意。

请务必注意，如果群集由多个ID组成，并且应用TCF 2.0，那么即使单个ID不包含正确的用途和供应商权限，也将排除整个群集。

## 后续步骤

本文档介绍了配置Platform数据操作以履行TCF 2.0中概述的业务义务的过程。请参阅概述，位于 [治理、隐私和安全](../../overview.md) 有关更多信息，请参阅Platform的隐私相关功能。
