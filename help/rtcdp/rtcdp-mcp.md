---
solution: Real-Time Customer Data Platform
title: 使用MCP客户端(Beta)
description: 了解如何使用MCP服务器将Adobe Real-Time CDP连接到MCP客户端
feature: Integrations
topic: Content Management, Artificial Intelligence
badge: label="Beta 版" type="Informative"
role: User, Developer
level: Beginner, Intermediate
hide: true
hidefromtoc: true
exl-id: 48dba0d2-7df9-4d76-bc87-5af49a8a40cc
source-git-commit: 8a9dd740bb210ef125bca65a8358bb6b51f6d28f
workflow-type: tm+mt
source-wordcount: '2379'
ht-degree: 0%

---

# 使用MCP客户端(Beta) {#rtcdp-mcp}

您可以使用Adobe Real-Time CDP MCP集成通过纯语言提示查询受众、目标和激活运行状况，而无需编写API调用或导航产品屏幕。 此页面介绍集成的工作方式、您可以对其执行的操作以及如何入门。

>[!AVAILABILITY]
>
>Real-Time CDP MCP服务器作为&#x200B;**远程HTTP传输服务器**&#x200B;进行分发，用户可以在支持的MCP客户端和应用程序平台（例如，Claude、ChatGPT、Claude Code、Codex、Cursor或VS Code）中安装和配置该服务器。 身份验证通过&#x200B;**基于浏览器的登录流程**&#x200B;来处理 — 当您的客户端首次连接到服务器时，它会打开您的默认浏览器，以便您可以使用您的Adobe凭据登录并授权访问。 请联系您的Adobe代表以访问此Beta计划。

## Beta、安全和法律声明 {#mcp-notices}

**Beta文档声明：**&#x200B;此文档涵盖了Beta的一项功能，并不构成最终文档。 此处描述的内容与Beta版本有关，在正式发布之前可能会发生更改。 Adobe不对本文档的完整性或准确性做出任何表示。

使用Adobe Real-Time CDP MCP Server (Beta) (“Beta”)，即表示您在此确认Beta按“原样”提供&#x200B;**，不提供任何形式的担保**。 Adobe没有义务维护、更正、更新、更改、修改或以其他方式支持Beta。 建议您谨慎使用，切勿依赖此类Beta和/或随附材料的正确功能或性能。 Beta被视为Adobe的机密信息。 您向Beta提供的任何“反馈”（有关Beta的信息，包括但不限于您在使用Adobe时遇到的问题或缺陷、建议、改进和推荐）均会分配给Adobe，其中包括针对该反馈的所有权利、标题和兴趣。

>[!WARNING]
>
>模型上下文协议(MCP)是一种新兴的开源标准，可能会带来安全性或可靠性风险。 Adobe MCP服务器集成和相关文档按“原样”提供，不提供任何类型的担保。
>
>将MCP客户端或服务器连接到Adobe产品是客户选择的配置。 客户负责评估任何MCP集成的安全性和适用性。 Adobe对于因错误配置、滥用MCP、第三方实施中的漏洞或通过支持MCP的工作流执行的意外操作而产生的问题，概不负责。
>
>为了降低风险，Adobe鼓励您在生产使用之前在沙盒环境中测试集成，并在确认或依赖集成之前，仔细审查和验证所有MCP启动的操作和响应。

## 什么是模型上下文协议？ {#mcp-overview}

营销、数据和客户体验团队日益依赖基于聊天的应用程序和开发人员工具（如Anthropic Claude、OpenAI ChatGPT、Cursor和Microsoft Copilot Studio）来简化日常工作。 这些应用程序支持&#x200B;**模型上下文协议(MCP)**，这是一个开放标准，允许应用程序以统一的方式向大型语言模型(LLM)公开后端工具。

Real-Time CDP现在提供了一个MCP服务器，可直接在任何MCP兼容的应用程序中呈现受众、目标和激活操作。 借助Real-Time CDP MCP集成，不同的角色可以围绕相同的分段和激活数据展开协作 — 无需针对Adobe Experience Platform REST API编写查询或导航多个UI屏幕。 客户可以通过对话方式描述其意图，并让LLM调用相应的MCP工具。

## 主要功能 {#mcp-capabilities}

Real-Time CDP MCP服务器允许您直接从AI助手检查、汇总受众和目标并对其进行故障排除。 所有操作都是&#x200B;**只读** — MCP服务器表面将API作为纯语言答案进行检索，因此您可以：

* **即时查看受众** — 无需导航菜单或手动提取报表，即可以纯语言询问受众定义、生命周期状态和命名空间。
* **在激活前估计受众大小** — 在承诺构建受众之前，预览PQL或SDD区段查询的成员资格计数和置信区间。
* **审核您的激活组合** — 审核已配置的目标、提供这些目标的数据流，以及每个流背后的源/目标连接，而无需解析JSON或跨产品屏幕跳转。
* **提早发现激活问题** — 表面失败或正在进行的目标在您询问时运行，以便您的团队可以快速行动。
* **围绕实时数据开展协作** — 营销人员、数据工程师和利益相关者均可通过其AI助手查询相同的实时Real-Time CDP数据，从而更轻松地保持一致、决策和移动。

## 可用工具 {#mcp-tools}

当我们启用新工具时，工具可用性正在迅速变化。 请联系您的Adobe代表以获取最新可用工具的列表。

>[!NOTE]
>
>所有工具均为&#x200B;**只读**。 当前Beta版本不支持写入操作（创建、更新或删除受众、目标或数据流）。

## 用例 {#mcp-use-cases}

以下示例显示如何使用自然语言与[!DNL Adobe Real-Time CDP] MCP服务器交互：

| 目标 | 示例提示 |
| --- | --- |
| **目标目录发现** | “TikTok能否作为我的沙盒中的目标？” /“我已为其配置了哪些目标类型？” |
| **目标清单（按类型）** | “列出我的所有Amazon S3目标。” / “我是否设置了任何数据集导出目标？” |
| **目标配置审核** | “我的`Loyalty S3 Export`目标正在写入哪个存储桶？” /“显示数据流[ID]的目标路径和文件格式。” |
| **帐户运行状况** | “我的哪些目标帐户凭据已过期？” / “是否有任何Pinterest或Facebook帐户处于错误状态？” |
| **激活运行状况 — 过去24小时** | “列出过去24小时内运行失败的每个目标。” /“我的数据集导出目标在过去24小时内是否发送了任何数据？” |
| **按目标列出的激活历史记录** | “`Weekly Loyalty Export`是否导出过去30天中的任何内容？” /“显示目标{NAME}的完整运行历史记录。” |
| **失败分析** | “对于本周基于文件的目标，最常见的失败原因是什么？” /“按错误类型对最近失败的运行进行分组。” |
| **受众发现和筛选** | “列出`marketing-prod`沙盒中每个基于CSV的受众。” /“哪些受众定义了外部受众ID？” |
| **受众规模调整审核** | “给我看看身高为0的所有受众。” / “哪些受众的用户档案超过1,000个？” |
| **受众过期审核** | “哪些目标具有结束日期已过的受众？” /“列出计划在未来7天内过期的受众。” |
| **受众激活占用空间** | “哪些目标激活了10个以上的受众？” /“哪个受众被激活到了大多数目标？” |
| **跨筛选器：受众×激活** | “向我显示大小大于1,000且至少在2个目标上激活的受众。” /“仅激活到单个目标的大型受众。” |
| **受众成员资格预览** | “预览受众`High-Value Loyalty Members`的成员资格大小。” /“在保存此PQL查询之前估计其大小： {EXPRESSION}。” |

## 先决条件 {#mcp-prerequisites}

在将Real-Time CDP MCP服务器连接到MCP客户端之前，请确保：

* 您拥有有效的Real-Time CDP许可证。
* 您可以访问可连接到远程MCP服务器或自定义MCP应用程序的受支持客户端，例如Claude、ChatGPT、Claude Code、Codex、Cursor或VS Code。
* 您拥有组织ID以及要查询的沙盒的名称。
* 您在Adobe Experience Platform中拥有查看受众、目标和流服务实体的必要权限。

## 连接Real-Time CDP MCP服务器 {#mcp-connect}

>[!NOTE]
>
>此集成位于Beta中。 客户端菜单、计划要求和管理控件可能因应用程序和版本而异。

在开始之前，请确保您具备以下条件：

* MCP服务器终结点URL： `Available to Beta customers through your Adobe representative`。
* 确认您的Adobe用户有权访问目标Experience Platform组织和沙盒。

Real-Time CDP MCP服务器是&#x200B;**远程HTTP MCP服务器**。 在每个客户端中，设置遵循相同的模式：

1. 添加服务器URL。
2. 保存或启用连接。
3. 在客户端首次调用工具时完成&#x200B;**基于浏览器的Adobe登录**。
4. 为每个请求提供`imsOrgId`和`sandboxName`。

### 在基于UI的客户端中安装 {#mcp-connect-ui}

#### 克劳德

对于`claude.ai`和Claude Desktop，使用Real-Time CDP代表提供的端点将Adobe MCP服务器添加为&#x200B;**自定义连接器**。 在单个Claude计划中，将其添加到&#x200B;**自定义>连接器**&#x200B;下。 在“团队”和“企业”计划中，所有者可能需要先在&#x200B;**组织设置>连接器**&#x200B;下添加它，然后每个用户使用他们自己的“克劳德”设置连接它。 配置完毕后，在对话中启用连接器，并在首次使用时完成Adobe浏览器登录。

#### ChatGPT

在ChatGPT中，使用Real-Time CDP代表提供的端点将Adobe MCP服务器添加为&#x200B;**自定义应用程序/连接器**。 根据您的ChatGPT计划，这可能需要&#x200B;**开发人员模式**&#x200B;和工作区管理员批准。 创建或启用应用程序/连接器后，从&#x200B;**设置>应用程序**&#x200B;或&#x200B;**设置>应用程序和连接器**&#x200B;中连接该应用程序/连接器，然后在出现提示时通过Adobe浏览器登录进行身份验证。

#### 光标

在光标中，使用Real-Time CDP代表提供的端点将Adobe MCP服务器添加为远程MCP服务器。 打开&#x200B;**设置> MCP**，添加新服务器，并粘贴终结点URL。 添加后，选择&#x200B;**连接**&#x200B;以通过浏览器进行身份验证，为您的工作区启用服务器。

#### 其他基于用户界面的客户端

对于客户端（如VS Code或其他支持远程MCP的桌面和Web应用程序），请使用Real-Time CDP代表提供的端点将Adobe MCP服务器添加为&#x200B;**远程HTTP**&#x200B;服务器。 如果客户端支持可选标头或持有者令牌，请将其留空，除非Adobe另有说明；身份验证在首次使用时通过基于浏览器的Adobe登录流处理。

### 在技术客户端中安装 {#mcp-connect-technical}

#### Claude码

从终端添加服务器：

```bash
claude mcp add --transport http rtcdp <endpoint provided by your Adobe representative>
```

然后启动Claude Code并运行：

```text
/mcp
```

选择`rtcdp`服务器并在浏览器中完成Adobe登录流程。 如果已在`claude.ai`中添加服务器，则当两者使用同一帐户时，该服务器也会自动显示在Claude代码中。

#### 法典

从终端添加服务器：

```bash
codex mcp add rtcdp --url <endpoint provided by your Adobe representative>
```

验证服务器：

```bash
codex mcp login rtcdp
```

验证配置：

```bash
codex mcp list
```

您还可以将服务器直接添加到`~/.codex/config.toml`：

```toml
[mcp_servers.rtcdp]
url = "<endpoint provided by your Adobe representative>"
```

### 必需的请求参数 {#mcp-connect-params}

每个工具调用都需要两个参数来限定请求的范围：

* `imsOrgId` — 您的组织ID，在下游Experience Platform API调用中映射到`x-gw-ims-org-id`标头。
* `sandboxName` — Experience Platform沙盒名称，已映射到`x-sandbox-name`标头。

## 已知限制(Beta) {#mcp-limitations}

以下限制适用于[!DNL Adobe Real-Time CDP] MCP服务器的当前Beta版本：

| 限制 | 描述 | 解决方法 |
| --- | --- | --- |
| **只读表面** | MCP服务器仅公开检索API。 您无法创建、更新、激活或删除受众、目标或数据流。 | 使用Real-Time CDP UI或AEP REST API执行写入操作。 |
| **没有参与或传递量度** | MCP服务器不会从目标平台返回下游投放统计信息、参与或转化量度。 | 使用目标平台自己的报表、Customer Journey Analytics MCP或Adobe Analytics MCP获取参与和转化数据。 |
| **区段查询必须在外部创作** | `Preview Audience Membership`需要有效的PQL或SDD表达式作为输入；MCP服务器不会为您撰写查询。 | 在区段生成器UI中或通过分段服务API创作PQL/SDD表达式，然后粘贴到MCP提示符下。 |
| **通过继续令牌分页** | 列表工具返回分页结果。 超大型沙盒中的完整枚举需要链接`continuationToken`调用。 | 使用过滤器（名称、状态、连接规范、时间范围）而不是枚举完整列表来缩小查询。 |
| **激活运行筛选仅基于时间** | `Inspect Activation Runs`支持按状态和完成时间戳（纪元毫秒UTC）进行筛选，但不支持直接按错误类型或目标平台进行筛选。 | 首先按`flowId`筛选（从`List Configured Destinations`获取），以将运行范围限定到特定目标。 |
| **需要区域配置** | 如果没有为用户所在的区域配置MCP网关，则工具调用将失败，并且HTTP 403“用户区域缺失”。 | 在首次使用之前，请联系您的Adobe代表，以确认为您所在的地区配置了网关。 |

## 常见问题 {#mcp-faq}

+++支持哪些MCP客户端？

Real-Time CDP MCP服务器可与受支持的客户端配合使用，这些客户端可以连接到远程MCP服务器或自定义MCP应用程序，包括Claude、ChatGPT、Claude Code、Codex、Cursor和VS Code。 设置流程取决于客户端：基于UI的客户端通常从设置添加服务器，而技术客户端（如Claude Code和Codex）可以从命令行或配置文件添加服务器。
+++

+++身份验证如何工作？

身份验证是通过基于&#x200B;**浏览器的登录**&#x200B;处理的。 当MCP客户端首次调用某个工具时，它将打开默认浏览器以访问Adobe登录页面。 在对客户端进行身份验证和授权后，将会建立会话，后续工具调用会重复使用它。 您的客户端配置中无需存储API密钥或长效凭据。
+++

+++我可以通过MCP访问哪些Real-Time CDP对象？

您可以访问受众、目标类型、配置的目标帐户、目标数据流、源和目标连接以及激活运行历史记录。 操作是只读的（检索API）；当前版本不支持写入操作。
+++

+++要使用Real-Time CDP MCP服务器，是否需要开发人员访问权限？

不是。 MCP服务器专为营销和技术人员而设计。 营销人员可以在任何支持的MCP客户端中使用自然语言提示与其交互，而数据工程师和开发人员可以在支持MCP的开发人员工具中使用它。
+++

+++我的数据是否发送到MCP客户端提供商？

当您提交提示时，MCP客户端可能会将相关上下文（包括MCP服务器返回的Real-Time CDP数据）发送到其模型以供处理。 在连接到生产数据之前，请查看MCP客户端提供商的隐私和数据处理策略。
+++

+++在Real-Time CDP中需要什么权限？

您需要对要查询的对象（受众、目标和流服务实体）具有至少&#x200B;**查看**&#x200B;权限。 不需要写入权限，因为MCP服务器只执行读取操作。 如果您不确定当前的访问级别，请联系您的[!DNL Adobe Experience Platform]管理员。
+++

+++我可以在沙盒环境中使用MCP服务器吗？

可以。 每次工具调用都需要一个`sandboxName`参数，因此MCP服务器始终遵循您的[!DNL Adobe Experience Platform]沙盒配置。 通过在提示中指定沙盒的名称，可以查询您有权访问的任何沙盒。
+++

+++预览受众成员资格与搜索现有受众之间有何区别？

`Search Existing Audiences`返回已创作并保存在沙盒中的受众。 `Preview Audience Membership`采用原始PQL或SDD区段表达式并返回其大小估计值 — 对于在将查询另存为受众之前&#x200B;*调整其大小非常有用。*
+++

+++我是否可以查询帐户受众以及配置文件受众？

可以。 `Search Existing Audiences`和`Preview Audience Membership`都支持实体类型参数。 配置文件受众可以用PQL或SDD表示；帐户受众始终使用SDD（关系）语法。
+++
