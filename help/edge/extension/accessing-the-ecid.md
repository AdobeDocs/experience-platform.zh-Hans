---
title: 访问ECID
description: 了解如何在Adobe Experience Platform标记中访问Experience CloudID(ECID)
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 5%

---


# 访问ECID

的 [!DNL Experience Cloud ID (ECID)] 是可帮助您识别网站访客的永久Experience Cloud标识符。 在某些情况下（例如将标识符发送到第三方平台），您可能需要访问 [!DNL ECID].

访问 [!DNL ECID] 在标记中，按照以下步骤操作：

1. 确保您的资产已配置为 [规则组件排序](../../tags/ui/managing-resources/rules.md#sequencing) 已启用。
2. 创建新规则。
3. 添加 [!UICONTROL Library Loaded] 事件。
4. 添加 [!UICONTROL 自定义条件] 对规则执行操作，并使用以下代码(假定您为SDK实例配置的名称为 `alloy`):

   ```javascript
   return alloy("getIdentity")
       .then(function(result) {
           _satellite.setVar("ECID", result.identity.ECID);
       });
   ```

5. 保存规则。

现在，您应该能够访问 [!DNL ECID] 在后续规则中，使用 `%ECID%` 或 `_satellite.getVar("ECID")`，与访问任何其他数据元素的方式类似。
