---
title: '访问ECID '
description: Adobe Experience Platform Web SDK扩展在标记中利用ECID
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 5%

---


# 访问ECID

[!DNL Experience Cloud Identity (ECID)]是网站访客的永久标识符。 在某些情况下，您可能希望访问ECID（例如，将其发送给第三方）。

要在标记中访问ECID，Adobe建议执行以下操作：

1. 确保为您的资产配置了[规则组件排序](https://experienceleague.adobe.com/docs/launch/using/ui/rules.html?lang=en#rule-component-sequencing)。
1. 创建新规则。
1. 向规则中添加[!UICONTROL Library Loaded]事件。
1. 将[!UICONTROL Custom Condition]操作添加到具有以下代码的规则中（假定您为SDK实例配置的名称为`alloy`）：

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 保存规则。

然后，您应该能够像使用任何其他数据元素一样，使用`%ECID%`或`_satellite.getVar("ECID")`在后续规则中访问ECID。
