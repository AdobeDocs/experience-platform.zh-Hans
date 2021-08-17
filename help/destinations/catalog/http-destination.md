---
keywords: 流；
title: HTTP连接
description: 利用Adobe Experience Platform中的HTTP目标，可将配置文件数据发送到第三方HTTP端点。
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 3%

---

# (Alpha)[!DNL HTTP]连接

>[!IMPORTANT]
>
>平台中的[!DNL HTTP]目标当前位于alpha中。 文档和功能可能会发生变化。

## 概述 {#overview}

[!DNL HTTP]目标是一个[!DNL Adobe Experience Platform]流目标，可帮助您将用户档案数据发送到第三方[!DNL HTTP]端点。

要向[!DNL HTTP]端点发送用户档案数据，您必须先连接到[[!DNL Adobe Experience Platform]](#connect-destination)中的目标。

## 用例 {#use-cases}

[!DNL HTTP]目标面向需要将XDM配置文件数据和受众区段导出到通用[!DNL HTTP]端点的客户。

[!DNL HTTP] 端点可以是客户自己的系统或第三方解决方案。

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL httpEndpoint]**:要 [!DNL URL] 将用户档案数据发送到的HTTP端点的。
   * 或者，您也可以将查询参数添加到[!UICONTROL httpEndpoint] [!DNL URL]。
* **[!UICONTROL authEndpoint]**:用于 [!DNL URL] 身份验证的HTTP端点的 [!DNL OAuth2] 。
* **[!UICONTROL 客户端ID]**:客户 [!DNL clientID] 端凭据中使 [!DNL OAuth2] 用的参数。
* **[!UICONTROL 客户端密钥]**:客户 [!DNL clientSecret] 端凭据中使 [!DNL OAuth2] 用的参数。

   >[!NOTE]
   >
   >当前仅支持[!DNL OAuth2]客户端凭据。

* **[!UICONTROL 名称]**:输入一个名称，在将来，您将通过该名称来识别此目标。
* **[!UICONTROL 描述]**:输入描述，以帮助您在将来标识此目标。
* **[!UICONTROL 自定义标题]**:按照以下格式，输入要包含在目标调用中的任何自定义标头： `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >当前实施至少需要一个自定义标头。 此限制将在将来的更新中解决。

## 将区段激活到此目标 {#activate}

有关将受众区段激活到目标的说明，请参阅[将配置文件和区段激活到目标](../ui/activate-destinations.md#select-attributes)。

## 目标属性 {#attributes}

在[[!UICONTROL 选择属性]](../ui/activate-destinations.md#select-attributes)步骤中，当[将区段](../ui/activate-destinations.md)激活到[!DNL HTTP]目标时，Adobe建议您从[并集架构](../../profile/home.md#profile-fragments-and-union-schemas)中选择唯一标识符。 选择唯一标识符以及要导出到目标的任何其他XDM字段。

## 导出的数据 {#exported-data}

导出的[!DNL Experience Platform]数据以JSON格式登陆到[!DNL HTTP]目标中。 例如，以下事件包含符合特定区段资格并退出另一个区段的受众的电子邮件地址配置文件属性。 此潜在客户的标识为[!DNL ECID]和电子邮件。

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
