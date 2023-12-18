---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；个人配置文件；字段；架构；架构；架构设计；字段组；字段组；iab；tcf；同意；
solution: Experience Platform
title: IAB TCF 2.0配置文件架构的同意字段组
description: 了解XDM Individual Profile类的IAB TCF 2.0同意架构字段组。
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# [!UICONTROL IAB TCF 2.0同意] 配置文件架构的字段组

>[!NOTE]
>
>本文档涵盖 [!UICONTROL IAB TCF 2.0同意] xdm Individual Profile类的架构字段组。 有关用于XDM ExperienceEvent类的字段组，请参阅以下内容 [文档](../event/iab.md) 而是。

[!UICONTROL IAB TCF 2.0同意] 是的标准架构字段组 [[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md) 用于捕获带有时间戳的系列IAB同意字符串，以跟踪随时间变化的同意更改模式。

![](../../images/field-groups/iab-profile.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `identityPrivacyInfo` | 地图 | 映射类型对象，用于将客户的各个标识值与不同的TCF同意字符串相关联。 下面提供了此对象结构的示例。 |

{style="table-layout:auto"}

以下JSON演示了 `identityPrivacyInfo` 映射。

```json
{
  "identityPrivacyInfo": {
    "ECID": {
      "13782522493631189": {
        "identityIABConsent": {
          "consentTimestamp": "2020-04-11T05:05:05Z",
          "consentString": {
            "consentStandard": "IAB TCF",
            "consentStandardVersion": "2.0",
            "consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
            "gdprApplies": true,
            "containsPersonalData": false
          }
        }
      }
    }
  }
}
```

如示例所示，每个根级别键为 `xdm:identityPrivacyInfo` 与Identity Service识别的身份命名空间相对应。 反过来，每个命名空间属性必须至少有一个子属性，其键与该命名空间对应的客户标识值匹配。 在此示例中，客户使用Experience CloudID (`ECID`)的值 `13782522493631189`.

>[!NOTE]
>
>虽然上述示例使用单个命名空间/值对来表示客户的身份，但您可以为其他命名空间添加其他键，并且每个命名空间可以有多个身份值，每个值都有自己的一组TCF同意首选项。

对于每个标识值，使用 `identityIABConsent` 必须提供属性，该属性为身份提供TCF同意值。 此属性的值必须符合 [[!UICONTROL 同意字符串] 数据类型](../../data-types/consent-string.md).

请参阅指南，网址为 [平台中的IAB TCF 2.0支持](../../../landing/governance-privacy-security/consent/iab/overview.md) 以了解有关此字段组用例的更多信息。 有关字段组本身的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
