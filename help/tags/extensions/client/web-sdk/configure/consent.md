---
title: 同意配置设置
description: 配置标记扩展的默认同意和隐私设置。
exl-id: 93913a8b-0351-409d-b26a-8dc2ac0296c5
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 同意配置设置 {#consent}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_consent"
>title="同意"
>abstract="选择默认同意级别，如果未提供其他明确的同意首选项，则假定使用该级别。"

**[!UICONTROL Consent]**&#x200B;部分允许您选择在没有提供其他明确的同意首选项时假设的默认同意级别。 默认同意级别未保存到用户配置文件。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Extensions]**，然后在&#x200B;**[!UICONTROL Configure]**&#x200B;信息卡上选择[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下滚动到&#x200B;**[!UICONTROL Consent]**&#x200B;部分。

![在标记UI中显示Web SDK标记扩展的隐私设置的图像](../assets/web-sdk-ext-privacy.png)

此部分包含一组单选按钮，用于决定默认同意级别：

* **[!UICONTROL In]**：收集在用户提供同意首选项之前发生的事件。
* **[!UICONTROL Out]**：删除在用户提供同意首选项之前发生的事件。
* **[!UICONTROL Pending]**：在用户提供同意首选项之前发生的队列事件。 获得同意后，已排队的事件将发送到Adobe。 拒绝同意时，将丢弃已排队的事件。
* **[!UICONTROL Provide a data element]**：选择一个可确定上述配置设置之一的数据元素。 有效值包括字符串`"in"`、`"out"`或`"pending"`。

如果您的组织需要明确的用户同意才能收集数据，Adobe建议将默认同意设置为&#x200B;**[!UICONTROL Out]**&#x200B;或&#x200B;**[!UICONTROL Pending]**。
