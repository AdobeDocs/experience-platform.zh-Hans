---
solution: Experience Platform
title: 区段成员资格详细信息架构字段组
description: 了解“区段成员资格详细信息”架构字段组。
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 1%

---


# [!UICONTROL 区段成员资格详细信息]架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 有关详细信息，请参阅有关[字段组名称更新](../name-updates.md)的文档。

[!UICONTROL 区段成员资格详细信息]是[[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md)的标准架构字段组。 字段组提供单个映射字段，用于捕获有关区段成员资格的信息，包括个人属于哪些区段、上次资格取得时间和成员资格有效期截止日期。

>[!WARNING]
>
>虽然`segmentMembership`字段必须使用此字段组手动添加到您的配置文件架构中，但您不应尝试手动填充或更新此字段。 在执行分段作业时，系统会自动更新每个配置文件的`segmentMembership`映射。

![配置文件分段](../../images/data-types/profile-segmentation.png){width=400}

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `segmentMembership` | 地图 | 描述个人区段成员资格的映射对象。 此对象的结构详见下文。 |

{style="table-layout:auto"}

以下是系统为特定配置文件填充的示例`segmentMembership`映射。 区段成员资格按命名空间排序，如对象的根级别键值所示。 反过来，每个命名空间下的各个键表示配置文件所属区段的ID。 每个区段对象都包含多个子字段，这些子字段提供有关成员资格的更多详细信息：

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadBooleanValue": true,
          "xdm:payloadType": "boolean"
        }
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "xdm:version": "3",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2018-04-27T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadPropensityValue": 0.5,
          "xdm:payloadType": "propensity"
        }
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "xdm:version": "1",
        "xdm:lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "xdm:validUntil": "2017-12-26T15:52:25+00:00",
        "xdm:status": "exited"
      }
    }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `xdm:version` | 此配置文件符合条件的区段的版本。 |
| `xdm:lastQualificationTime` | 此配置文件上次符合区段资格的时间戳。 |
| `xdm:validUntil` | 不再假定区段成员资格有效的时间戳。 对于外部受众，如果未设置此字段，则区段成员资格将仅从`lastQualificationTime`中保留30天。 |
| `xdm:status` | 一个字符串字段，指示区段成员资格是否已在当前请求中实现。 接受以下值： <ul><li>`realized`：配置文件符合区段的条件。</li><li>`exited`：作为当前请求的一部分，配置文件正在退出该区段。</li></ul> |
| `xdm:payload` | 某些区段成员资格包括一个有效负荷，该有效负荷描述与成员资格直接相关的其他值。 每个成员资格只能提供一个给定类型的有效负荷。 `xdm:payloadType`指示有效负载的类型（`boolean`、`number`、`propensity`或`string`），而它的同级属性为有效负载类型提供值。 |

{style="table-layout:auto"}

>[!NOTE]
>
>任何基于`lastQualificationTime`且处于`exited`状态超过30天的区段成员资格都将被删除。

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
