---
title: 身份设置UI
description: 了解如何使用身份设置用户界面。
badge: Beta 版
source-git-commit: 72773f9ba5de4387c631bd1aa0c4e76b74e5f1dc
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# 身份设置UI

>[!AVAILABILITY]
>
>此功能尚不可用；标识图链接规则的测试版计划预计于7月在开发沙盒上开始。 有关参与标准的信息，请与您的Adobe客户团队联系。

身份设置是Adobe Experience Platform Identity Service UI中的一项功能，可用于指定唯一的命名空间并配置命名空间优先级。

阅读本指南，了解如何在UI中配置身份设置。

## 先决条件

在开始使用标识设置之前，请阅读以下文档：

* [身份图链接规则配置指南](./configuration.md)
* [身份优化算法](./identity-optimization-algorithm.md)
* [命名空间优先级](./namespace-priority.md)
* [图形模拟](./graph-simulation.md)

## 配置您的身份设置

要访问身份设置，请在Adobe Experience Platform UI中导航到Identity Service工作区，然后选择&#x200B;**[!UICONTROL 设置]**。

![已选择身份设置按钮。](../images/rules/identities-ui.png)

身份设置页面分为两个部分：[!UICONTROL 人员命名空间]和[!UICONTROL 设备或Cookie命名空间]。 人员命名空间是单个个人的标识符。 它们可以是跨设备ID、电子邮件地址和电话号码。 设备或Cookie命名空间是设备和Web浏览器的标识符，不能赋予它们比人员命名空间更高的优先级。 您也不能将设备或Cookie命名空间指定为唯一的命名空间。

### 配置命名空间优先级

要配置命名空间优先级，请在身份设置菜单中选择命名空间，然后将该命名空间拖放到您喜欢的顺序中。 将命名空间放在列表上较高可为其提供较高的优先级，相反，将命名空间放在列表上较低可为其提供较低的优先级。 具有最高优先级的命名空间也应指定为唯一的命名空间。

![身份设置工作区中突出显示了人员命名空间。](../images/rules/namespace-priority.png)

### 指定您的唯一命名空间

要指定唯一的命名空间，请选中与该命名空间对应的[!UICONTROL 每个图形唯一]复选框。 可以为身份设置配置选择多个唯一的命名空间。

![选定两个命名空间并将其定义为唯一。](../images/rules/unique-namespace.png)

建立唯一的命名空间后，图形将不再能够拥有包含唯一命名空间的多个身份。 例如，如果您指定CRM ID作为唯一的命名空间，则图表只能有一个具有CRM ID命名空间的身份。 有关详细信息，请阅读[标识优化算法概述](./identity-optimization-algorithm.md#unique-namespace)。

完成配置后，选择&#x200B;**[!UICONTROL 下一步]**。 出现确认消息，请使用此机会验证您的配置是否正确，然后选择&#x200B;**[!UICONTROL 完成]**。

![已突出显示Finish的验证页面。](../images/rules/finish.png)

出现警告，指示您的新设置不会对身份图中的现有链接和已摄取的体验事件配置文件片段产生任何影响。 此外，您会收到通知，新设置最多需要6小时才能反映在系统中。 要确认输入您的沙盒名称，然后选择&#x200B;**[!UICONTROL 确认]**。

![确认窗口，显示有关在处理配置之前延迟6小时的警告。](../images/rules/confirm-settings.png)

## 后续步骤

现在，您已配置命名空间优先级，并使用身份设置UI页面指定了唯一的命名空间。 有关详细信息，请阅读[标识图链接规则概述](./overview.md)。