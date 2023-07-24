---
title: 访问ECID
description: 了解如何从数据准备或标记访问Experience CloudID
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---


# 访问ECID

此 [!DNL Experience Cloud Identity (ECID)] 是用户访问您的网站时分配给用户的永久标识符。 在某些情况下，您可能希望访问 [!DNL ECID] （例如，发送给第三方）。 另一个用例是设置 [!DNL ECID] 在自定义XDM字段中，以及标识映射。

您可以通过以下任一方式访问ECID [为数据收集准备数据](../../../../datastreams/data-prep.md) （推荐）或通过标记进行标记。

## 通过数据准备访问ECID（首选方法） {#accessing-ecid-data-prep}

如果您希望在自定义XDM字段中设置ECID，则除了在身份映射中使其可用外，您还可以通过设置 `source` 到以下路径：

```js
xdm.identityMap.ECID[0].id
```

然后，将目标设置为字段为类型的XDM路径 `string`.

![](./assets/access-ecid-data-prep.png)

## 标记

如果您需要访问 [!DNL ECID] 在客户端，使用如下所述的标记方法。

1. 确保您的资产配置有 [规则组件排序](../../../ui/managing-resources/rules.md#sequencing) 已启用。
1. 创建新规则。
1. 添加 [!UICONTROL 库已加载] 事件到规则。
1. 添加 [!UICONTROL 自定义完成情况] 对规则的操作，代码如下(假定您为SDK实例配置的名称为 `alloy`)：

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 保存规则。

然后，您应该能够访问 [!DNL ECID] 在后续规则中，使用 `%ECID%` 或 `_satellite.getVar("ECID")`，就像您会访问任何其他数据元素一样。
