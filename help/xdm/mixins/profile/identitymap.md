---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；个人用户档案；字段；模式;模式；标识映射；标识映射；模式设计；映射；映射；合并模式;合并
solution: Experience Platform
title: IdentityMap Mixin
topic-legacy: overview
description: 本文档概述了XDM单个用户档案类。
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# [!UICONTROL IdentityMap] mixin

>[!NOTE]
>
>几个混音的名称已经更改。 有关详细信息，请参阅[mixin name updates](../name-updates.md)上的文档。

[!UICONTROL IdentityMap] 是班级的标准混 [[!DNL XDM Individual Profile] 音](../../classes/individual-profile.md)。混音提供单个映射字段，该字段包含由命名空间键入的一组用户标识。

>[!WARNING]
>
>系统会在摄取标识数据时自动更新`IdentityMap`字段。 为了将此字段正确用于[实时客户用户档案](../../../profile/home.md)，请不要尝试手动更新数据操作中字段的内容。

<img src="../../images/mixins/identitymap.png" width="600" /><br />

有关模式组合的用例的详细信息，请参阅[基础知识](../../schema/composition.md#identityMap)中有关标识映射的部分。
