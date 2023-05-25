---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；个人配置文件；字段；架构；架构；区段；segmentMembership；区段成员资格；架构设计；映射；映射；
solution: Experience Platform
title: 区段成员资格详细信息架构字段组
description: 本文档概述了“区段成员资格详细信息”架构字段组。
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: 229dd08bc5d5dfab068db3be84ad20d10992fd31
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---


# [!UICONTROL 区段成员资格详细信息] 架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 查看文档 [字段组名称更新](../name-updates.md) 了解更多信息。

[!UICONTROL 区段成员资格详细信息] 是的标准架构字段组 [[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md). 字段组提供单个映射字段，用于捕获有关区段成员资格的信息，包括个人属于哪些区段、上次资格取得时间和成员资格有效期结束时间。

>[!WARNING]
>
>而 `segmentMembership` 字段必须使用此字段组手动添加到您的配置文件架构中，您不应尝试手动填充或更新此字段。 系统会自动更新 `segmentMembership` 在执行分段作业时映射每个配置文件。

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `segmentMembership` | 地图 | 描述个人区段成员资格的映射对象。 此对象的结构详见下文。 |

{style="table-layout:auto"}

以下是示例 `segmentMembership` 系统为特定配置文件填充的映射。 区段成员资格按命名空间排序，如对象的根级别键值所示。 反过来，每个命名空间下的各个键代表配置文件所属的区段的ID。 每个区段对象都包含多个子字段，这些子字段提供有关成员资格的更多详细信息：

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
| `xdm:lastQualificationTime` | 上次此配置文件符合区段资格的时间戳。 |
| `xdm:validUntil` | 区段成员资格何时不再被视为有效的时间戳。 对于外部受众，如果未设置此字段，则区段成员资格将仅保留30天，从 `lastQualificationTime`. |
| `xdm:status` | 一个字符串字段，指示区段成员资格是否作为当前请求的一部分实现。 接受以下值： <ul><li>`realized`：用户档案符合区段的条件。</li><li>`exited`：用户档案将作为当前请求的一部分退出区段。</li></ul> |
| `xdm:payload` | 某些区段成员资格包括一个有效负荷，该有效负荷描述与成员资格直接相关的其他值。 每个成员资格只能提供一个给定类型的有效负载。 `xdm:payloadType` 指示有效负载的类型(`boolean`， `number`， `propensity`，或 `string`)，而其同级属性则为有效负载类型提供值。 |

{style="table-layout:auto"}

>[!NOTE]
>
>中的任何区段成员资格 `exited` 超过30天的状态，基于 `lastQualificationTime`，将被删除。

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
