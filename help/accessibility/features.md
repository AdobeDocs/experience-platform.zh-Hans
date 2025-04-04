---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API；统一配置文件；统一配置文件；配置文件；rtcp；XDM图
title: Experience Platform中的常规辅助功能
type: Documentation
description: 详细了解Adobe Experience Platform支持的常规辅助功能，包括键盘导航、调色板和对比度以及辅助技术支持。
exl-id: 4b7e2f2b-af51-4376-8a63-16c921cc7135
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# Experience Platform中的辅助功能

Adobe Experience Platform致力于为所有用户提供无障碍和具有包容性的功能，包括使用语音识别软件和屏幕阅读器等辅助设备的用户。 本文档概述了Experience Platform支持的一般辅助功能，包括键盘导航、语义结构、前景元素和背景元素之间的充分对比度以及支持辅助技术。

## 辅助技术

残障用户经常依赖硬件和软件（称为辅助技术）来访问数字内容和使用软件产品。 Adobe Experience Platform通过遵循辅助功能最佳实践（如使用语义代码、等效文本、标签和在需要时使用ARIA），支持多种类型的辅助技术(AT)，如屏幕阅读器、缩放和语音识别软件。 Experience Platform用户界面(UI)中的交互式元素使用相应的标签、可访问名称和角色，来标识其用途及其当前状态。 这可确保辅助技术（如屏幕阅读器）可以向用户朗读标签和其他信息，以便他们能够轻松地与应用程序控件交互。

## 键盘辅助功能

Experience Platform致力于支持完整的键盘辅助功能。

以下导航元素有助于促进无障碍功能：
* Tab键可在UI元素、部分和菜单组之间移动。
* 箭头键在菜单组中移动，以将焦点设置为单个活动元素。
* Shift + Tab键向后移动Tab键顺序。
* Return (Enter)和空格键可激活选定项。
* Esc键(ESC)充当取消按钮，可在出现时关闭对话框。
* Experience Platform在选定元素周围显示蓝色边框，以清楚地指示当前具有焦点的UI元素。

![选定元素周围出现蓝色边框，指示已应用焦点。](images/profile-overview-tab.png)

## 调色板和对比度

Experience Platform致力于符合[WCAG 2.1 AA](https://www.w3.org/TR/WCAG/)，包括对颜色对比度的要求。 Experience Platform UI在应用程序中提供了足够的对比度，可确保视力低下或色觉缺失的用户获得可访问的查看体验。

![Experience Platform UI的主页上显示的调色板和对比度。](images/homepage.png)

## 必填字段验证

在添加数据、创建模式或定义区段时，必填字段以可视方式（在字段的文本标签旁使用星号）和编程方式显示。 当您在字段中输入无效数据并保存时，这些字段会触发验证。 如果必填字段未通过验证，则会以红色列出，并带有错误图标，同时还会显示需要修复的问题的书面说明。

![未通过验证的必填字段的特写。 该字段显示为红色，并出现错误图标。](images/field-validation.png)
