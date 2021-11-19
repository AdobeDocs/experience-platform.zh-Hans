---
keywords: 流；
title: HTTP连接
description: 利用Adobe Experience Platform中的HTTP API目标，可将配置文件数据发送到第三方HTTP端点。
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 3bec18f1b7209b1f329dc90aadb597edb6143291
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 3%

---

# （测试版） [!DNL HTTP] API连接

>[!IMPORTANT]
>
>的 [!DNL HTTP] 平台中的目标当前为测试版。 文档和功能可能会发生变化。

## 概述 {#overview}

的 [!DNL HTTP] API目标是 [!DNL Adobe Experience Platform] 可帮助您将用户档案数据发送到第三方的流目标 [!DNL HTTP] 端点。

将用户档案数据发送到 [!DNL HTTP] 端点，您必须首先在 [[!DNL Adobe Experience Platform]](#connect-destination).

## 用例 {#use-cases}

的 [!DNL HTTP] 目标针对需要将XDM配置文件数据和受众区段导出到通用 [!DNL HTTP] 端点。

[!DNL HTTP] 端点可以是客户自己的系统或第三方解决方案。

## 连接到目标 {#connect}

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!UICONTROL httpEndpoint]**:the [!DNL URL] 要将用户档案数据发送到的HTTP端点的URL。
   * （可选）您可以将查询参数添加到 [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**:the [!DNL URL] 用于 [!DNL OAuth2] 身份验证。
* **[!UICONTROL 客户端ID]**:the [!DNL clientID] 参数 [!DNL OAuth2] 客户端凭据。
* **[!UICONTROL 客户端密钥]**:the [!DNL clientSecret] 参数 [!DNL OAuth2] 客户端凭据。

   >[!NOTE]
   >
   >仅 [!DNL OAuth2] 当前支持客户端凭据。

* **[!UICONTROL 名称]**:输入一个名称，在将来，您将通过该名称来识别此目标。
* **[!UICONTROL 描述]**:输入描述，以帮助您在将来标识此目标。
* **[!UICONTROL 自定义标题]**:按照以下格式，输入要包含在目标调用中的任何自定义标头： `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >当前实施至少需要一个自定义标头。 此限制将在将来的更新中解决。

## 将区段激活到此目标 {#activate}

请参阅 [将受众数据激活到流配置文件导出目标](../../ui/activate-streaming-profile-destinations.md) 有关将受众区段激活到此目标的说明。

### 目标属性 {#attributes}

在 [[!UICONTROL 选择属性]](../../ui/activate-streaming-profile-destinations.md#select-attributes) 步骤，Adobe建议您从 [合并模式](../../../profile/home.md#profile-fragments-and-union-schemas). 选择唯一标识符以及要导出到目标的任何其他XDM字段。

## 导出的数据 {#exported-data}

导出的 [!DNL Experience Platform] 数据登陆您的 [!DNL HTTP] 目标。 例如，以下事件包含符合特定区段资格并退出另一个区段的受众的电子邮件地址配置文件属性。 此潜在客户的标识为 [!DNL ECID] 和电子邮件。

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
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
