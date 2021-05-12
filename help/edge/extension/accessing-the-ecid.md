---
title: '访问ECID '
description: Adobe Experience Platform Web SDK扩展利用Adobe Experience Platform Launch中的ECID
source-git-commit: 3002036d7366e2f7310aa62e53c7c391d9ff7a07
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 5%

---


# 访问ECID

[!DNL Experience Cloud Identity (ECID)]是您网站访客的永久标识符。 在某些情况下，您可能希望访问ECID（例如，将其发送给第三方）。

要在Adobe Experience Platform Launch中访问ECID，Adobe建议：

1. 确保您的属性已配置[规则组件序列](https://experienceleague.adobe.com/docs/launch/using/ui/rules.html?lang=en#rule-component-sequencing)。
1. 创建新规则。
1. 向规则添加[!UICONTROL Library Loaded]事件。
1. 将[!UICONTROL Custom Condition]操作添加到规则中，其代码如下（假定您为SDK实例配置的名称为`alloy`）：

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. 保存规则。

然后，您应该能够像访问任何其他数据元素一样使用`%ECID%`或`_satellite.getVar("ECID")`在后续规则中访问ECID。
