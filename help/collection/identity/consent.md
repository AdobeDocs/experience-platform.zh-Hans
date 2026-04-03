---
title: 数据收集中的同意和身份
description: 了解同意选择如何影响Web SDK实施中的身份行为，包括ECID生成、Cookie持久性和访客连续性。
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 2%

---

# 数据收集中的同意和身份

在Web SDK实施中，同意和身份密切相关。 收集同意的方式和时间会直接影响到Web SDK何时生成ECID、设置身份Cookie并将数据发送到Edge Network以及是否生成这些数据。 如果同意处理不当，结果通常是访客数量出现意外增加、身份连续性出现差距或同时出现两者。

此页面介绍同意选择如何与身份行为交互，并提供配置实施以避免常见隐患的指导。 有关Web SDK如何处理ECID、FPID和其他身份信号的背景，请参阅数据收集中的[身份](./overview.md)。

## 同意如何影响身份 {#how-consent-affects-identity}

Web SDK同时使用[`defaultConsent`](/help/collection/js/commands/configure/defaultconsent.md)配置变量和[`setConsent`](/help/collection/js/commands/setconsent.md)命令来控制它是否向Edge Network发送数据。 同意状态直接决定何时生成ECID以及何时设置身份Cookie。

下表显示了`defaultConsent`和`setConsent`对数据收集、Cookie设置和标识行为的组合影响。

| `defaultConsent` | `setConsent` | 发生数据收集 | 已设置浏览器Cookie | 身份行为 |
| --- | --- | --- | --- | --- |
| `in` | 未设置 | 是 | 是 | ECID会在第一个请求时立即生成。 标识Cookie在页面加载时设置。 |
| `in` | `in` | 是 | 是 | 访客的现有ECID将保留。 身份行为保持不变。 |
| `in` | `out` | 否 | 是 | 数据收集停止。 现有ECID和`kndctr_`身份Cookie将保留在浏览器中，直到它们过期。 |
| `pending` | 未设置 | 否 | 否 | 不生成ECID。 未设置Cookie。 事件在本地排队，直到调用`setConsent`。 |
| `pending` | `in` | 是 | 是 | 发送排队的事件。 ECID在第一个请求中生成，并设置身份Cookie。 |
| `pending` | `out` | 否 | 是 | 排队的事件将被丢弃。 不生成ECID。 同意Cookie设置为记录访客的偏好。 |
| `out` | 未设置 | 否 | 否 | 不生成ECID。 未设置Cookie。 不发送任何事件。 |
| `out` | `in` | 是 | 是 | ECID在第一个请求中生成，并设置身份Cookie。 |
| `out` | `out` | 否 | 是 | 不生成ECID。 同意Cookie设置为记录访客的偏好。 |

>[!NOTE]
>
>即使访客选择禁用，也会设置身份和同意Cookie。 这些Cookie是尊重访客的数据收集偏好设置所必需的。 有关Web SDK设置的Cookie的完整列表，请参阅[Web SDK Cookie](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk)。

当访客在之前撤销同意后重新授予同意（通过在`setConsent`后使用`"general": "in"`调用`"general": "out"`）时，Web SDK会恢复发送事件并使用Cookie中的现有ECID（如果尚未过期）。 访客的身份将被保留。

在访客授予或拒绝同意后，Web SDK会在`kndctr_`同意Cookie中保留其偏好设置。 在后续加载页面时，SDK会读取此Cookie并自动应用存储的首选项 — 除非访客的首选项发生更改，否则无需再次调用`setConsent`。 请注意，`defaultConsent`配置值在页面加载之间不持久，但访客的已解析同意（通过`setConsent`设置）持久。

>[!NOTE]
>
>在同意为`pending`时排队的事件保留在内存中，在页面重新加载后无法继续运行。 如果访客在同意得到解决之前导航到新页面，则前一个页面中的排队事件将丢失。

## 实施模式 {#implementation-patterns}

### 选择加入模型（收集之前需要征得同意） {#opt-in}

当法规（如GDPR）在收集任何数据之前需要明确同意时，可使用此模式。

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "pending"
});

// When the visitor grants consent:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "in" }
  }]
});
```

采用以下模式：
* 在获得同意之前，不会生成ECID。
* 同意之前触发的事件（例如初始页面查看）将排入队列，并在同意被授予后发送。
* 身份Cookie仅在首次成功的Edge Network请求后设置。

### 选择退出模型（默认收集，拒绝时停止） {#opt-out}

当法规默认允许数据收集并带有选择退出选项时，请使用此模式。

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "in"
});

// If the visitor opts out:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "out" }
  }]
});
```

采用以下模式：
* ECID在首次加载页面时立即生成。
* 所有事件都会发送，直到访客选择退出为止。
* 选择退出后，Web SDK将停止发送事件，但现有Cookie会保留。

## 同意第一方设备ID {#consent-with-fpids}

如果您的实施使用[第一方设备ID (FPID)](./fpid.md)，则您的服务器将设置FPID Cookie，而不依赖于Web SDK的同意状态。 FPID Cookie是在您自己的基础架构中管理的标识符。 但是，FPID仅在Web SDK发出请求（由同意控制）时发送到Edge Network：

* 使用`defaultConsent: "pending"`时，浏览器中存在FPID，但在获得同意之前，不会使用FPID为ECID提供种子。
* 对于`defaultConsent: "in"`，FPID用于第一个请求并立即为ECID提供种子。

如果您的同意实施要求在同意之前不设置标识符，请延迟设置FPID Cookie，直到传达同意为止。 仅Web SDK的同意审核不会阻止设置FPID Cookie，因为它由您的服务器管理。

## 常见陷阱 {#common-pitfalls}

+++**同意横幅清除身份Cookie**

**问题**：在展示同意横幅时，在访客做出选择之前，某些同意管理平台(CMP)会清除所有Cookie（包括`kndctr_`身份Cookie）。 当访客授予同意时，Web SDK会生成一个新的ECID，因为之前的ECID已被删除。 访客在报表中显示为新人员。

**症状**：
* 部署同意横幅后，独特访客计数激增。
* 每次同意过期且再次与横幅交互后，回访访客均会计为新访客。

**解决方案**：配置您的CMP以保留`kndctr_`个Cookie。 这些Cookie是身份Cookie，而不是跟踪Cookie — 它们识别设备并且不包含行为数据。 如果您的CMP需要清除Cookie，请将`kndctr_`前缀的Cookie添加到排除列表。 或者，延迟清除Cookie直到访客明确拒绝同意后才清除，而不是先占式清除。

+++

+++**延迟同意导致身份重复**

**问题**：当`defaultConsent`设置为`pending`时，Web SDK将在发送任何数据之前等待同意。 如果在页面生命周期的后期授予同意（例如，在触发页面重新加载的横幅交互之后），以下顺序可能会导致问题：

1. 页面加载。 `defaultConsent: "pending"`的问题。Web SDK不发送请求。
2. 访客授予同意。 CMP触发页面重新加载。
3. 页面将再次加载。 Web SDK使用现在已授予的同意进行初始化，并生成ECID。

此流程正常，并且可以正常工作。 当CMP或您的实施无意中清除了步骤2和步骤3之间的Cookie，或者在重新加载时以不同方式配置Web SDK时，就会出现问题。

**解决方案**：确保Web SDK配置（尤其是`orgId`和`defaultConsent`）在每次页面加载时都相同。 如果您的CMP在同意后触发重新加载，请验证身份Cookie是否在重新加载后继续存在。

+++

+++**在同意横幅中使用`defaultConsent: "in"`**

**问题**：某些实施设置了`defaultConsent: "in"`，如果访客拒绝，则使用`setConsent`调用`"general": "out"`。 此方法会生成一个ECID，并在同意被拒绝之前发送至少一个请求。 根据您的监管要求，此初始数据收集可能与贵组织的隐私政策不一致。

**解决方案**：如果您的监管环境要求在任何数据收集或ECID生成之前获得同意，请改用`defaultConsent: "pending"`。 此设置可确保在明确授予同意之前，Web SDK不会与Edge Network通信。

+++
