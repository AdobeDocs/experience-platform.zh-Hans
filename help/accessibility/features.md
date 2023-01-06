---
keywords: Experience Platform；配置文件；实时客户配置文件；故障诊断；API；统一配置文件；统一配置文件；统一；配置文件；rtcp;XDM图形
title: 平台中的常规辅助功能
type: Documentation
description: 进一步了解Adobe Experience Platform支持的常规辅助功能，包括键盘导航、调色板和对比度以及辅助技术支持。
exl-id: 4b7e2f2b-af51-4376-8a63-16c921cc7135
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 3%

---

# Experience Platform中的辅助功能

Adobe Experience Platform致力于向所有个人提供无障碍且包含所有内容的功能，包括使用语音识别软件和屏幕阅读器等辅助设备的用户。 本文档概述了平台支持的常规辅助功能，包括键盘导航、语义结构、前景元素和背景元素之间的充分对比度，以及对辅助技术的支持。

## 辅助技术

残障用户经常依赖硬件和软件（称为辅助技术）来访问数字内容和使用软件产品。 Adobe Experience Platform通过遵循辅助功能最佳实践（如在需要时使用语义代码、对等文本、标签和ARIA）来支持多种类型的辅助技术(AT)，例如屏幕阅读器、缩放和语音识别软件。 Experience Platform用户界面(UI)中的交互式元素使用相应的标签、可访问名称和角色来标识其用途和当前状态。 这可确保辅助技术（如屏幕阅读器）能够向用户朗读标签和其他信息，以便他们能够轻松与应用程序控件进行交互。

## 键盘辅助功能

Experience Platform努力支持完整的键盘无障碍功能。

以下导航元素有助于促进无障碍功能：
* 选项卡键在UI元素、部分和菜单组之间移动。
* 箭头键在菜单组内移动，以将焦点设置到单个活动元素。
* Shift + Tab按制表符顺序向后移动。
* 返回键(Enter)和空格键可激活选定项目。
* 转义键(ESC)用作取消按钮，在出现时关闭对话框。
* Experience Platform在选定元素周围显示一个蓝色边框，以明确指示当前具有焦点的UI元素。

![选定元素周围显示蓝色边框，指示已应用焦点。](images/profile-overview-tab.png)

## 调色板和对比度

Experience Platform努力 [WCAG 2.1 AA](https://www.w3.org/TR/WCAG/) 符合性，包括对颜色对比度的要求。 Experience PlatformUI在应用程序中提供了足够的对比度，以确保视力低下或色觉缺失的用户具有无障碍的观看体验。

![Experience PlatformUI的主页上显示的调色板和对比度。](images/homepage.png)

## 必填字段验证

添加数据、创建架构或定义区段时，必填字段以可视方式（在字段的文本标签旁边使用星号）以及以编程方式指示。 当您在字段中输入无效数据并在保存时，这些字段会触发验证。 如果必填字段未通过验证，则会以红色列出，并带有错误图标，同时还会显示需要修复的问题的书面说明。

![未通过验证的必填字段的特写。 该字段以红色显示，并显示错误图标。](images/field-validation.png)
