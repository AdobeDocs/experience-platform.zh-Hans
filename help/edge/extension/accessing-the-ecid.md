---
title: 访问ECID
description: 了解如何从数据准备或标记中访问Experience CloudID
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: dee04f2cdeb9057ac10e27a17f9db3f065712618
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---


# 访问ECID

的 [!DNL Experience Cloud Identity (ECID)] 是在用户访问您的网站时分配给用户的永久标识符。 在某些情况下，您可能希望访问 [!DNL ECID] （例如，将其发送给第三方）。 另一个用例是设置 [!DNL ECID] 在自定义XDM字段中，以及将其包含在身份映射中之外。

您可以通过 [为数据收集准备数据](../datastreams/data-prep.md) （推荐）或通过标记。

## 通过数据准备（首选方法）访问ECID {#accessing-ecid-data-prep}

如果您要在自定义XDM字段中设置ECID，则除了要在身份映射中设置ECID之外，还可以通过将 `source` 路径：

```js
xdm.identityMap.ECID[0].id
```

然后，将目标设置为字段类型为的XDM路径 `string`.

![](./assets/access-ecid-data-prep.png)

## 标记

如果您需要访问 [!DNL ECID] 在客户端，使用如下所述的标记方法。

1. 确保您的资产已配置为 [规则组件排序](../../tags/ui/managing-resources/rules.md#sequencing) 已启用。
1. 创建新规则。
1. 添加 [!UICONTROL Library Loaded] 事件。
1. 添加 [!UICONTROL 自定义条件] 使用以下代码对规则执行操作(假定您为SDK实例配置的名称为 `alloy`):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 保存规则。

然后，您应该能够访问 [!DNL ECID] 在后续规则中使用 `%ECID%` 或 `_satellite.getVar("ECID")`，类似于访问任何其他数据元素。
