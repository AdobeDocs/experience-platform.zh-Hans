---
keywords: 流；
title: HTTP连接
description: Adobe Experience Platform中的HTTP目标允许您将用户档案数据发送到第三方HTTP端点。
translation-type: tm+mt
source-git-commit: 5435661d750c4138ea6a2d40619a48236b7b1e4f
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 2%

---


# (Alpha)[!DNL HTTP]连接

>[!IMPORTANT]
>
>平台中的[!DNL HTTP]目标当前位于alpha中。 文档和功能可能会发生变化。

[!DNL HTTP]目标是[!DNL Adobe Experience Platform]流目标，可帮助您将用户档案数据发送到第三方[!DNL HTTP]端点。

要将用户档案数据发送到[!DNL HTTP]终结点，必须首先连接到[[!DNL Adobe Experience Platform]](#connect-destination)中的目标。

## 用例 {#use-cases}

[!DNL HTTP]目标针对需要将XDM用户档案数据和受众段导出到通用[!DNL HTTP]端点的客户。

[!DNL HTTP] 端点可以是客户自己的系统或第三方解决方案。

## 连接到目标{#connect-destination}

在&#x200B;**[!UICONTROL 连接]** > **[!UICONTROL 目标]**&#x200B;中，选择[!DNL HTTP API]，然后选择&#x200B;**[!UICONTROL 配置]**。

![激活HTTP目标](../assets/catalog/http/activate.png)

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按钮。 有关&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之间差异的详细信息，请参阅目标工作区文档的[Catalog](../ui/destinations-workspace.md#catalog)部分。
>
>![激活HTTP目标](../assets/catalog/http/connect.png)

在[!UICONTROL 帐户]步骤中，需要定义HTTP端点连接详细信息。 选择&#x200B;**[!UICONTROL 新建帐户]**&#x200B;并输入要连接到的HTTP端点的连接详细信息。
- **[!UICONTROL httpEndpoint]**:要 [!DNL URL] 将用户档案数据发送到的HTTP端点的完整。
   - 或者，您也可以向[!UICONTROL httpEndpoint] [!DNL URL]添加查询参数。
- **[!UICONTROL authEndpoint]**:用于 [!DNL URL] 身份验证的HTTP端点的完 [!DNL OAuth2] 整。
- **[!UICONTROL 客户端ID]**:客户端 [!DNL clientID] 凭据中使用 [!DNL OAuth2] 的参数。
- **[!UICONTROL 客户机密]**:客户端 [!DNL clientSecret] 凭据中使用 [!DNL OAuth2] 的参数。

>[!NOTE]
>
>当前仅支持[!DNL OAuth2]客户端凭据。

![HTTP端点连接](../assets/catalog/http/connect.png)

单击&#x200B;**[!UICONTROL 连接到目标]**。 连接成功后，单击&#x200B;**[!UICONTROL 下一步]**。

在[!UICONTROL 身份验证]步骤中，输入帐户身份验证凭据：
- **[!UICONTROL 名称]**:输入一个名称，您将通过该名称在将来识别此目标。
- **[!UICONTROL 描述]**:输入说明，帮助您在将来识别此目标。
- **[!UICONTROL 自定义标题]**:按照以下格式输入要包含在目标调用中的任何自定义标头： `header1:value1,header2:value2,...headerN:valueN`.
- **[!UICONTROL 营销操作]**:营销活动指示要将数据导出到目标的目的。您可以从Adobe定义的营销活动中进行选择，也可以创建自己的营销活动。 有关营销操作的详细信息，请参阅Adobe Experience Platform](/help/data-governance/policies/overview.md)中的[数据治理页面。 有关各个Adobe定义的营销操作的信息，请参阅[数据使用策略概述](/help/data-governance/policies/overview.md)。

>[!IMPORTANT]
>
>当前实现至少需要一个自定义标头。 此限制将在将来的更新中解决。

![HTTP身份验证](../assets/catalog/http/authenticate.png)

**[!UICONTROL 营销活动]**:营销活动指示要将数据导出到目标的目的。您可以从Adobe定义的营销活动中进行选择，也可以创建自己的营销活动。 有关营销操作的详细信息，请参阅[数据使用策略概述](../../data-governance/policies/overview.md)。

单击&#x200B;**[!UICONTROL 创建目标]**。

## 激活区段

有关区段用户档案工作流的信息，请参阅[将激活和区段激活到目标](../ui/activate-destinations.md#select-attributes)。

## 目标属性

在[[!UICONTROL 选择属性]](../ui/activate-destinations.md#select-attributes)步骤中，当[将区段](../ui/activate-destinations.md)激活到[!DNL HTTP]目标时，建议您从[合并模式](../../profile/home.md#profile-fragments-and-union-schemas)中选择唯一标识符。 选择唯一标识符以及要导出到目标的任何其他XDM字段。

## 导出的数据{#exported-data}

导出的[!DNL Experience Platform]数据以JSON格式进入您的[!DNL HTTP]目标。 例如，以下事件包含符合特定区段条件并退出另一区段的受众的电子邮件地址用户档案属性。 此潜在客户的标识为[!DNL ECID]和电子邮件。

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
