---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；个人配置文件；字段；架构；架构；区段；区段成员资格；区段成员资格；架构设计；映射；映射；
solution: Experience Platform
title: 区段成员资格详细信息架构字段组
topic-legacy: overview
description: 本文档概述了区段成员资格详细信息架构字段组。
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 2%

---


# [!UICONTROL 区段成员资] 格详细信息架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 有关详细信息，请参阅[字段组名称更新](../name-updates.md)上的文档。

[!UICONTROL 区段成] 员资格详细说明类的标准架构字 [[!DNL XDM Individual Profile] 段组](../../classes/individual-profile.md)。字段组提供单个映射字段，用于捕获有关区段成员资格的信息，包括个人所属的区段、上次资格鉴定时间以及成员资格在有效期间的信息。

>[!WARNING]
>
>必须使用此字段组将`segmentMembership`字段手动添加到您的用户档案架构，但不应尝试手动填充或更新此字段。 在执行分段作业时，系统会自动更新每个用户档案的`segmentMembership`映射。

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `segmentMembership` | 地图 | 描述个人区段成员资格的映射对象。 此对象的结构在下文中有详细描述。 |

{style=&quot;table-layout:auto&quot;}

以下是`segmentMembership`映射示例，该示例映射系统已为特定配置文件填充。 区段成员关系按命名空间排序，如对象的根级别键所示。 反过来，每个命名空间下的各个键都表示用户档案所属区段的ID。 每个区段对象包含多个子字段，这些子字段提供了有关成员资格的更多详细信息：

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "existing",
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
| `xdm:version` | 此用户档案符合条件的区段版本。 |
| `xdm:lastQualificationTime` | 此用户档案上次符合区段资格条件的时间戳。 |
| `xdm:validUntil` | 不再假定区段成员资格有效的时间戳。 |
| `xdm:status` | 指示区段成员资格是否已作为当前请求的一部分实现。 接受以下值： <ul><li>`existing`:在请求之前，用户档案已经是区段的一部分，并将继续保持其会员资格。</li><li>`realized`:用户档案将在当前请求中输入区段。</li><li>`exited`:该用户档案将作为当前请求的一部分退出该区段。</li></ul> |
| `xdm:payload` | 某些区段成员资格包括描述与成员资格直接相关的其他值的有效负载。 每个成员只能提供给定类型的有效负荷。 `xdm:payloadType` 指示有效负载类型(`boolean`、 `number`、 `propensity`或 `string`)，而其同级属性为有效负载类型提供值。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
