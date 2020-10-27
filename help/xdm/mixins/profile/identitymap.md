---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: IdentityMap混音
topic: overview
description: 此文档概述了XDM单个用户档案类。
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# [!UICONTROL IdentityMap] mixin

>[!NOTE]
>
>几个混音的名称已经更改。 有关详细信息，请 [参阅混合名称](../name-updates.md) 更新文档。

[!UICONTROL IdentityMap] 是类的标准混 [[!DNL XDM Individual Profile] 合](../../classes/individual-profile.md)。 混音提供单个映射字段，该字段包含由命名空间键入的一组用户标识。

>[!WARNING]
>
>系 `IdentityMap` 统在摄取身份数据时自动更新字段。 为了将此字段正确用于实 [时客户用户档案](../../../profile/home.md)，请不要尝试手动更新数据操作中字段的内容。

<img src="../../images/mixins/identitymap.png" width="600" /><br />

有关模式组合的更多信息，请 [参阅组合基础](../../schema/composition.md#identityMap) 中有关标识映射的部分。