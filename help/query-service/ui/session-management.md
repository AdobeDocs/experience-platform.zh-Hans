---
title: 在Adobe Experience Platform中管理查询服务会话
description: 了解管理员如何查看、监控和结束活动的查询服务会话，以释放空闲容量和维护可靠的Data Distiller工作流。
keywords: Experience Platform；查询服务；会话；会话管理；数据Distiller；管理员
solution: Experience Platform
badgeLimitedAvailability: label="限量发布版" type="Informative"
exl-id: f986177a-9a46-4fc6-927e-98b6b7dc8cfe
source-git-commit: 2117b7ad0f507b5a35595d702cb8a70e2e09f39d
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# 管理查询服务会话

>[!AVAILABILITY]
>
>查询服务的会话管理当前处于有限可用性，仅适用于拥有&#x200B;**Data Distiller**&#x200B;权利的组织。 要请求获取访问权限，请联系您的Adobe客户团队。

使用本指南可从Adobe Experience Platform用户界面管理活动的查询服务会话。 会话管理可帮助管理员跨沙盒监视并发查询编辑器会话，并在用户保持会话打开状态时释放容量。

## 会话管理所需的权限 {#permissions}

>[!IMPORTANT]
>
>此功能面向管理员。 运行查询的最终用户无法管理会话。

要查看和结束会话，您必须属于具有数据Distiller访问权限的组织，并且分配了&#x200B;**[!UICONTROL Manage Query Session]**&#x200B;权限。 没有所需权限的用户可以访问查询服务，但无法查看或管理活动会话。

## 查看活动会话 {#view-active-sessions}

管理员可以查看组织中各个沙盒的所有活动查询服务会话。 在Experience Platform中，从左侧导航中选择&#x200B;**[!UICONTROL Queries]**&#x200B;以打开查询服务工作区，然后选择&#x200B;**[!UICONTROL Admin]**&#x200B;选项卡以访问会话管理。

![选择了“管理员”选项卡的查询服务工作区。 此时将显示“会话管理”表，该表列出了组织中多个沙盒中的活动会话和不活动会话。](../images/ui/session-management/session-management-admin-tab.png)

会话管理表会实时自动更新，并列出当前占用分配给贵组织的查询服务并发会话容量的所有会话。 每一行表示在查询编辑器中打开的单个会话。

## 会话状态和空闲时间 {#session-status}

会话表提供了帮助您确定会话是否可以安全结束的信息。

| 列 | 描述 |
| --- | --- |
| 用户 ID | 负责会话的用户的Adobe ID |
| 用户名 | 与Adobe ID关联的名称 |
| 沙盒 | 指示运行会话的沙盒 |
| 会话状态 | 显示会话是&#x200B;**[!UICONTROL Active]**&#x200B;还是&#x200B;**[!UICONTROL Inactive]** |
| 空闲时间 | 显示会话已打开而没有交互的时间 |
| 剩余会话时间 | 指示会话在自动过期之前可以保持打开状态的时间 |

### 会话状态

**[!UICONTROL Inactive]**&#x200B;表示用户未主动运行查询；这些会话可以结束。 **[!UICONTROL Active]**&#x200B;表示查询当前正在运行；**[!UICONTROL End session]**&#x200B;控件在查询执行完成之前不可用。

### 空闲时间和剩余会话时间

“空闲时间”显示会话在未经用户交互的情况下打开的时间。 剩余会话时间表示会话在系统自动关闭之前可以保持打开状态的时间。 会话在允许的最长持续时间（不活动状态两小时）后自动过期。 此持续时间由系统定义，无法配置。

## 结束空闲会话 {#end-idle-sessions}

您可以结束空闲会话以释放其他用户并发会话的容量。 当用户不再主动工作时，请考虑以高空闲时间结束会话。

从会话管理表中，选择&#x200B;**[!UICONTROL End session]**&#x200B;以选择要结束的非活动会话。

![会话管理表显示了一个非活动会话，其中突出显示了结束会话。](../images/ui/session-management/end-session.png)

出现确认对话框，以防止意外终止。 在对话框中选择&#x200B;**[!UICONTROL End session]**&#x200B;以确认操作。

![结束会话确认对话框显示警告消息并突出显示结束会话。](../images/ui/session-management/end-session-confirmation-dialog.png)

会话结束后，会话将从表中删除，容量会立即可用，并记录操作以供审核。

>[!NOTE]
>
>无法结束状态为&#x200B;**[!UICONTROL Active]**&#x200B;的会话。 此保护措施可防止正在执行的工作负载中断。

## 终止后的会话行为 {#session-behavior-after-termination}

当管理员结束会话时，受影响用户的代码将保留在编辑器中且不会丢失工作。 如果用户在终止后尝试运行查询，则系统会检测已结束的会话，自动重新建立连接，并保持“查询编辑器”内容不变。

此行为可确保用户不会丢失在编辑器中编写的工作，并在建立新会话后继续操作。

## 会话管理的审核日志 {#audit-logs}

系统记录会话管理操作，以提供可视性和责任性。 审核日志记录会话ID、会话结束的用户、执行操作的管理员以及操作的时间。

使用审核日志可查看会话终止历史记录和调查意外断开情况。

有关查看审核日志的详细信息，请参阅[查询服务审核日志指南](../data-governance/audit-log-guide.md)。

## 后续步骤 {#next-steps}

请考虑使用以下资源以扩展查询服务和数据Distiller的使用：

* [了解用户如何在查询编辑器用户指南中创建和运行查询](user-guide.md)
* [使用计划查询监控文档监控计划工作负载](monitor-queries.md)
