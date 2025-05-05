---
title: （公司） LinkedIn连接
description: 使用此目标来激活 Account-Based Marketing (ABM) 用例的帐户受众。根据散列电子邮件，激活LinkedIn营销活动的用户档案，以实现受众定位、个性化和抑制。
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=zh-Hans#rtcdp-editions newtab=true"
badgeB2P: label="B2P版本" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=zh-Hans#rtcdp-editions newtab=true"
exl-id: 68d2cca3-952b-49d0-8ea2-e776a233b752
source-git-commit: e7c0551276d31d6809ace096c00e0dc2665090e6
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 5%

---

# （公司） LinkedIn匹配受众连接 {#companies-linkedin}

>[!AVAILABILITY]
>
>向（公司） LinkedIn目标激活帐户受众的功能适用于购买[企业对企业](/help/rtcdp/overview.md#rtcdp-b2b)和[企业对个人](/help/rtcdp/overview.md#rtcdp-b2p)版本的Real-Time Customer Data Platform的公司。

使用此目标为Account-Based Marketing (ABM)用例激活您的[帐户受众](/help/segmentation/types/account-audiences.md)。 通过&#x200B;**[!UICONTROL （公司） LinkedIn]**&#x200B;企业到企业目标向目标帐户中的相关角色和角色播发。 访问LinkedIn文档，以在LinkedIn平台上[了解有关帐户定位](https://business.linkedin.com/marketing-solutions/cx/21/10/ad-targeting/account-targeting)的更多信息。

>[!TIP]
>
>对于个人级别（或企业对消费者）用例，Adobe建议您使用[LinkedIn匹配的受众](/help/destinations/catalog/social/linkedin.md)目标。

在Experience Platform UI中显示![LinkedIn帐户目标。](/help/destinations/assets/catalog/social/linkedin-b2b/linkedin-b2b-destination.png)

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 支持 | 描述 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | X | 受众[已从CSV文件将](../../../segmentation/ui/overview.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-and-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|--------------|-----------|---------------------------|
| 导出类型 | 受众导出 | 将使用关键标识符（如姓名、电话号码等）导出所有受众成员。 |
| 频度 | 流式处理 | 基于“始终运行”API的连接。 配置文件更改后，更新会立即发送到下游。 |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

确保您满足以下先决条件，以将帐户受众导出到LinkedIn：

### LinkedIn帐户先决条件 {#LinkedIn-account-prerequisites}

在使用[!UICONTROL （公司） LinkedIn匹配的受众]目标之前，请确保您的[!DNL LinkedIn Campaign Manager]帐户具有[!DNL Creative Manager]权限级别或更高。

要了解如何编辑您的[!DNL LinkedIn Campaign Manager]用户权限，请参阅LinkedIn文档中的[添加、编辑和删除Advertising帐户的用户权限](https://www.linkedin.com/help/lms/answer/5753)。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

1. 在目标目录中找到[!DNL (Companies) LinkedIn Matched Audiences]目标并选择&#x200B;**[!UICONTROL 设置]**。
2. 选择&#x200B;**[!UICONTROL 连接到目标]**。
   ![对LinkedIn进行身份验证](/help/destinations/assets/catalog/social/linkedin-b2b/authenticate-linkedin-destination.png)
3. 输入您的LinkedIn凭据并选择&#x200B;**登录**。

使用LinkedIn完成登录过程后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 帐户ID]**：您的[!DNL LinkedIn Campaign Manager Account ID]。 您可以在您的[!DNL LinkedIn Campaign Manager]帐户中找到此ID。

现在，您可以向LinkedIn激活帐户受众。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将帐户受众激活到目标。](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "选择工作流中突出显示的身份命名空间以将帐户受众激活到目标。"){width="100" zoomable="yes"}

有关将帐户受众激活到此目标的说明，请阅读[激活帐户受众](/help/destinations/ui/activate-account-audiences.md)。

## 将帐户受众激活到&#x200B;**[!UICONTROL （公司） LinkedIn匹配的受众]**&#x200B;目标时，映射步骤中需要映射对 {#required-mappings}

将帐户受众激活到&#x200B;**[!UICONTROL （公司） LinkedIn匹配的受众]**&#x200B;目标时，请注意，以下两个映射对是成功导出数据的必备项：

![LinkedIn映射必填字段。](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| 源字段 | 目标字段 |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` （在选择&#x200B;**[!UICONTROL 目标字段]**&#x200B;时，在&#x200B;**[!UICONTROL 选择身份命名空间]**&#x200B;视图中选择此字段）。<br> ![选择工作流中突出显示的身份命名空间以将帐户受众激活到目标。](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "选择工作流中突出显示的身份命名空间以将帐户受众激活到目标。"){width="100" zoomable="yes"} |

{style="table-layout:auto"}

## 导出的数据 {#exported-data}

成功激活意味着[!DNL LinkedIn]自定义受众是在[[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login)中以编程方式创建的。 当用户在激活的受众中符合资格或被取消资格时，会调整受众成员资格。
