---
title: 访问ECID
description: 了解如何从数据准备或标记访问Experience CloudID
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: e53ae6053a4b00e7e75242b95496c6795953005a
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 1%

---


# 访问ECID

[!DNL Experience Cloud Identity (ECID)]是用户访问您的网站时分配给用户的永久标识符。 在某些情况下，您可能希望访问[!DNL ECID]（例如，将其发送给第三方）。 另一个使用案例是在自定义XDM字段中设置[!DNL ECID]，并将其包含在身份映射中。

您可以通过用于数据收集[&#128279;](../../../../datastreams/data-prep.md)的数据准备（推荐）或通过标记来访问ECID。

## 通过数据准备访问ECID（首选方法） {#accessing-ecid-data-prep}

此方法使用数据收集[&#128279;](../../../../datastreams/data-prep.md)的数据准备来配置`ECID`的自定义映射。

请参阅用于数据收集[&#128279;](../../../../datastreams/data-prep.md)的数据准备文档，了解如何使用此功能。

如果您要在自定义XDM字段中设置ECID，并且要在标识映射中设置ECID，则可以通过将`source`设置为以下路径来实现此目的：

```js
xdm.identityMap.ECID[0].id
```

然后，将目标设置为字段类型为`string`的XDM路径。

![](./assets/access-ecid-data-prep.png)

## 标记

如果您需要在客户端访问[!DNL ECID]，请使用如下所述的标记方法。

1. 请确保您的属性配置为启用[规则组件排序](../../../ui/managing-resources/rules.md#sequencing)。
1. 创建新规则。 此规则应仅用于捕获[!DNL ECID]，而不执行任何其他重要操作。
1. 将[!UICONTROL Library Loaded]事件添加到规则中。
1. 使用以下代码将[!UICONTROL Custom Code]操作添加到规则（假定您为SDK实例配置的名称为`alloy`，并且还没有具有相同名称的数据元素）：

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 保存规则。

然后，您应该能够使用`%ECID%`或`_satellite.getVar("ECID")`访问后续规则中的[!DNL ECID]，就像访问任何其他数据元素一样。
