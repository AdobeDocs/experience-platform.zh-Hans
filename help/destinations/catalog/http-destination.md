---
keywords: streaming;
title: HTTP目标是实时客户数据平台目标，可帮助您将用户档案数据发送到第三方HTTP端点。
seo-title: HTTP目标是实时客户数据平台目标，可帮助您将用户档案数据发送到第三方HTTP端点。
description: HTTP目标是实时客户数据平台目标，可帮助您将用户档案数据发送到第三方HTTP端点。
seo-description: HTTP目标是实时客户数据平台目标，可帮助您将用户档案数据发送到第三方HTTP端点。
translation-type: tm+mt
source-git-commit: 85e6a65e1407ca60e7b63681c045fadaaa24aef9
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 2%

---


# (Alpha)目 [!DNL HTTP] 标

>[!IMPORTANT]
>
>实 [!DNL HTTP] 时CDP中的目标当前位于alpha中。 文档和功能可能会发生变化。

## 概述 {#overview}

目 [!DNL HTTP] 标是一个流 [!DNL Real-time Customer Data Platform] 式目标，可帮助您将用户档案数据发送到第三方端 [!DNL HTTP] 点。

要将用户档案数据发 [!DNL HTTP] 送到端点，您必须先连接到中的目标 [[!DNL Real-time Customer Data Platform]](#connect-destination)。

## 用例 {#use-cases}

目 [!DNL HTTP] 标针对需要将XDM用户档案数据和受众段导出到通用端点的 [!DNL HTTP] 客户。

[!DNL HTTP] 端点可以是客户自己的系统或第三方解决方案。

## 连接到目标 {#connect-destination}

在“ **[!UICONTROL 连接]** ”>“ **[!UICONTROL 目标]**”中 [!DNL HTTP API]，选 **[!UICONTROL 择并选择“]**&#x200B;配置”。

![激活HTTP目标](../assets/catalog/http/activate.png)

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡 **[!UICONTROL 上看到]** “激活”按钮。 有关激活和配置之 **[!UICONTROL 间差异]** 的详 **[!UICONTROL 细信]**&#x200B;息，请参 [阅目标工](../ui/destinations-workspace.md#catalog) 作区文档的“目录”部分。
>
>![激活HTTP目标](../assets/catalog/http/connect.png)

在“帐 [!UICONTROL 户] ”步骤中，您需要定义HTTP端点连接详细信息。 选 **[!UICONTROL 择“新]** 建帐户”，然后输入要连接到的HTTP端点的连接详细信息。
- **[!UICONTROL httpEndpoint]**:要发 [!DNL URL] 送用户档案数据的HTTP端点的完整。
   - 或者，您也可以将查询参数添 [!UICONTROL 加到httpEndpoint][!DNL URL]。
- **[!UICONTROL authEndpoint]**:用于身 [!DNL URL] 份验证的HTTP端点的完 [!DNL OAuth2] 整。
- **[!UICONTROL 客户端ID]**:客户端 [!DNL clientID] 凭据中使用 [!DNL OAuth2] 的参数。
- **[!UICONTROL 客户端机密]**:客户端 [!DNL clientSecret] 凭据中使用 [!DNL OAuth2] 的参数。

>[!NOTE]
>
>当前 [!DNL OAuth2] 仅支持客户端凭据。

![HTTP端点连接](../assets/catalog/http/connect.png)

单击 **[!UICONTROL “连接到目标”]**。 连接成功后，单击“下 **[!UICONTROL 一步]**”。

在身份验证 [!UICONTROL 步骤] ，输入帐户身份验证凭据：
- **[!UICONTROL 名称]**:输入一个名称，您将通过该名称在将来识别此目标。
- **[!UICONTROL 描述]**:输入将帮助您在将来识别此目标的描述。
- **[!UICONTROL 自定义标题]**:按照以下格式输入要包含在目标调用中的任何自定义标题： `header1:value1,header2:value2,...headerN:valueN`.

>[!IMPORTANT]
>
>当前实现至少需要一个自定义头。 此限制将在将来的更新中解决。

![HTTP身份验证](../assets/catalog/http/authenticate.png)

**[!UICONTROL 营销用例]**:市场营销用例指明要将数据导出到目标的目的。 您可以从Adobe定义的营销用例中进行选择，也可以创建自己的营销用例。 有关营销使用案例的更多信息， [请参阅实时CDP中的数据管理](../../rtcdp/privacy/data-governance-overview.md#destinations) 。 有关各个Adobe定义的营销用例的信息，请参阅数据 [使用策略概述](../../data-governance/policies/overview.md#core-actions)。

单击“ **[!UICONTROL 创建目标]**”。

## 激活区段

有关 [区段用户档案工作流的信息](../ui/activate-destinations.md#select-attributes) ，请参阅将激活和区段激活到目标。

## 目标属性

在选择 [[!UICONTROL 属性]](../ui/activate-destinations.md#select-attributes) 步骤中， [将区段激活到目标](../ui/activate-destinations.md) 时， [!DNL HTTP] 建议您从合并模式中选择唯一标 [识符](../../profile/home.md#profile-fragments-and-union-schemas)。 选择唯一标识符以及要导出到目标的任何其他XDM字段。

## 导出的数据 {#exported-data}

导出的 [!DNL Experience Platform] 数据以JSON格 [!DNL HTTP] 式进入您的目标。 例如，以下事件包含符合特定区段资格并退出另一区段的受众的电子邮件地址用户档案属性。 此潜在客户的身份为 [!DNL ECID] 电子邮件。

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
