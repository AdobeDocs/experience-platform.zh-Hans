---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；个人配置文件；字段；架构；架构；身份映射；身份映射；架构设计；映射；映射；合并架构；合并
title: IdentityMap架构字段组
description: 了解XDM Individual Profile类。
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---

# [!UICONTROL IdentityMap]架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 有关详细信息，请参阅有关[字段组名称更新](../name-updates.md)的文档。

[!UICONTROL IdentityMap]是[[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md)的标准架构字段组。 字段组提供单个映射字段，该字段包含一组由命名空间键控的用户身份。

![架构字段组[!UICONTROL IdentityMap]的图表](../../images/field-groups/identitymap.png)

请参阅架构组合](../../schema/composition.md#identityMap)的[基础知识中关于标识映射的部分，以了解有关其用例的更多信息，包括其优点和缺点。

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

有关字段组的更多详细信息，请参阅公共XDM存储库中的[完整架构](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json)。
