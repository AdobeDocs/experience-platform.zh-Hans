---
title: edgeConfigOverrides
description: 为实施配置数据流覆盖。
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# `edgeConfigOverrides` （`configure`命令）

`edgeConfigOverrides`对象允许您覆盖在当前页面上运行的命令的配置设置。 当您在不同的国家/地区拥有不同的网站或子域，或者您拥有多个Experience Platform沙盒来存储特定于不同业务部门的数据时，此对象非常有用。 如果只想覆盖页面上单个命令的配置设置，请考虑在[`edgeConfigOverrides`命令`sendEvent`中使用](../sendevent/edgeconfigoverrides.md)对象。

数据流配置覆盖过程包括两个主要步骤：

1. 首先，当在数据流UI中[配置数据流](/help/datastreams/configure.md)时，必须定义数据流配置覆盖。 有关如何配置覆盖的说明，请参阅数据流文档中的[数据流配置覆盖](/help/datastreams/overrides.md)。
1. 在数据流用户界面中配置数据流覆盖后，您可以配置`edgeConfigOverrides`对象。

当您在`edgeConfigOverrides`命令中设置`configure`对象时，它将应用于发送到Adobe的所有数据。 以下命令&#x200B;_也_&#x200B;支持`edgeConfigOverrides`对象：

* [&#39;sendEvent&#39;](../sendevent/edgeconfigoverrides.md)
* [&#39;setConsent&#39;](../setconsent.md)
* [&#39;getIdentity&#39;](../getidentity.md)
* [&#39;appendIdentityToUrl&#39;](../appendidentitytourl.md)

如果同时设置了上述任何命令中的`edgeConfigOverrides`设置，则优先于`edgeConfigOverrides`命令中的`configure`对象。 如果这些命令中的任何命令不包含`edgeConfigOverrides`对象，则使用`edgeConfigOverrides`命令中的`configure`对象。

## 示例

如果您的数据流配置启用了所有受支持的服务，则以下示例将覆盖此设置并禁用所有服务。

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77"
        }
      },
      com_adobe_edge_ode: {
        enabled: false
      },
      com_adobe_edge_segmentation: {
        enabled: false
      },
      com_adobe_edge_destinations: {
        enabled: false
      },
      com_adobe_edge_ajo: {
        enabled: false
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["exampleoverridersid","exampleoverridersid2"]
    },
    com_adobe_identity: {
      idSyncContainerId: 34373
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94"
    },
    com_adobe_audience_manager: {
      enabled: false
    },
    com_adobe_launch_ssf: {
      enabled: false
    }
  }
});
```

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| **`orgId`** | `string` | 您公司的IMS组织ID。 |
| **`datastreamId`** | `string` | 要将数据发送到的数据流ID。 |
| **`com_adobe_experience_platform`** | `object` | 为Adobe Experience Platform服务定义动态数据流配置。 |
| **`com_adobe_experience_platform.enabled`** | `boolean` | 确定是否将事件发送到Adobe Experience Platform。 |
| **`com_adobe_experience_platform.datasets`** | `object` | 定义用于事件的数据集。 |
| **`com_adobe_experience_platform.com_adobe_edge_ode.enabled`** | `boolean` | 确定是否将事件发送到Offer Decisioning。 |
| **`com_adobe_experience_platform.com_adobe_edge_segmentation.enabled`** | `boolean` | 确定是否将事件发送到Edge分段。 |
| **`com_adobe_experience_platform.com_adobe_edge_destinations.enabled`** | `boolean` | 确定是否将事件发送到Edge目标。 |
| **`com_adobe_experience_platform.com_adobe_edge_ajo.enabled`** | `boolean` | 确定事件是否在Adobe Journey Optimizer发送。 |
| **`com_adobe_analytics.enabled`** | `boolean` | 确定是否将事件发送到Adobe Analytics。 |
| **`com_adobe_analytics.reportSuites[]`** | `string[]` | 一个字符串数组，它确定要将Analytics数据发送到的报表包。 |
| **`com_adobe_audience_manager.enabled`** | `boolean` | 确定是否将事件发送到Adobe Audience Manager。 |
| **`com_adobe_identity.idSyncContainerId`** | `integer` | 您要在Audience Manager中使用的第三方ID同步容器。 需要`com_adobe_audience_manager.enabled`设置为`true`。 否则，将禁用Audience Manager服务。 |
| **`com_adobe_target.enabled`** | `boolean` | 确定是否将事件发送到Adobe Target。 |
| **`com_adobe_target.propertyToken`** | `string` | Adobe Target目标资产的令牌。 |
| **`com_adobe_launch_ssf`** | `boolean` | 确定是否将事件发送到服务器端转发。 |

## 使用Web SDK标记扩展配置覆盖

配置标记扩展时，此字段的Web SDK标记扩展等效项位于[配置覆盖](/help/tags/extensions/client/web-sdk/configure/configuration-overrides.md)下。
