---
title: AI助手自然语言到SQL模型卡
description: 了解AI Assistant自然语言到SQL AI模型。
hide: true
hidefromtoc: true
source-git-commit: 70b705a7c6df24ad9549c46832ff4898253670ac
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# AI助理操作分析自然语言到SQL模型卡

## 模型概述 {#model-overview}

* 模型的正式名称为AI助理操作分析自然语言到SQL模型([!DNL NL2SQL])，并在2025年2月的最新正式发布版本中发布。
* 该模型旨在将客户有关运营见解的自然语言查询转换为SQL查询。 这些SQL查询通过Adobe Experience Platform知识图执行，该图包含有关客户Experience Platform实体（如架构、数据集、受众、目标和历程）的元数据。 然后，SQL查询的结果用于生成对客户原始自然语言问题的响应。
* 此模型的主要用户是营销专业人员、数据分析师或客户历程经理，他们试图使用自然语言理解并运用Experience Platform中的运营见解。 他们可能不是SQL或数据工程方面的专家，而是需要有关其Experience Platform实体的快速、准确答案，以做出明智的决策并优化客户体验。
* 此模型是用于Operational Insights的AI助手的一部分，它可帮助用户访问有关其Experience Platform实体的元数据，例如受众、历程、架构、属性、数据集和目标。 用户可以用自然语言提出问题，例如激活了哪些受众或者哪些受众正在使用特定架构，模型会通过Experience Platform知识图将这些问题转换为SQL查询。 这使用户能够快速获得运营可视性并做出明智的决策，而无需手动探索或查询系统。
* 此模型解决了使用Experience Platform的业务用户和分析师面临的关键棘手问题，例如导航大量互连元数据的复杂性、手动编写SQL查询以检索运营洞察的需要，以及对Experience Platform实体（如受众、数据集和历程）如何连接或执行缺乏可见性。 通过支持对元数据的自然语言访问和自动化SQL生成，该模型减少对技术资源的依赖，缩短了insight发现时间，并使用户能够更快地做出数据驱动型决策。
* 该模型不应用于访问或推断个人身份信息(PII)，例如客户姓名、电子邮件地址或电话号码，即使此类数据存在于平台中。
* 此外，也不应依赖它来执行法规遵从性或治理检查，如验证数据保留策略、访问控制规则或同意状态。 这些任务需要专门的系统和策略。

## 模型详细信息 {#model-details}

* 模型类型为“带动态上下文学习的LLM提示”。
* 模型输入是用户自然语言查询。
* 该模型以[!DNL Snowflake]语法输出SQL查询，这些查询通过Experience Platform知识图执行。

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

## 模型训练 {#model-training}

* [!DNL NL2SQL]已使用[!DNL OpenAI]个基于GPT的模型来进行上下文学习。
* [!DNL NL2SQL]问题库包含来自[!DNL Operational Insights]团队的428个查询和外部团队的524个关于Alpha使用案例的查询。

## 模型评估 {#model-evaluation}

* 模型使用精确度来评估。 例如，在所有[!DNL NL2SQL]请求中，有多少请求产生了正确的SQL结果。
* 评估过程是基于规则的匹配（SQL标准化，然后是直接SQL字符串匹配）、基于LLM的SQL求解器和人工评估的组合
* 开放集用于回归测试，每周注释项目通过采样的实际客户流量监控模型的性能。
* 在对抗性评估方面，有单独的范围和范围外模型，可作为[!DNL NL2SQL]的护栏。

## 模型部署 {#model-deployment}

* LLM模型是基于GPT的模型，由[!DNL Azure OpenAI] API托管。
* 基础模型由[!DNL Azure]托管。
* 通过问题库的扩展，该模型每周定期更新。 模式列表还根据需要通过新的提示策略和指令更新。

## 解释 {#explainability}

该模型对SQL使用单独的说明模型。

## 公平和偏见 {#fairness-and-bias}

* 为确保模型能在不同用户意图和语言变体之间以一致的方式解释和生成查询，而不会引入偏见或强化定型观念，Adobe使用及时审核、解释和防护措施，防止产生有偏见或不道德的输出。
* 模型输出受上下文学习示例以及检索器在提示中选择的内容的影响。 问题银行示例包含从预防性维护的角度看具有代表性的示例，并且我们正在根据真实客户流量扩展问题银行。

## 稳健性 {#robustness}

由于它收到的大部分查询不在问题库中覆盖，因此生产流量的准确性反映了模型的鲁棒性。

## 隐私和安全注意事项 {#privacy-and-security-considerations}

该模型不会处理或保留任何个人身份信息(PII)，并且会屏蔽这些信息以生成SQL。 对于基于属性的访问控制权限检查，生成的SQL将由Experience Platform知识图团队进一步处理，以确保治理质量。

## 道德注意事项 {#ethical-considerations}

为了避免公开PII或敏感属性，该模型旨在支持隐私、避免增强现有数据偏差并尊重访问控制边界。 这包括筛选、标记和审核架构字段，以便负责任地使用。

