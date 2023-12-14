---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；个人配置文件；字段；架构；架构；身份映射；身份映射；架构设计；映射；映射；合并架构；合并
title: IdentityMap架构字段组
description: 本文档概述了XDM Individual Profile类。
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: 43b3b79a4d24fd92c7afbf9ca9c83b0cbf80e2c2
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# [!UICONTROL Identitymap] 架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 查看文档 [字段组名称更新](../name-updates.md) 以了解更多信息。

[!UICONTROL Identitymap] 是的标准架构字段组 [[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md). 字段组提供单个映射字段，该字段包含一组由命名空间键控的用户身份。

![的图表 [!UICONTROL Identitymap] 架构字段组](../../images/field-groups/identitymap.png)

请参阅中有关身份映射的部分 [模式组合基础](../../schema/composition.md#identityMap) 以了解关于它们的用例，包括其优点和缺点的信息。

**示例**

```JSON
{
    "identityMap":{
        "ECID":[
            {
                "id":"83238819066235616291057085344313877718",
                "authenticatedState":"ambiguous",
                "primary":true
            }
        ]
    }
}
```

有关字段组的更多详细信息，请参阅 [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json) 在公共XDM存储库中。
