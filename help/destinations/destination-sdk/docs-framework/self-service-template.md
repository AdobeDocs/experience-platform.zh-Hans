---
title: 文档自助服务模板//将替换为您的目标名称
description: 使用此模板可在Adobe Experience Platform目录中为您的目标创建公共文档。//替换为“概述”部分中的段落
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 396b9a9ec1509abedba96797f68ad3e5aa2e5988
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 1%

---

# 您的目标 {#your-destination}

*在完成此模板时，请替换或删除所有斜体段落（从此模板开始）。*

*首先，更新页面顶部的元数据（标题和描述）。请忽略此页面上的所有UICONTROL实例。 这是一个标记，可帮助我们的机器翻译流程将页面正确翻译为我们支持的多种语言。 在您提交文档后，我们会在文档中添加标记。*

## 概述 {#overview}

*为您的公司提供简短的概述，包括它为客户提供的价值。包含指向您的产品文档主页的链接，以供进一步阅读。*

>[!IMPORTANT]
>
>本文档页面由&#x200B;*YOURDESTINATION*&#x200B;团队创建。 如有任何查询或更新请求，请直接通过&#x200B;*插入链接或电子邮件地址与他们联系，您可以在此处获取更新*

## 先决条件 {#prerequisites}

*在此部分中添加有关客户在开始在Adobe Experience Platform用户界面中设置目标之前需要了解的任何内容的信息。这可以是关于：*

* *需要添加到允许列表*
* *电子邮件哈希处理要求*
* *您方面的任何帐户详情*
* *如何获取连接到您平台的API密钥*

*如果相关文档对客户有用，您可以将其链接到相关文档。*

## 支持的身份 {#supported-identities}

*在此部分中添加有关目标支持的身份的信息。我们已预填表中一些标准值。 删除未应用于您的目标的值以及任何未预填充的值。*

** YOURDESTINATION支持激活下表中所述的身份。了解有关[identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)的更多信息。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google广告ID | 如果源标识是GAID命名空间，请选择GAID目标标识。 |
| IDFA | 适用于广告商的Apple ID | 如果源标识是IDFA命名空间，请选择IDFA目标标识。 |
| ECID | Experience Cloud ID | 表示ECID的命名空间。 此命名空间也可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 有关更多信息，请参阅以下关于[ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html)的文档。 |
| phone_sha256 | 使用SHA256算法进行哈希处理的电话号码 | Adobe Experience Platform支持纯文本和SHA256哈希电话号码。 当源字段包含未哈希属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]在激活时自动对数据进行哈希处理。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 当源字段包含未哈希属性时，请选中&#x200B;**[!UICONTROL Apply transformation]**&#x200B;选项，以使[!DNL Platform]在激活时自动对数据进行哈希处理。 |
| extern_id | 自定义用户ID | 如果源标识是自定义命名空间，请选择此目标标识。 |

{style=&quot;table-layout:auto&quot;}

## 导出类型 {#export-type}

**区段导出**  — 您要导出区段（受众）的所有成员，以及YOURDESTINATIONdestination中使用的标识符（名称、电话号码或其他） ** 。

## 用例

为了帮助您更好地了解您应如何以及何时使用&#x200B;*YOURDESTINATION*&#x200B;目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1

*对于移动消息平台：*

*一个家庭租赁和销售平台希望向客户的Android和iOS设备推送移动通知，以告知他们以前搜索的租赁区域有100个更新列表。*

### 用例#2

*对于社交网络平台：*

*一家运动服装品牌希望通过其社交媒体帐户联系现有客户。服装品牌可以将电子邮件地址从自己的CRM摄取到Adobe Experience Platform，从自己的离线数据构建区段，并将这些区段发送到您的目标，以在其客户的社交媒体信息源中显示广告。*

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html)此目标时，必须提供以下信息：

*添加客户在配置新目标时必须填写的字段。这些字段特定于目标，取决于您在目标SDK中的配置。 目标的字段可能与下面列出的字段不同。*

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 帐户ID]**:您 ** 的DESTINATION帐户ID。


<!--

*Replace YOURDESTINATION with your destination name and TOBEFILLEDIN with the category that your destination belongs to.*

1. In **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, scroll to the ***TOBEFILLEDIN*** category. Select ***YOURDESTINATION***, then select **[!UICONTROL Configure]**.


    >[!NOTE]
    >
    >If a connection with this destination already exists, you can see an **[!UICONTROL Activate]** button on the destination card. For more information about the difference between **[!UICONTROL Activate]** and **[!UICONTROL Configure]**, refer to the [Catalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destinations-workspace.html#catalog) section of the destination workspace documentation.  

    ![Connect to YOURDESTINATION](./assets/yourdestination1.png)

2. In the **Account** step, if you had previously set up a connection to your *YOURDESTINATION* destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to *YOURDESTINATION*. Select **[!UICONTROL Connect to destination]** to log in and connect Adobe Experience Cloud to your *YOURDESTINATION* account.

    >[!NOTE]
    >
    >Adobe Experience Platform supports credentials validation in the authentication process and displays an error message if you input incorrect credentials to your ***YOURDESTINATION*** account. This ensures that you don't complete the workflow with incorrect credentials.

3. Once your credentials are confirmed and Adobe Experience Cloud is connected to your ***YOURDESTINATION*** account, you can select **[!UICONTROL Next]** to proceed to the **[!UICONTROL Setup]** step.

4. In the **[!UICONTROL Authentication]** step, enter a **[!UICONTROL Name]** and a **[!UICONTROL Description]** for your activation flow and fill your account ID. <br> Also in this step, you can select any marketing action that should apply to this destination. Marketing actions indicate the intent for which data will be exported to the destination. You can select from Adobe-defined marketing actions or you can create your own marketing action. For more information about marketing actions, see the [Data usage policies overview](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html).

    ![Connect to YOURDESTINATION](./assets/yourdestination2.png)

5. Your destination is now created. You can select **[!UICONTROL Save & Exit]** if you want to activate segments later on or you can select **[!UICONTROL Next]** to continue the workflow and select segments to activate. In either case, see the next section, [Activate segments](#activate-segments), for the rest of the workflow.

-->

## 将区段激活到此目标 {#activate}

有关将受众区段激活到此目标的说明，请阅读[将配置文件和区段激活到流区段导出目标](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en)。

<!--

To activate segments to *YOURDESTINATION*, follow the steps below: 

1. In **[!UICONTROL Destinations > Browse]**, select the *YOURDESTINATION* destination where you want to activate your segments.

2. Click the name of the destination. This takes you to the Activate flow.
    ![activate-flow](./assets/yourdestination3.png)
    Note that if an activation flow already exists for a destination, you can see the segments that are currently being sent to the destination. Select **[!UICONTROL Edit activation]** in the right rail and follow the steps below to modify the activation details.
3. Select **[!UICONTROL Activate]**;
4. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to *YOURDESTINATION*.
    ![segments-to-destination](./assets/activate-segments-google-customer-match.png)
5.  In the **[!UICONTROL Mapping]** step, select which attributes and identities from the source XDM schema to map to the target schema. Select **[!UICONTROL Add new mapping]** and browse your schema, select identity namespaces and map them to the corresponding target identity.  
![identity mapping initial screen](./assets/gcm-identity-mapping.png) <br>&nbsp;
   *Plain text email address as primary identity*: If you have plain text (unhashed) email addresses as primary identity in your schema, select the email field in your **[!UICONTROL Source Attributes]** and map to the Email field in the right column under **[!UICONTROL Target Identities]**, as shown below. Set up a mapping between any other attributes you plan to use.
   ![identity mapping step](./assets/ssd-template-identity.png) <br>&nbsp;
6. On the **[!UICONTROL Segment schedule]** page, you can set the start date for sending data to the destination.
7. On the **[!UICONTROL Review]** page, you can see a summary of your selection. Select **[!UICONTROL Cancel]** to break up the flow, **[!UICONTROL Back]** to modify your settings, or **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

>[!IMPORTANT]
>
>In this step, Adobe Experience Platform checks for data usage policy violations. Shown below is an example where a policy is violated. You cannot complete the segment activation workflow until you have resolved the violation. For information on how to resolve policy violations, see [Policy enforcement](https://experienceleague.adobe.com/docs/experience-platform/data-governance/enforcement/auto-enforcement.html#enforcement) in the data governance documentation section.
 
![confirm-selection](./assets/data-policy-violation.png)

If no policy violations have been detected, select **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

![confirm-selection](./assets/gcm-review.png)

-->

## 导出的数据 {#exported-data}

*添加有关如何将数据导出到目标的注释。这将有助于客户确保他们已正确与您的目标集成。 例如，您可以提供类似于下面的示例JSON。*

```
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

## 数据使用和管理 {#data-usage-governance}

处理数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据管理的详细信息，请阅读[数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)。

## 其他资源 {#additional-resources}

*您可以提供产品文档的进一步链接，或您认为对客户成功非常重要的任何其他资源。*
