---
title: edgeConfigOverrides
description: 仅为sendEvent命令配置数据流覆盖。
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# `edgeConfigOverrides` （`sendEvent`命令）

`edgeConfigOverrides`对象允许您仅覆盖当前`sendEvent`命令的配置设置。 当您希望使用与其他Web SDK实施不同的配置设置运行的同一页面上有特定命令时，此对象非常有用。 如果要覆盖给定页面上所有命令的配置设置，请考虑在[`edgeConfigOverrides`命令`configure`中使用](../configure/edgeconfigoverrides.md)对象。

总体数据流配置覆盖过程包括两个主要步骤：

1. 首先，当在数据流UI中[配置数据流](/help/datastreams/configure.md)时，必须定义数据流配置覆盖。 有关如何配置覆盖的说明，请参阅数据流文档中的[数据流配置覆盖](/help/datastreams/overrides.md)。
1. 在数据流用户界面中配置数据流覆盖后，您可以配置`edgeConfigOverrides`对象。

请注意，`configure`命令还支持`edgeConfigOverrides`对象；请参阅[`edgeConfigOverrides`](../configure/edgeconfigoverrides.md)命令下的`configure`。 如果同时设置了`edgeConfigOverrides`命令中的`sendEvent`对象，则该对象优先于`edgeConfigOverrides`命令中的`configure`对象。

## 示例

如果您的数据流配置启用了所有受支持的服务，则以下示例将覆盖此设置并禁用所有服务（请参阅每个服务上的`enabled: false`设置）。 此对象支持与[`edgeConfigOverrides`](../configure/edgeconfigoverrides.md)命令中的`configure`对象相同的属性。

```js
alloy("sendEvent", {
  renderDecisions: true,
  edgeConfigOverrides: {
    datastreamId: "bfa8fe21-6157-42d3-b47a-78310920b39d",
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f949a8a6891ca8a28911",
        },
      },
      com_adobe_edge_ode: {
        enabled: false,
      },
      com_adobe_edge_segmentation: {
        enabled: false,
      },
      com_adobe_edge_destinations: {
        enabled: false,
      },
      com_adobe_edge_ajo: {
        enabled: false,
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["examplersid3"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34374,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "f3fd55e1-a06d-8650-9aa5-c8356c6e2223",
    },
    com_adobe_audience_manager: {
      enabled: false,
    },
    com_adobe_launch_ssf: {
      enabled: false,
    },
  },
});
```

## 使用Web SDK标记扩展的数据流配置覆盖

在配置“[”操作时，此对象的Web SDK标记扩展等效项是](/help/tags/extensions/client/web-sdk/actions/send-event.md#datastream-configuration-overrides)数据流配置覆盖[!UICONTROL Send event]部分。
