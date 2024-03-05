---
title: 数据流配置覆盖
description: 了解如何通过Web SDK配置数据流覆盖。
source-git-commit: 9cb46957a1c9755dcad6279aae5f5cc04eb6b305
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 14%

---


# 配置数据流覆盖

此 `edgeConfigOverrides` 对象允许您覆盖在当前页面上运行的命令的配置设置。 此覆盖对象不是命令，而是可包含在大多数Web SDK命令中的对象。

当您在不同的国家/地区拥有不同的网站或子域，或者您拥有多个Experience Platform沙盒来存储特定于不同业务部门的数据时，此对象非常有用。

>[!IMPORTANT]
>
>有关数据流覆盖的详细端到端配置说明，请参阅 [数据流配置覆盖](../../datastreams/overrides.md#configure-overrides) 文档。

数据流配置覆盖分为两步：

1. 首先，您必须在以下位置定义数据流配置覆盖 [数据流配置页面](../../datastreams/configure.md)，在数据流UI中。 请参阅 [数据流配置覆盖](../../datastreams/overrides.md#configure-overrides) 有关如何配置覆盖的说明文档。
2. 在UI中配置数据流覆盖后，必须通过以下方式之一将覆盖发送到Edge Network：
   * 通过Web SDK [标记扩展](#tag-extension).
   * 通过 `sendEvent` 或 `configure` Web SDK命令。
   * 通过Mobile SDK `sendEvent` 命令。

如果在Web SDK配置和特定命令(例如 [`sendEvent`](sendevent/overview.md))，则特定命令中的覆盖优先。

## 对象属性

以下属性在此对象中可用：

* **数据流覆盖**：将调用发送到其他数据流。 如果设置此值，则必须在此处设置的数据流中配置需要数据流配置的其他覆盖。
* **第三方ID同步容器**：Adobe Audience Manager中目标第三方ID同步容器的ID。 使用此字段之前，需要在数据流的设置中配置第三方ID容器覆盖。
* **目标资产令牌**：Adobe Target中目标资产的令牌。 使用此字段之前，需要先在数据流的设置中配置Target属性令牌覆盖。
* **报表包**：要在Adobe Analytics中覆盖的报表包ID。 使用此字段之前，需要先在数据流的设置中配置报表包覆盖。

## 通过Web SDK标记扩展向Edge Network发送数据流覆盖 {#tag-extension}

请参阅相关文档 [配置数据流覆盖](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides) 从Web SDK标记扩展获取详细的配置说明。

如果要从Web SDK标记扩展配置数据流覆盖，请在 **[!UICONTROL 数据流配置覆盖]** 时间 [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下滚动到 **[!UICONTROL 数据流配置覆盖]** 部分。 设置每个所需的覆盖值。
1. 单击 **[!UICONTROL 保存]**，然后发布更改。

如果只想为特定命令设置覆盖，请在标记规则的操作中设置每个所需字段。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 规则]**，然后选择所需的规则。
1. 下 [!UICONTROL 操作]，选择现有操作或创建操作。
1. 设置 [!UICONTROL 扩展名] 下拉字段至 **[!UICONTROL Adobe Experience Platform Web SDK]**，并设置 [!UICONTROL 操作类型] 到 **[!UICONTROL 发送事件]**.
1. 向下滚动到标记为的部分 **[!UICONTROL 数据流配置覆盖]**.
1. 将此部分中的每个字段设置为所需的覆盖值。
1. 单击 **[!UICONTROL 保留更改]**，然后运行发布工作流程。

为以下内容提供了单独的字段 [!UICONTROL 开发]， [!UICONTROL 暂存]、和 [!UICONTROL 生产] 环境。 确保为每个环境填写每个所需的字段。

## 通过Web SDK JavaScript库将覆盖发送到Edge Network {#library}

之后 [配置数据流覆盖](../../datastreams/overrides.md) 在数据收集UI中，您现在可以通过Web SDK JavaScript库将覆盖发送到Edge Network。

如果您使用的是Web SDK，请通过 `edgeConfigOverrides` 命令是激活数据流配置覆盖的第二步，也是最后一步。

数据流配置覆盖通过 `edgeConfigOverrides` Web SDK 命令发送到 Edge Network。此命令创建数据流覆盖，并将其传递给 [!DNL Edge Network] 在下一个命令中。 如果您使用 `configure` 命令，则会为每个请求传递覆盖。

此 `edgeConfigOverrides` 命令创建数据流覆盖，这些覆盖将传递给 [!DNL Edge Network] 在下一个命令中。

当使用 `configure` 命令发送配置覆盖时，它包含在以下 Web SDK 命令中。

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [configure](../commands/configure/overview.md)

全局指定的选项可由各个命令上的配置选项覆盖。

### 通过Web SDK发送配置覆盖 `sendEvent` 命令 {#send-event}

以下示例显示 `sendEvent` 命令中的配置覆盖的情况。

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
    datastreamId: "{DATASTREAM_ID}"
    com_adobe_experience_platform: {
      datasets: {
        event: {
          datasetId: "SampleEventDatasetIdOverride"
        }
      }
    },
    com_adobe_analytics: {
      reportSuites: [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
    },
    com_adobe_identity: {
      idSyncContainerId: "1234567"
    },
    com_adobe_target: {
      propertyToken: "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  }
});
```

| 参数 | 描述 |
|---|---|
| `edgeConfigOverrides.datastreamId` | 使用此参数可允许单个请求转到与 `configure`命令定义的数据流不同的数据流。 |
| `com_adobe_analytics.reportSuites[]` | 一个字符串数组，它确定要将Analytics数据发送到哪些报表包。 |
| `com_adobe_identity.idSyncContainerId` | 要在Audience Manager中使用的第三方ID同步容器。 |
| `com_adobe_target.propertyToken` | Adobe Target目标资产的令牌。 |

### 通过Web SDK发送配置覆盖 `configure` 命令 {#send-configure}

以下示例显示 `configure` 命令中的配置覆盖的情况。

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  datastreamId: "{DATASTREAM_ID}",
  orgId: "org",
  debugEnabled: true,
  edgeConfigOverrides: {
    "com_adobe_experience_platform": {
      "datasets": {
        "event": {
          datasetId: "SampleProfileDatasetIdOverride"
        }
      }
    },
    "com_adobe_analytics": {
      "reportSuites": [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
      ]
    },
    "com_adobe_identity": {
      "idSyncContainerId": "1234567"
    },
    "com_adobe_target": {
      "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  },
  onBeforeEventSend: function() { /* … */ });
};
```

| 参数 | 描述 |
|---|---|
| `edgeConfigOverrides.datastreamId` | 使用此参数可允许单个请求转到与 `configure`命令定义的数据流不同的数据流。 |
| `com_adobe_analytics.reportSuites[]` | 一个字符串数组，它确定要将Analytics数据发送到哪些报表包。 |
| `com_adobe_identity.idSyncContainerId` | 要在Audience Manager中使用的第三方ID同步容器。 |
| `com_adobe_target.propertyToken` | Adobe Target目标资产的令牌。 |