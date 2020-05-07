---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: 实时机器学习概述
topic: Overview
translation-type: tm+mt
source-git-commit: ab8b000bec0ae30c695582f57c40105b7ca1f22f
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 2%

---


# 实时机器学习概述

>[!IMPORTANT]
>尚未向所有用户提供实时机器学习。 此功能在alpha中，仍在测试中。 此文档可能会更改。

Adobe Experience Platform的实时机器学习框架使您能够使用机器学习在适当的时间在适当的渠道通过次秒的时间框架，在适当的时间向适当的最终用户提供适当的体验。

## 优点

实时机器学习可以显着增强您的数字体验内容对最终用户的相关性。 通过在Experience Edge上利用实时参考和持续学习，可以实现这一点。

在集线器和边缘上的无缝计算相结合可显着减少过去在为超级个性化体验提供相关性和响应性方面所涉及的延迟。 因此，实时机器学习为同步决策提供了极低延迟的推理。 示例包括呈现个性化网页内容或呈现优惠或折扣，以减少客户流失并提高网店转化率。

## 实时机器学习架构

下图提供了实时机器学习体系结构的概述。

![简化的概述](../images/rtml/simple-overview.png)

## 实时机器学习工作流程(Alpha)

以下工作流概述了创建和利用实时机器学习模型时涉及的典型步骤和结果。

### 数据获取和准备

借助Adobe Experience Platform上的体验数据模型(XDM)，数据被摄取并转换。 此数据用于模型培训。 要进一步了解XDM，请访 [问XDM概述](../../xdm/home.md)。

### 创作

通过从头开始创作实时机器学习模型，或在Adobe Experience Platform Jupyter笔记本中将其作为经过预先培训的序列化ONNX模型引入，创建实时机器学习模型。

### 部署

将您的模型部署到Experience Edge以使用预测API端点在服务库中创建实时机器学习服务。

### 推理

使用Prediction REST API端点实时生成机器学习洞察。

### 投放

然后，营销人员可以定义将实时机器学习得分与使用Adobe目标的体验相对应的细分和规则。 这样，品牌网站的访客可以实时显示相同或下一页的超个性化体验（100毫秒以下）。

## 开发计划

实时机器学习目前处于Alpha阶段。 下表概述了预计在未来测试版中发布的一些功能和更新。

<table>
    <th></th>
    <th>Alpha（5月）</th>
    <th>测试版</th>
    <tr>
        <td>
            <strong>功能</strong>
        </td>
        <td>
            <li>Data Science Workspace通过集成笔记本启动器，提供您自己的模型和作者。</li>
            <li>创作操作符的起始集。</li>
            <li>部署到中心</li>
            <li>基于Scikit学习的模型。</li>
        </td>
        <td>
            <li>数据科学工作区服务库UI集成。</li>
            <li>利用推理结果自动丰富实时客户用户档案。</li>
            <li>深入学习模型。</li>
            <li>扩展了包括自定义运算符在内的创作运算符集。</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>可用性</strong>
        </td>
        <td>
            北美洲
        </td>
        <td>
            <li>北美洲</li>
            <li>欧洲和中东(EMEA)</li>
            <li>亚太地区(APAC)</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>创作</strong>
        </td>
        <td>
            <li>Python支持</li>
            <li>实时机器学习SDK</li>
            <li>Python创作节点： Apnotics、ScikitLearn、ONNode、Split、ModelUpload、OneHotEncoder。</li>
        </td>
        <td>
            <li>张力流支持。</li>
            <li>其他Python创作节点： 实时客户用户档案阅读器、实时客户用户档案编写器、Numpy阵列、XDM2Frame、Frame2XDM。 </li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>评分运行时间</strong>
        </td>
        <td>
            ONNX
        </td>
        <td>
            ONNX
        </td>
    </tr>
</table>

## 后续步骤

您可以按照入门指 [南开始](./getting-started.md) 。 本指南将指导您设置创建实时机器学习模型所需的所有先决条件。

