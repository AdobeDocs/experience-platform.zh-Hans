---
title: AI助手自然语言到SQL模型详细信息
description: 了解AI Assistant自然语言到SQL AI模型。
exl-id: ca157945-5f74-45d0-9d40-c65d09a8e80d
source-git-commit: 26d05e9519491ef2e8f239cba6a2cde43cff941c
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# AI助理操作分析自然语言到SQL模型详细信息

>[!IMPORTANT]
>
>Adobe正在积极发布更多模型详细信息；当有其他文档可用时，会将其添加到Experience League。

## 模型概述 {#model-overview}

* **模型名称和版本**： Adobe Experience Platform AI Assistant操作分析自然语言到SQL模型([!DNL NL2SQL])。
* **模型发布日期**：2025年2月
* **模型目的**：模型旨在将客户有关操作见解的自然语言查询转换为SQL查询。 这些SQL查询通过Adobe Experience Platform知识图执行，该图包含有关客户Experience Platform实体（如架构、数据集、受众、目标和历程）的元数据。 然后，SQL查询的结果用于生成对客户原始自然语言问题的响应。
* **目标用户**：此模型的主要用户是营销专业人员、数据分析师或客户历程经理，他们试图使用自然语言理解并处理Experience Platform中的运营洞察。 他们可能不是SQL或数据工程方面的专家，而是需要有关其Experience Platform实体的快速、准确答案，以做出明智的决策并优化客户体验。
* **用例**：此模型可帮助用户访问有关其Experience Platform实体的元数据，如受众、历程、架构、属性、数据集和目标。 用户可以用自然语言提出问题，例如激活了哪些受众或者哪些受众正在使用特定架构，模型会通过Experience Platform知识图将这些问题转换为SQL查询。 这使用户能够快速获得运营可视性并做出明智的决策，而无需手动探索或查询系统。
* **痛点**：此模型解决了使用Experience Platform的业务用户和分析师所面临的关键痛点，例如导航大量互连元数据的复杂性、手动编写SQL查询以检索运营洞察信息的需要，以及对Experience Platform实体（如受众、数据集和历程）如何连接或执行缺乏可见性。 通过支持对元数据的自然语言访问和自动化SQL生成，该模型减少对技术资源的依赖，缩短了insight发现时间，并使用户能够更快地做出数据驱动型决策。

## 模型详细信息 {#model-details}

* **模型类型**：具有动态上下文学习的LLM提示
* **输入**：用户自然语言查询。
* **输出**：模型输出[!DNL Snowflake]语法的SQL查询，将通过Experience Platform知识图执行。

**示例输入**

```console
How many datasets were created within the last 10 days?
```

**示例输出**

```SQL
SELECT
    COUNT(*) AS datasetCount 
FROM hkg_dim_dataset 
WHERE
    createdTime >= DATEADD(day, -10, CURRENT_DATE);
```

## 模型评估 {#model-evaluation}

* **评估量度和过程**：通过查看[!DNL NL2SQL]个请求并评估有多少个请求产生了正确的SQL结果来评估模型。 评估过程是基于规则的匹配（SQL标准化，然后是直接SQL字符串匹配）、基于LLM的SQL求解器和人工评估的组合。
* **评估数据和预处理**：我们使用开放集进行回归测试，并且我们还有每周的注释项目通过采样的实际客户流量来监视模型的性能。

## 模型部署 {#model-deployment}

* **模型监视**：基本模型由[!DNL Azure]托管。
* **模型更新**： Adobe Experience Platform AI Assistant Operational Insights Natural Language to SQL Model通过问题库扩展定期（每周）更新。 如果需要，还可以通过新的提示策略和指令更新模型。

## 公平和偏见 {#fairness-and-bias}

* **模型公平性**：为确保模型能在不同用户意图和语言变体之间以一致的方式解释和生成查询，而不引入偏见或强化定型观念，Adobe使用及时审核、解释和防护措施防止生成有偏见或不道德的输出。
* **数据偏差**：模型输出受In-Context Learning示例以及检索器在提示中选择的内容影响。 问题库示例包含从产品管理的角度被视为具有代表性的示例。 根据用例，客户应考虑模型输出中的潜在偏差如何与其预期应用程序一致或影响。

## 道德注意事项 {#ethical-considerations}

**与模型相关的道德考量**：为了避免公开PII或敏感属性，模型已设计为避免增强现有的数据偏差并遵守访问控制边界。 这包括筛选、标记和审核架构字段，以便负责任地使用。
