---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;segment;segmentMembership;segment membership;Schema design;map;Map;
solution: Experience Platform
title: 用户档案分段混合
topic: overview
description: 此文档概述了XDM单个用户档案类。
translation-type: tm+mt
source-git-commit: 53575488c08f73a65a7f1cc5f803f9ead707ae48
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---


# [!UICONTROL 用户档案分段] mixin

[!UICONTROL 用户档案分段] 是类的标准混合 [[!DNL XDM Individual Profile] 项](../../classes/individual-profile.md)。 混音提供单个地图字段，该字段捕获有关区段成员资格的信息，包括个人所属的区段、最后的资格时间以及会员资格的有效期到何时。

>[!WARNING]
>
>虽然必 `segmentMembership` 须使用此混音将字段手动添加到用户档案模式，但您不应尝试手动填充或更新此字段。 当执行分段作业时， `segmentMembership` 系统会自动更新每个用户档案的映射。

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `segmentMembership` | 地图 | 描述个人区段成员关系的映射对象。 此对象的结构在下面有详细说明。 |

以下是系统已 `segmentMembership` 为特定用户档案填充的示例映射。 段成员关系按命名空间排序，如对象的根级键所示。 反过来，每个命名空间下的各个键代表用户档案是其成员的段的ID。 每个区段对象都包含多个子字段，这些子字段提供有关成员关系的更多详细信息：

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
| `xdm:version` | 此用户档案符合的区段版本。 |
| `xdm:lastQualificationTime` | 此用户档案上次限定区段的时间的时间戳。 |
| `xdm:validUntil` | 区段成员资格不再被视为有效的时间戳。 |
| `xdm:status` | 指示区段成员资格是否已作为当前请求的一部分实现。 接受以下值： <ul><li>`existing`:在请求之前，用户档案已经是该细分的一部分，并继续保持其会员资格。</li><li>`realized`:用户档案将输入作为当前请求一部分的区段。</li><li>`exited`:用户档案作为当前请求的一部分退出区段。</li></ul> |
| `xdm:payload` | 某些区段成员资格包含描述与成员资格直接相关的其他值的有效负荷。 每个会员资格只能提供一个给定类型的有效负荷。 `xdm:payloadType` 指示有效负荷的类`boolean`型 `number`(、 `propensity`、或 `string`)，而其同级属性提供有效负荷类型的值。 |

有关混音的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
