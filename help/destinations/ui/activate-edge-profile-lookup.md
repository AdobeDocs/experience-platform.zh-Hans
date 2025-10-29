---
title: 实时查找边缘配置文件属性
description: 了解如何使用自定义Personalization目标和Edge Network API实时查找边缘配置文件属性
type: Tutorial
exl-id: e185d741-af30-4706-bc8f-d880204d9ec7
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1843'
ht-degree: 1%

---

# 实时查找边缘上的配置文件属性

Adobe Experience Platform使用[实时客户个人资料](../../profile/home.md)作为所有个人资料数据的单一真实来源。 为了快速实时检索数据，它使用[边缘配置文件](../../profile/edge-profiles.md)，这些是分布在[Edge Network](../../collection/home.md#edge)中的轻量级配置文件。 这允许快速实时的个性化用例。

## 用例 {#use-cases}

以下是边缘配置文件查找有用的两个用例。

* **实时Personalization**：从边缘配置文件中快速检索配置文件信息，以个性化用户在您网站上的体验。
* **客户支持**：当客户致电支持中心代理时，实时检索配置文件信息。

本页介绍要实时查找边缘用户档案数据、提供个性化体验或通过下游应用程序告知决策规则必须执行的步骤。

## 术语和先决条件 {#prerequisites}

在配置本页中所述的用例时，您将使用以下Experience Platform组件：

* [数据流](../../datastreams/overview.md)：数据流接收来自Web SDK的传入事件数据并使用边缘配置文件数据进行响应。
* [合并策略](../../segmentation/ui/segment-builder.md#merge-policies)：您将创建一个[!UICONTROL Active-On-Edge]合并策略，以确保边缘配置文件使用正确的配置文件数据。
* [自定义Personalization连接](../catalog/personalization/custom-personalization.md)：您将配置新的自定义个性化连接，以将配置文件属性发送到Edge Network。
* [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)：您将使用Edge Network API [交互式数据收集](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)功能从Edge配置文件中快速检索配置文件属性。

## 性能护栏 {#guardrails}

Edge配置文件查找用例受下表所述的特定性能护栏的约束。 有关Edge Network API护栏的更多详细信息，请参阅护栏[文档页面](https://developer.adobe.com/data-collection-apis/docs/getting-started/guardrails/)。

| Edge Network服务 | Edge区段 | 每秒请求数 |
|---------|----------|---------|
| 通过[Edge Network API](../catalog/personalization/custom-personalization.md)的[自定义个性化目标](https://developer.adobe.com/data-collection-apis/docs/api/) | 是 | 1500 |
| 通过[Edge Network API](../catalog/personalization/custom-personalization.md)的[自定义个性化目标](https://developer.adobe.com/data-collection-apis/docs/api/) | 否 | 1500 |

## 步骤1：创建和配置数据流 {#create-datastream}

按照[数据流配置](../../datastreams/configure.md#create-a-datastream)文档中的步骤使用以下&#x200B;**[!UICONTROL Service]**&#x200B;设置创建新数据流：

* **[!UICONTROL Service]**: [!UICONTROL Adobe Experience Platform]
* **[!UICONTROL Personalization Destinations]**：已启用
* **[!UICONTROL Edge Segmentation]**：如果需要边缘分段，请启用此选项。 如果您只想在边缘上查找配置文件属性，但不想根据边缘配置文件执行任何分段，则将此选项保留为禁用。


<!-- >[!IMPORTANT]
>
>Enabling edge segmentation limits the maximum number of lookup requests to 1500 request per second. If you need a higher request throughput, disable edge segmentation for your datastream. See the [guardrails documentation](../guardrails.md#edge-destinations-activation) for detailed information. -->

    ![显示数据流配置屏幕的Experience Platform UI图像。](../assets/ui/activate-edge-profile-lookup/datastream-config.png)


## 步骤2：配置受众以进行Edge评估 {#audience-edge-evaluation}

在Edge上查找配置文件属性时，需要配置受众以进行Edge评估。

确保您计划激活的受众已将[Edge上的活动合并策略](../../segmentation/ui/segment-builder.md#merge-policies)设置为默认值。 [!DNL Active-On-Edge]合并策略确保在[边缘上持续评估受众](../../segmentation/methods/edge-segmentation.md)，并且可用于实时个性化用例。

按照[创建合并策略](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)中的说明进行操作，并确保启用&#x200B;**[!UICONTROL Active-On-Edge Merge Policy]**&#x200B;切换开关。

>[!IMPORTANT]
>
>如果您的受众使用不同的合并策略，您将无法从边缘检索配置文件属性，也无法执行边缘配置文件查找。

## 步骤3：将配置文件属性数据发送到Edge Network{#configure-custom-personalization-connection}

要实时查找Edge用户档案（包括属性和受众成员资格数据），需要在Edge Network中提供这些数据。 为此，您必须创建与&#x200B;**[!UICONTROL Custom Personalization With Attributes]**&#x200B;目标的连接并激活受众，包括要在边缘配置文件中查找的属性。

+++ 使用属性连接配置自定义Personalization

有关如何创建新目标连接的详细说明，请按照[目标连接创建教程](../ui/connect-destination.md)中的说明进行操作。

配置新目标时，在[字段中选择您在](#create-datastream)步骤1 **[!UICONTROL Datastream ID]**&#x200B;中创建的数据流。 对于&#x200B;**[!UICONTROL Integration alias]**，您可以使用任何有助于将来识别此目标连接的值，如目标名称。

![Experience Platform UI图像显示“具有属性的自定义Personalization”配置屏幕。](../assets/ui/activate-edge-profile-lookup/destination-config.png)

+++

+++将受众激活到具有属性的自定义Personalization连接

创建&#x200B;**[!UICONTROL Custom Personalization With Attributes]**&#x200B;连接后，即可将配置文件数据发送到Edge Network。

>[!IMPORTANT]
> 
> * 要激活数据并启用工作流的[映射步骤](#mapping)，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。
> 
> 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

1. 转到&#x200B;**[!UICONTROL Connections > Destinations]**，然后选择&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡。

   在Experience Platform UI中突出显示![目标目录选项卡。](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. 找到&#x200B;**[!UICONTROL Custom Personalization With Attributes]**&#x200B;目标卡，然后选择&#x200B;**[!UICONTROL Activate audiences]**，如下图所示。

   ![激活目录中目标卡上突出显示的受众控件。](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. 选择您之前配置的目标连接，然后选择&#x200B;**[!UICONTROL Next]**。

   ![在激活工作流中选择目标步骤。](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. 选择您的受众。 使用受众名称左侧的复选框选择要激活到目标的受众，然后选择&#x200B;**[!UICONTROL Next]**。

   您可以从多种类型的受众中进行选择，具体取决于其来源：

   * **[!UICONTROL Segmentation Service]**：分段服务在Experience Platform中生成的受众。 有关详细信息，请参阅[分段文档](../../segmentation/ui/overview.md)。
   * **[!UICONTROL Custom upload]**：受众在Experience Platform之外生成，并以CSV文件形式上传到Experience Platform。 要了解有关外部受众的更多信息，请参阅有关[导入受众](../../segmentation/ui/overview.md#import-audience)的文档。
   * 其他类型的受众，来自其他Adobe解决方案，如[!DNL Audience Manager]。

     ![在激活工作流中选择突出显示多个受众的受众步骤。](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

1. 选择要使其可用于边缘轮廓的轮廓属性。

   * **选择源属性**。 要添加源属性，请选择&#x200B;**[!UICONTROL Add new field]**&#x200B;列上的&#x200B;**[!UICONTROL Source field]**&#x200B;控件，然后搜索或导航到所需的XDM属性字段，如下所示。

     ![显示如何在映射步骤中选择目标属性的屏幕录制。](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

   * **选择目标属性**。 要添加目标属性，请选择&#x200B;**[!UICONTROL Add new field]**&#x200B;列上的&#x200B;**[!UICONTROL Target field]**&#x200B;控件，并键入要将源属性映射到其中的自定义属性名称。

     ![显示如何在映射步骤](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)中选择XDM属性的屏幕录制



完成配置文件属性的映射后，选择&#x200B;**[!UICONTROL Next]**。

在&#x200B;**[!UICONTROL Review]**&#x200B;页面上，您可以看到所选内容的摘要。 选择&#x200B;**[!UICONTROL Cancel]**&#x200B;以中断流，**[!UICONTROL Back]**&#x200B;以修改您的设置，或&#x200B;**[!UICONTROL Finish]**&#x200B;以确认您的选择并开始将配置文件数据发送到Edge Network。

![审核步骤中的选择摘要。](../assets/ui/activate-edge-personalization-destinations/review.png)

+++

+++同意策略评估

如果您的组织购买了&#x200B;**Adobe Healthcare Shield**&#x200B;或&#x200B;**Adobe Privacy &amp; Security Shield**，请选择&#x200B;**[!UICONTROL View applicable consent policies]**&#x200B;以查看应用的同意政策以及激活中因此包含的用户档案数。 有关详细信息，请阅读[同意策略评估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)。

**数据使用策略检查**

在&#x200B;**[!UICONTROL Review]**&#x200B;步骤中，Experience Platform还会检查是否存在任何数据使用策略违规。 下面显示了一个违反策略的示例。 在解决该违规之前，您无法完成受众激活工作流。 有关如何解决策略违规的信息，请参阅数据治理文档部分中的[数据使用策略违规](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation)。

![数据策略违规示例。](../assets/common/data-policy-violation.png)

+++

+++筛选受众

在&#x200B;**[!UICONTROL Review]**&#x200B;步骤中，您可以使用页面上的可用过滤器只显示其计划或映射已作为此工作流的一部分更新的受众。 您还可以切换要查看的表列。

![显示审核步骤中可用的受众过滤器的屏幕录制。](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)


如果您对您的选择感到满意，并且未检测到任何违反策略的情况，请选择&#x200B;**[!UICONTROL Finish]**&#x200B;以确认您的选择。

+++

## 步骤4：查找边缘上的配置文件属性 {#configure-edge-profile-lookup}

到现在您应该已经完成了[数据流的配置](#create-datastream)，您已经[创建了新的具有属性的自定义Personalization目标连接](#configure-destination)，并且您已使用此连接将[发送配置文件属性](#activate-audiences)，您将能够查找到Edge Network。

下一步是配置您的个性化解决方案，以从边缘配置文件中检索配置文件属性。

>[!IMPORTANT]
>
>配置文件属性可能包含敏感数据。 要保护此数据，必须通过[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/getting-started/)检索配置文件属性。 此外，您必须通过Edge Network API [交互式数据收集终结点](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)检索配置文件属性，才能对API调用进行身份验证。
>&#x200B;><br>如果您不遵循上述要求，则将仅基于受众成员资格进行个性化，并且用户档案属性将不可使用。

您在[步骤1](#create-datastream)中配置的数据流现在已准备好接受传入事件数据并使用边缘配置文件信息进行响应。

配置集成以检索边缘配置文件信息，如下面的示例所示。

### 请求 {#request}

要检索边缘配置文件数据，请向`POST`端点发送空`/interact`调用，该端点具有要查找包含在事件中的配置文件属性的主标识，如下所示。

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
    "event":
    {
        "xdm": {
            "identityMap": {
                "Email": [
                    {  
                        "id":"test123@adobetest.com",
                        "primary":true
                    }
                ]
            }
        }
    }
    
}'
```

| 参数 | 类型 | 必需 | 描述 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 可以。 | 您在[步骤1](#create-datastream)中创建的数据流的数据流ID。 |

### 响应 {#response}

成功的响应返回HTTP状态`200 OK`，其中的`Handle`对象包含与以下选项卡中的示例类似的信息，具体取决于是否在边缘上找到配置文件。

>[!NOTE]
>
>API响应是模块化的，`handle`对象可以包含多个不同类型的`payload`对象。 与边缘配置文件查找相关的信息被分组到具有`payload`的`"type": "activation:pull"`对象下，

>[!BEGINTABS]

>[!TAB 配置文件存在于边缘]

如果配置文件存在于边缘，则根据激活到边缘的配置文件属性和受众，您可以期待一个包含属性和受众成员资格的响应，如下所示。

```json
{
  "requestId": "3c600138-d785-42ca-a025-bb725f4b5da9",
  "handle": [
    {
      "payload": [
        {
          "type": "profileLookup",
          "destinationId": "9218b727-ec59-4a46-b8b9-05503f138c5d",
          "alias": "rk-demo-custom-personalization-XXXX",
          "attributes": {
            "zip": {
              "value": "19000"
            },
            "firstName": {
              "value": "Test"
            },
            "lastName": {
              "value": "User123"
            },
            "gender": {
              "value": "male"
            },
            "city": {
              "value": "Philadelphia"
            },
            "state": {
              "value": "PA"
            },
            "email": {
              "value": "test123@adobetest.com"
            }
          },
          "segments": [
            {
              "id": "85018bd8-7ad1-4e17-ae30-8389c04bd3c0",
              "namespace": "ups"
            },
            {
              "id": "d09a8159-8b30-4178-b2f2-7a8c5e3168d9",
              "namespace": "ups"
            }
          ]
        }
      ],
      "type": "activation:pull",
      "eventIndex": 0
    }
  ]
}
```

`handle`对象提供了下表描述的信息。

| 参数 | 描述 |
|---------|----------|
| `payload` | 包含边缘查找信息的`payload`对象。 响应可能包含多个其他`payload`对象，这些对象与边缘查找无关。 |
| `type` | 在响应中，负载按其类型分组。 边缘配置文件查找的有效负载类型始终设置为`profileLookup`。 |
| `destinationId` | 您在&#x200B;**[!UICONTROL Custom Personalization]**&#x200B;步骤3[中创建的](#configure-custom-personalization-connection)连接实例的ID。 |
| `alias` | 目标连接的别名，由用户在创建[自定义Personalization](../catalog/personalization/custom-personalization.md)目标连接时配置。 |
| `attributes` | 此数组包含您在[步骤3](#configure-custom-personalization-connection)中激活的受众的边缘配置文件属性。 |
| `segments` | 此数组包括您在[步骤3](#configure-custom-personalization-connection)中激活的受众。 |
| `type` | `handle`对象按类型分组。 对于边缘配置文件查找用例，`handle`对象的类型始终为`activation:pull`。 |
| `eventIndex` | Edge Network以数组的形式从客户端接收事件。 数组中的事件顺序在处理期间保持不变，并反映在此索引中。 事件索引从`0`开始。 |

>[!TAB 边缘上不存在配置文件]

如果配置文件在边缘上不存在，您可以看到与以下类似的响应。

```json
{
  "requestId": "531b541a-4541-419e-ac99-fd7e452f0c0f",
  "handle": [
    {
      "payload": [],
      "type": "activation:pull",
      "eventIndex": 0
    }
  ]
}
```

`handle`对象提供了下表描述的信息。

| 参数 | 描述 |
|---------|----------|
| `payload` | 当边缘上不存在该配置文件时，`payload`对象为空。 |
| `type` | `payload`对象按类型分组。 对于边缘配置文件查找用例，`payload`对象的类型始终为`activation:pull`。 |
| `eventIndex` | Edge Network以数组的形式接收来自客户端的事件。 数组中的事件顺序在处理期间保持不变，并反映在此索引中。 事件索引从`0`开始。 |

>[!ENDTABS]

>[!SUCCESS]
>
>如果您已正确配置集成，则现在可以访问Edge配置文件数据，并且可以使用Edge配置文件的属性和受众成员资格在下游个性化引擎中触发实时个性化。

## 结论 {#conclusion}

通过执行上述步骤，您可以高效地实时查找边缘配置文件属性，从而通过下游应用程序实现个性化体验和明智决策。
