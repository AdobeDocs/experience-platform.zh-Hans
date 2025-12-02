---
title: 应用响应
description: 根据Edge Network的响应执行操作。
source-git-commit: f87e6a0e969aa0924656cdb2ea56aa79d2d7c841
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# 应用响应

**[!UICONTROL Apply response]**&#x200B;操作类型允许您根据Edge Network的响应执行各种操作。 此操作类型通常用于混合部署，其中服务器对Edge Network进行初始调用，然后此操作类型从该调用中获取响应并在浏览器中初始化Web SDK。 使用此操作类型可减少混合个性化用例的客户端加载时间。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Rules]**，然后选择所需的规则。
1. 在[!UICONTROL Actions]下，选择现有操作或创建操作。
1. 将[!UICONTROL Extension]下拉字段设置为&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，然后将[!UICONTROL Action type]设置为&#x200B;**[!UICONTROL Apply response]**。

![显示“应用响应”操作类型的Experience Platform用户界面的图像。](../assets/apply-response.png)

## 用例

* **数据收集和个性化之间的手动拆分**：您可以在渲染决策设置为[时触发](send-event.md)发送事件`false`操作，然后使用“发送事件完成”规则捕获promise。 此规则中的第一个操作可以是“应用响应”。 利用此工作流，可将DOM操作延迟到组织自己的代码完成其他工作之后。
* **从Web SDK外部收到的Edge响应**：如果您使用其他库与Edge Network通信，则可以允许Web SDK仍然使用此操作处理来自Edge Network的响应。

## 可用字段

此操作类型支持以下配置选项：

* **[!UICONTROL Instance]**：操作适用的SDK实例。 如果您的实施使用单个SDK实例，则会禁用此下拉菜单。
* **[!UICONTROL Response headers]**：选择数据元素，该数据元素将返回一个对象，其中包含从Edge Network服务器调用返回的标头键和值。
* **[!UICONTROL Response body]**：选择数据元素，该数据元素将返回包含Edge Network响应提供的JSON有效负载的对象。
* **[!UICONTROL Render visual personalization decisions]**：启用此选项以自动呈现Edge Network提供的个性化内容并预隐藏内容以防止闪烁。
