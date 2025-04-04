---
keywords: Experience Platform；主页；热门主题；访问控制；基于属性的访问控制；ABAC
title: 基于属性的访问控制管理标签
description: 本文档提供了有关通过Adobe Experience Cloud中的权限界面管理标签的信息
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 24%

---

# 管理标签

>[!NOTE]
>
>要创建或查看字段包含给定标签的计算属性，您必须有权访问该标签。

标签允许您根据应用于该数据的使用情况和访问策略对数据集和字段进行分类。 您可以随时应用标签，灵活地选择管理数据的方式。 最佳实践鼓励在将数据摄取到Experience Platform中后立即为其设置标签，或者当数据在Experience Platform中可用时立即为其设置标签。

## 创建新标签 {#create-new-label}

>[!CONTEXTUALHELP]
>id="platform_abac_labelusage"
>title="标签使用"
>abstract="您可以使用自定义标签将数据治理和访问控制配置应用于您的数据。"

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="创建新标签"
>abstract="可自行创建自定义标签以适合组织需求。自定义标签可用于将数据治理和访问控制配置应用于您的数据。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html#manage-labels" text="管理自定义标签"

>[!NOTE]
>
>整个组织只有一个标签列表。 要创建自定义标签，您需要在生产沙盒上具有&#x200B;**[!UICONTROL 管理使用标签]**&#x200B;权限。 当前不支持删除标签。

要创建新标签，请选择侧边栏中的&#x200B;**[!UICONTROL 标签]**&#x200B;选项卡，然后选择&#x200B;**[!UICONTROL 创建标签]**。

![flac-new-label](../../images/flac-ui/create-label.png)

出现&#x200B;**[!UICONTROL 创建新标签]**&#x200B;对话框，提示您输入名称、可选的友好名称和可选的说明。

![new-label-info](../../images/flac-ui/new-label-info.png)

完成后，选择&#x200B;**[!UICONTROL 确认]**。
