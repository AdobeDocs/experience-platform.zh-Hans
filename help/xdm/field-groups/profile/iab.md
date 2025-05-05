---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；个人配置文件；字段；架构；架构；架构设计；字段组；字段组；iab；tcf；同意；
solution: Experience Platform
title: IAB TCF 2.0配置文件架构的同意字段组
description: 了解XDM Individual Profile类的IAB TCF 2.0同意架构字段组。
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 1%

---

# 配置文件架构的[!UICONTROL IAB TCF 2.0同意]字段组

>[!NOTE]
>
>本文档介绍XDM Individual Profile类的[!UICONTROL IAB TCF 2.0 Consent]架构字段组。 有关用于XDM ExperienceEvent类的字段组，请改为参阅以下[文档](../event/iab.md)。

[!UICONTROL IAB TCF 2.0同意]是[[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md)的标准架构字段组，用于捕获带有时间戳的系列IAB同意字符串，以跟踪一段时间内同意更改的模式。

![](../../images/field-groups/iab-profile.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `identityPrivacyInfo` | 地图 | 映射类型对象，用于将客户的各个标识值与不同的TCF同意字符串相关联。 下面提供了此对象结构的示例。 |

{style="table-layout:auto"}

以下JSON演示了`identityPrivacyInfo`映射的结构。

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

如示例所示，`xdm:identityPrivacyInfo`的每个根级别键均与标识服务识别的标识命名空间相对应。 反过来，每个命名空间属性必须至少有一个子属性，其键与该命名空间对应的客户标识值匹配。 在此示例中，客户的Experience Cloud ID (`ECID`)值为`13782522493631189`。

>[!NOTE]
>
>虽然上述示例使用单个命名空间/值对来表示客户的身份，但您可以为其他命名空间添加其他键，并且每个命名空间可以有多个身份值，每个值都有自己的一组TCF同意首选项。

对于每个标识值，必须提供`identityIABConsent`属性，该属性为标识提供TCF同意值。 此属性的值必须符合[[!UICONTROL 同意字符串]数据类型](../../data-types/consent-string.md)。

有关此字段组用例的更多信息，请参阅Experience Platform[&#128279;](../../../landing/governance-privacy-security/consent/iab/overview.md)中支持IAB TCF 2.0的指南。 有关字段组本身的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
