---
title: Demandbase人员连接
description: 使用此目标可激活您的受众，并使用Demandbase第三方数据扩充这些受众，以用于营销和销售中的其他下游用例。
exl-id: 748f5518-7cc1-4d65-ab70-4a129d9e2066
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 4%

---

# Demandbase人员连接 {#demandbase-people}

激活Demandbase营销活动的配置文件，以实现受众定位、个性化和抑制。

>[!IMPORTANT]
>
>对于需要[激活帐户受众](../../ui/activate-account-audiences.md)的B2B用例，请改用[Demandbase](demandbase.md)目标连接器。

## 用例 {#use-case}

营销人员可以使用Adobe Real-Time CDP创建第一方联系人的“人员列表”，并在Demandbase中激活该列表，以在其需求方平台(DSP)和其他渠道（如LinkedIn）中优化和协调参与。

此方法允许营销人员优先考虑将营销活动支出用于源自其自身CRM或营销自动化系统的已知个人，确保营销工作专注于高价值潜在客户。

激活后，Demandbase会优化广告投放，优化定位策略以最大限度地提高参与度、访问范围和转化率，最终提高营销活动效率。

## 支持的身份 {#supported-identities}

[!DNL Demandbase People]连接支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 纯文本电子邮件地址 | [!DNL Demandbase People]连接仅支持纯文本电子邮件地址。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | X | 受众[已从CSV文件将](../../../segmentation/ui/overview.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-and-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|--------------|-----------|---------------------------|
| 导出类型 | 受众导出 | 您正在导出具有&#x200B;*Demandbase*&#x200B;目标中使用的标识符（姓名、电话号码或其他）的受众的所有成员。 |
| 频率 | 流传输 | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

要将受众导出到Demandbase，您需要满足以下条件：

1. Demandbase帐户。
2. Demandbase API令牌。 您可以在Demandbase中使用用户生成API令牌。 要生成令牌，请在登录到Demandbase帐户后导航到[我的个人资料> API令牌](https://web.demandbase.com/o/ad/at)。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要验证目标，请填写必填字段并选择&#x200B;**[!UICONTROL Connect to destination]**。

![添加持有者令牌](../../assets/catalog/advertising/demandbase-people/bearer-token.png)

* **[!UICONTROL Bearer token]**：填写持有者令牌以对目标进行身份验证。 有关如何获取令牌的信息，请查看[先决条件](#prerequisites)。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![添加有关目标连接的信息](../../assets/catalog/advertising/demandbase-people/name-and-description.png)

* **[!UICONTROL Name]**：将来用于识别此目标的名称。
* **[!UICONTROL Description]**：可帮助您将来识别此目标的描述。

现在，您已准备好在Demandbase People中激活受众。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 强制映射 {#mandatory-mappings}

将受众激活到[!DNL Demandbase People]目标时，您必须在映射步骤中配置以下必填字段映射：

| 源字段 | 目标字段 | 描述 |
|--------------|--------------|-------------|
| `xdm: b2b.personKey.sourceKey` | `xdm: externalPersonId` | 人员的唯一标识符 |
| `xdm: person.name.lastName` | `xdm: lastName` | 人员的姓氏 |
| `xdm: person.name.firstName` | `xdm: firstName` | 人员的名字 |
| `xdm: workEmail.address` | `Identity: email` | 人员的工作电子邮件地址 |

![Demandbase人员映射](/help/destinations/assets/catalog/advertising/demandbase-people/demandbase-people-mapping.png)

目标需要这些映射才能正常运行，并且必须先配置这些映射，然后才能继续激活工作流。

## 其他注释和重要标注 {#additional-notes}

* **Demandbase API护栏**：如果您已将受众导出到Demandbase，并且在Experience Platform中成功导出，但并非所有数据都到达Demandbase，则您可能会在Demandbase端遇到API限制。 请联系他们以获取说明。
* **列表删除**：人员列表是唯一的，因此不能使用名称重新创建新列表。 从列表中删除人员后，这些人员将不再可用，但不会被删除。
* **激活时间**：在Demandbase中加载的数据需要过夜处理。
* **受众命名**：如果之前已将具有相同名称的帐户受众激活到Demandbase，则无法通过其他数据流将其再次激活到Demandbase目标。
