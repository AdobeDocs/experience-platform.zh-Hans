---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Adobe Experience Platform术语表
topic-legacy: getting started
description: Experience Platform 重要术语词汇表。
exl-id: 00eae5f5-7dfa-45ac-aff9-9e1769a3a53a
source-git-commit: c0f01efa224bffb5b435e2f247e793edfbc576b9
workflow-type: tm+mt
source-wordcount: '7428'
ht-degree: 0%

---

# Adobe Experience Platform 术语表 {#adobe-experience-platform-glossary}

## A

**访问控制**:基于角色的访问控制使管理员能够向Experience Platform用户分配访问权限和权限。 权限包括查看和/或使用Experience Platform功能的功能，例如创建沙箱、定义架构和管理数据集。

**访问密钥ID**:访问密钥ID是与 [!DNL Amazon] S3密钥访问密钥。 访问密钥ID和密钥访问密钥一起用于签名 [!DNL Amazon Web Services] (AWS)请求。

**操作**:在标记的上下文中，操作是一种特定类型的规则组件，用于定义事件发生后应当发生的情况，以及评估和传递条件。

**激活**:激活是用户将区段或用户档案映射到目标(如 [!DNL Oracle Eloqua], [!DNL Google]或 [!DNL Salesforce Marketing Cloud].

**活动**:在 [!DNL Offer Decisioning]，则活动包含用于通知选件选择的逻辑。

**管理员**:您组织中一位或多位个人，可以在Adobe Admin Console中配置和自定义Experience Platform权限。

**Adobe Admin Console**:Adobe Admin Console提供了一个中心位置，用于管理Adobe产品权利和贵组织的访问权限。 通过控制台，管理员可以向用户组授予各种Platform功能（如“管理数据集”、“查看数据集”或“管理配置文件”）的访问权限。

**Adobe Experience Platform**:Adobe Experience Platform实现了整个企业中的数据和内容的标准化，为实时消费者用户档案提供强大动力，支持数据科学，并加快内容速度以推动客户历程中的体验个性化。

**Adobe Experience Platform查询服务**:使数据分析人员能够查询事件和配置文件，以用于分析和机器学习。 借助查询服务，数据科学家和分析人员可以提取他们存储在Experience Platform中的所有数据集(包括行为数据以及销售点(POS)、客户关系管理(CRM)等)，并查询这些数据集以回答有关数据的特定问题。

**Adobe Experience Platform Segmentation Service**:支持根据实时客户资料数据生成区段和生成受众。 然后，可以将这些受众导出到数据湖中他们自己的数据集。

**Adobe智能服务**:智能服务(如Attribution AI和Customer AI)是基于机器学习和人工智能的模型，这些模型是专门构建的，需要Experience Platform来运行和操作。

**Adobe I/O**:Adobe I/O是Experience Platform的一部分，可让开发人员访问集成、扩展和自定义平台所需的所有功能，包括API、事件、开发人员控制台和有用的工具。

**Adobe Sensei**:Adobe Sensei是支持Experience Platform的情报框架。 它还提供了一套AI服务，使品牌能够增强提供实时、个性化客户体验的能力。

**Amazon S3存储段**: [!DNL Amazon S3] 存储段是存储在 [!DNL Amazon] 生态系统。 存储段包含对象，每个对象都使用由开发人员分配的唯一密钥进行存储和检索。

**Amazon S3连接器**:的 [!DNL Amazon] S3连接器允许Experience Platform客户安全地连接和访问其 [!DNL Amazon] S3数据。

**附加保存策略**:“追加”保存策略是指定要通过连接摄取的第三方数据，并在数据集末尾附加任何新数据或行时使用的选项。 之前摄取的行将保持不变，并且只会将自上次计划运行后创建的行摄取到Experience Platform。 在源系统中更改的任何行在Experience Platform时均保持不变。

**数组**:数组用于具有相同数据类型的已排序元素。

**人工智能**:人工智能是计算机系统的理论和发展，能够执行通常需要人类智能的任务，如视觉感知、语音识别、决策和语言之间的翻译。

**属性**:属性是指表示用户档案的特征。

**属性合并**:使用实时客户资料API定义合并策略时， `attributeMerge` 对象指示在发生数据冲突时合并策略优先处理配置文件属性的方式。 它等同于选择 [!UICONTROL 合并方法] 在平台UI中定义合并策略时。

**Attribution AI**: [!DNL Attribution AI] 是一项由Adobe Sensei提供支持的智能服务，可在整个客户生命周期中提供算法多渠道归因功能。

**受众**:受众是指生成的一组符合区段定义标准的用户档案。

**受众大小**:受众规模是指符合区段定义标准并符合受众成员资格的用户档案总数。

**受众快照**:受众快照会捕获在分段时符合区段标准的所有用户档案。

## B

**回填**:对于计划的源，回填选项允许摄取历史数据。

**回填期**:回填期是一个选项，用于设置通过源连接摄取第三方历史数据的时长。 选择“forever”的回填期将摄取源数据的整个历史记录以Experience Platform。

**批次**:批处理是在一段时间内收集并作为单个单位一起处理的一组数据。 数据集由多个批次组成。

**批处理ID**:批量ID是Adobe生成的批量数据标识符。

**批量摄取**:批量摄取允许您将数据作为批处理文件导入到Experience Platform中。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。

**批量分段**:批量分段是持续数据选择流程的一种替代方法，可一次通过区段定义移动所有配置文件数据以生成相应的受众。 创建此区段后，会保存并存储该区段，以便导出以供使用。

**生成**:在标记的上下文中，内部版本是一个文件或一组文件，其中包含执行库中包含的业务逻辑所需的所有配置和代码，允许您在网站或移动设备应用程序上部署该库。

**商业智能工具**:业务智能(BI)工具主要与 [!DNL Experience Platform Query Service]. BI工具是从内部和外部系统收集和处理大量非结构化数据的应用程序软件类型。

## C

**上限**:在 [!DNL Offer Decisioning]，在决策规则中使用上限（也称为频率上限）来定义选件的显示次数。 大写有两种类型：在合并的目标受众中，可以提出选件多少次（称为“全局上限”），以及可以向同一最终用户建议选件多少次（称为“配置文件上限”）。

**目录**:在源和目标的背景下，目录是一个图库，其中具有与Adobe应用程序和第三方技术的可用连接。 不要搞混 [!DNL Catalog Service].

**[!DNL Catalog Service]**: [!DNL Catalog Service] (有时称为 [!DNL Catalog])是Adobe Experience Platform中数据位置和谱系的记录系统。 虽然摄取到Experience Platform的所有数据都作为文件和目录存储在数据湖中， [!DNL Catalog] 包含这些文件和目录的元数据和描述，用于查找、监控和数据管理。

**类**:在体验数据模型(XDM)中，类定义用于构建架构的最小字段集，并定义架构所表示的业务对象的基本行为。

**客户端**:客户端是连接到 [!DNL Query Service] 通过PostgreSQL协议或HTTP API。

**收藏集**:在 [!DNL Offer Decisioning]，收藏集是基于营销人员定义的预定义条件（如选件的类别）的选件子集。

**与PII营销操作结合使用**:将任何个人身份信息(PII)与匿名数据相结合的营销操作。 来自广告网络、广告服务器和第三方数据提供商的数据合同通常包括禁止使用具有直接可识别数据的此类数据的具体合同。

**命令行界面**:命令行界面是基于文本的工具，可用于连接到 [!DNL Query Service] 用于执行原始查询。

**组合物**:组合是一组组件，这些组件一起组成了架构。

**条件**:在标记的上下文中，条件是一个规则组件，用于评估必须返回的逻辑语句 `true` 或 `false`. 所有条件都必须评估为 `true` 和所有例外条件都必须评估 `false` 执行规则上的任何操作之前。

**控制台**:在 [!DNL Query Service]，则控制台会提供有关查询状态和操作的信息。 控制台将显示与 [!DNL Query Service]、正在执行的查询操作以及从这些查询产生的任何错误消息。

**合同(&quot;C&quot;)标签**:合同(“C”)数据使用标签用于对具有合同义务或与客户数据管理策略相关的数据进行分类。

**C1合同标签**:A `C1` 合同数据使用标签指定只能以聚合形式从Adobe Experience Cloud导出数据，而不包含单个或设备标识符。 例如，源自社交网络的数据。

**C2合同标签**:A `C2` 合同数据使用标签指定无法导出到第三方的数据。 一些数据提供商在其合同中订有条款，禁止从最初收集的地方导出数据。 例如，社交网络合同通常会限制您从这些合同中收到的数据的传输。 C2比C1的限制更多，C1仅需要聚合和匿名数据。

**C3合同标签**:A `C3` 合同数据使用标签指定不能与直接可识别信息组合或以其他方式使用的数据。 某些数据提供商在其合同中订有条款，禁止合并或使用具有直接可识别信息的数据。 例如，来自广告网络、广告服务器和第三方数据提供商的数据合同通常包括禁止使用直接可识别数据的具体合同。

**C4合同标签**:A `C4` 合同数据使用标签指定数据不能用于定位任何广告或内容（现场或跨站点）。 C4是最严格的标签，因为它包含C5、C6和C7标签。

**C5合同标签**:A `C5` 合同数据使用标签指定数据不能用于基于兴趣的内容或广告的跨站点定位。 如果满足以下三个条件，则会进行基于兴趣的定位或个性化：现场收集的数据用于推断用户的兴趣；用于其他上下文，如在其他网站或应用程序上；和用于根据这些引用选择提供哪些内容或广告。

**C6合同标签**:A `C6` 合同数据使用标签指定数据不能用于现场广告定位。 现场广告定位包括在您组织的网站或应用程序上选择和投放广告，或衡量此类广告的投放和效果。 这包括使用先前收集的有关用户兴趣的现场数据来选择广告，处理有关显示了哪些广告、何时何地显示广告以及用户是否采取了与广告相关的任何操作（如选择广告或购买广告）的数据。

**C7合同标签**:A `C7` 合同数据使用标签指定数据不能用于内容的现场定位。 现场内容定位包括在您组织的网站或应用程序上选择和交付内容，或用于衡量此类内容的交付和有效性。 这包括以前收集的有关用户选择内容的兴趣、处理有关显示内容的数据、显示内容的频率或时长、显示时间和位置，以及用户是否执行了与内容相关的任何操作（例如选择内容）的信息。

**C8合同标签**:A `C8` 合同数据使用标签指定数据不能用于测量贵组织的网站或应用程序。 这不包括基于兴趣的定位，即关于您使用此服务以后在其他环境中个性化内容和/或广告的信息集合。

**C9合同标签**:A `C9` 合同数据使用标签指定数据不能在数据科学工作流中使用。 一些合同明确禁止用于数据科学的数据。 有时，这些措辞的措辞禁止将数据用于人工智能(AI)、机器学习(ML)或建模。

**C10合同标签**:A `C10` 合同数据使用标签指定数据不能用于拼合身份激活。 某些数据使用策略会限制使用拼合身份数据进行个性化。 的 `C10` 如果区段的合并策略使用“专用图”选项，则会自动将标签应用于这些区段。

**创建日期列**:选择创建日期列是通过源连接指定第三方数据时的一个选项。 选择附加保存策略且数据集架构包含多个日期字段时，您必须从可用架构中进行选择以指定“创建日期”键列。 选择覆盖保存策略后，“创建日期”选项将不可用。

**创建选定表**:Create Table as Select(CTAS)是SQL命令，在作为完整有效SQL查询的一部分执行时，该命令将指示 [!DNL Query Service] 将查询结果保留在数据集中。 可以创建新结果集、覆盖先前的结果或附加到先前的结果。

**跨站点数据**:跨站点数据是来自多个站点的数据的组合，包括站点数据和站点外数据的组合，或来自多个站点外源的数据的组合。

**跨站点定位营销操作**:使用数据进行跨站点广告定位的营销操作。 来自多个网站的数据组合（包括网站数据和网站外数据的组合或来自多个网站外来源的数据组合）称为跨网站数据。 通常会收集并处理跨站点数据，以便对客户兴趣做出推论。

**自定义身份命名空间**:您的组织可以创建自定义身份命名空间，以表示特定组织或业务案例的身份。

**自定义标签**:自定义数据使用标签允许您创建特定标签并将其应用于满足特定业务需求的数据字段。

**客户人工智能**:客户人工智能是由Adobe Sensei提供支持的智能服务，可通过基于人工智能的倾向性来丰富客户档案，并支持客户细分和定位工作。

## D

**每日**:在计划文件导出的上下文中，计划完整或增量文件导出每天一次，从开始日期到结束日期的时间（由用户指定的时间）。

**数据字典**:在标记的上下文中，数据字典（也称为数据映射）是在属性中定义的一组数据元素。

**数据元素**:在标记的上下文中，数据元素是规则和扩展中使用的指针，用于指向客户端设备上存在的特定数据段。

**数据摄取**:数据摄取是将数据从源添加到Experience Platform的过程。 可以通过多种方式将数据摄取到平台，包括通过源连接器进行流、批量处理或添加。

**数据层**:在标记的上下文中，数据层是客户端设备上存在的数据结构，其中包含有关在其中查看页面或屏幕的上下文的元数据。

**数据管理**:数据管理包括用于确保数据符合有关数据使用的法规和组织政策的战略和技术。

**数据集成合作伙伴**:数据集成合作伙伴可简化并自动化从200多个源向Experience Platform的大量数据的加载和转换，而无需编写代码。

**数据集标签**:数据使用情况标签可以添加到数据集。 该数据集中的所有字段都将继承该数据集的标签。

**数据科学工作区**: [!DNL Data Science Workspace] 在Experience Platform内，客户能够利用跨平台的数据和Adobe应用程序创建机器学习模型，以创建智能区段、生成洞察并提供预测，从而大大增强最终用户的数字体验。

**数据源**:数据源是用户指定的数据源。 数据源的示例包括移动设备应用程序、用户档案和/或体验事件、网站用户档案事件或CRM。

**数据管理**:数据管理员是负责管理、监督和执行组织数据资产的人员。 数据管理人员还确保数据管理政策得到维护和维护，以符合政府法规和组织政策。

**数据流**:数据流是一组或一组消息，这些消息共享相同的架构并由同一来源发送。

**数据类型**:数据类型是可重用的XDM资源，它定义一个对象类型字段，该字段在分层表示中包含多个属性。

**数据使用标签**:数据使用标签允许您对反映隐私相关考虑因素和合同条件的数据进行分类，以符合法规和公司政策。 添加到数据集的数据使用情况标签将被继承下来或应用于该数据集中的所有字段。 数据使用情况标签也可以直接应用于字段。

**数据流**:数据流是从源流入平台并流出目标的虚拟数据管道。

**数据流运行**:数据流运行是根据用户指定的调度登陆Experience Platform的数据流。

**数据集**:数据集是用于数据集合（通常是表）的存储和管理结构，其中包含架构（列）和字段（行）。

**数据集ID**:摄取的数据集的Adobe生成的标识符。

**数据集输出**:数据集输出提供了一种机制来确定“将表格创建为选择”选项将用于特定 [!DNL Query Service] 运行。

**重复数据删除键**:用户定义的主键，用于确定用户希望用户档案删除重复项时所依据的身份&#x200B;。

**“增量”列**:增量列允许您选择源数据字段来表示增量摄取的时间戳。

**增量保存策略**:增量保存策略是用于通过源连接摄取第三方数据的选项。 利用选项，可指定将新行或更改的源数据行摄取到Experience Platform。 新行将添加到数据集的末尾，更改的行将在Experience Platform的数据集中进行更新。

**描述符**:在体验数据模型(XDM)中，描述符是一组额外的与架构相关的元数据，用于描述字段的特定行为。 描述符可供Experience Platform用来了解预期的模式行为，如两个模式之间的关系。

**目标**:目标是任何端点(例如激活和交付受众的Adobe应用程序、广告平台、云存储服务或营销服务)的一般术语。

**目标类别**:目标类别是具有相似特征的目标的分组。

**目标目录**:目标目录是Experience Platform中可用目标的列表。

**直接调用规则**:在标记上下文中，直接调用规则是在直接从页面调用时执行的规则，绕过事件检测和查找系统。

**显示名称**:在体验数据模型(XDM)中，显示名称是UI中显示的字段的用户友好名称。

## E

**合格选件**:符合条件的选件可始终如一地提供给用户档案，因为它符合上游定义的限制条件。

**资格规则**:在 [!DNL Offer Decisioning]，则资格规则将应用于与日历、计划和上限约束相关的配置文件。

**电子邮件定位营销操作**:在电子邮件定位营销活动中使用数据的营销操作。

**嵌入代码**:在标记的上下文中，嵌入代码是放置在网站或环境的HTML中的脚本标记。 嵌入代码会指示浏览器在何处检索内部版本。

**明细列表**:枚举（枚举）是一个XDM字段，受一组预定义值的约束。

**环境**:在标记的上下文中，环境是一组部署指令，用于指定内部版本的主机交付和文件格式。 库必须先与环境相配对，然后才能构建。

**错误诊断**:错误诊断允许为摄取的批生成详细的错误消息。 错误阈值允许您在批处理失败之前配置可接受错误的百分比。

**事件**:在标记的上下文中，事件是特定类型的规则组件，它是在客户端设备上发生的用于开始执行规则的触发器。

**事件实体**:在数据建模的上下文中，事件实体表示与客户可以执行的操作、系统事件或您希望跟踪随时间变化的任何其他概念相关的概念。 属于此类别的实体应由基于 [!DNL XDM ExperienceEvent] 类。

**事件**:事件是与用户档案关联的行为数据。

**体验数据模型(XDM)** [!DNL Experience Data Model] (XDM)是一个开源框架，它使用标准架构来统一数据，以便与Experience Platform和Adobe Experience Cloud应用程序一起使用。 XDM实现了数据结构的标准化，并加快了速度，简化了从大量数据中获取洞察信息的过程。

**实验**:实验是通过使用实时生产数据的样本部分来训练实例来创建训练过的模型的过程。 这与针对维持测试数据集进行测试的已培训模型不同。 这也与一些机器学习框架中的实验概念不同，在这些框架中，实验实际上意味着一个示例建模项目。

**体验事件**:体验事件表示在发生与客户体验相关的交互或事件时系统的快照。 体验事件是所发生事件的不可变事实记录，它表示所发生的事件，而不进行聚合或解释。 在体验数据模型(XDM)中，此概念由 [!DNL XDM ExperienceEvent] 类。

**导出完整文件**:一个导出文件，其中包含选定区段的所有配置文件资格的完整快照。

**导出增量文件**:一系列导出文件，其中第一个文件是所选区段所有配置文件资格的完整快照，而后续文件是自上次导出以来的增量配置文件资格。

**扩展**:在标记的上下文中，扩展是添加到标记属性的一组功能。 扩展通常以特定营销或分析解决方案为中心，并提供将该技术部署到客户端环境所需的工具。

**扩展包**:在标记上下文中，扩展包是扩展开发人员创建并上传的ZIP文件，可提供标记用户在其资产中安装扩展所需的一切功能。 扩展包包含一个清单，该清单指定有关该扩展的信息、最终用户配置标记扩展行为所需的HTML/JavaScript，以及交付到客户端环境的可执行JavaScript（如果需要）。

## F

**后备优惠**:备用选件是当最终用户不符合所用集合中的任何选件的条件时显示的默认选件。

**功能映射**:特征映射是指将特征从数据映射到机器学习模型所需的输入和目标特征的过程。

**字段**:字段是数据集中级别最低的元素，由数据集的XDM架构定义。 每个字段都有一个用于引用的名称，以及一个用于指示其所包含数据类型的类型。 字段类型可以包括（但不限于）整数、数字、字符串、布尔值和对象。

**字段组**:请参阅“架构字段组”。

**字段标签**:字段标签是从数据集继承或直接应用于字段的数据管理标签。

**字段名称**:字段名称用于引用查询和下游服务中字段的值。

**频率**:在 [!DNL Query Service]，频度决定定期计划查询的运行频率。

## G

**地理围栏**:地理围栏是由GPS或RFID技术定义的虚拟地理边界，它使软件能够在移动设备进入或离开特定区域时触发响应。

**GDPR（《通用数据保护条例》）**:《通用数据保护条例》(GDPR)是一项法律框架，旨在为在欧盟(EU)内收集和处理个人信息制定准则。 GDPR规定了数据管理原则和个人权利，并涵盖处理欧盟公民数据的所有公司。

**护栏**:护栏是指为Adobe Experience Platform中的数据和系统使用、性能优化以及避免错误或意外结果提供指导的阈值。 护栏可以是指您对与授权许可相关的数据和处理的使用情况或使用情况。

## H

**主机**:在标记的上下文中，主机指定系统交付内部版本所需的位置、域和用户凭据。

**每小时**:在计划文件导出的上下文中，每3、6、8或12小时计划一次增量文件导出。

## I

**身份**:标识是唯一表示单个客户的标识符，如Cookie ID、设备ID或电子邮件ID。

**标识字段**:标识字段是XDM字段，用于拼合有关来自多个数据源的各个客户的信息。 必须定义单个主标识，才能启用架构以在实时客户资料中使用。

**身份(“I”)标签**:身份(“I”)数据使用标签用于对可识别或联系特定人员的数据进行分类。

**身份图**:身份图是单个客户的拼合身份与链接身份之间关系的映射。 每个身份图会随客户活动近乎实时地更新。 数据中身份关系的通用结构由 [!UICONTROL 专用图]，用作每个个人身份图的结构蓝图。

**身份命名空间**:标识命名空间定义标识符的上下文，如电子邮件地址或CRM ID。

**Identity Service**: [!DNL Experience Platform Identity Service] 允许创建和管理身份类型，从而跨设备和渠道链接客户身份。 该服务将身份链接在一起的功能允许实时客户资料提供每个单独客户的完整呈现。

**身份拼合**:身份拼合是识别数据片段并将它们拼合在一起以形成完整用户档案记录的过程。

**身份符号**:身份符号是身份命名空间的缩写，可在API中用作引用。

**标识值**:标识值与标识命名空间相结合，是表示唯一个人、组织或资产的标识符。 在配置文件片段中匹配记录数据时，命名空间和标识值必须匹配。

**I1数据使用标签**:的 `I1` 数据使用标签用于对可以直接识别或联系特定人员而非设备的数据进行分类。

**I2数据使用标签**:的 `I2` 数据使用标签用于对可与任何其他数据结合使用的数据进行分类，以间接识别或联系特定人员。

**IMS组织**:IMS组织（有时称为IMS组织）是用于在Adobe产品中标识公司或公司内特定组的名称。 管理员可以配置和管理对组织用户的功能的访问权限和权限。

**摄取**:请参阅数据摄取。

**摄取计划**:摄取计划在从源摄取到Experience Platform时提供基于时间的选项。

**输入功能**:在特征映射中指定输入特征，并由机器学习模型用于进行预测。

**[!DNL Intelligent Services]**: [!DNL Intelligent Services] 例如 [!DNL Attribution AI] 和 [!DNL Customer AI] 是机器学习、基于人工智能的模型，需要Experience Platform(或基于平台构建的应用程序，如Real-time Customer Data Platform)才能运行和运行。

**基于兴趣的定位或个性化**:如果满足以下三个条件，则会进行基于兴趣的定位（也称为个性化）：

1. 网站上收集的数据用于推断用户的兴趣。
1. 数据用在其他上下文中，如在其他网站或应用程序（站外）上。
1. 数据用于根据这些引用选择提供哪些内容或广告。

## J

**[!DNL JupyterLab]**:适用于项目的开源、基于Web的界面 [!DNL Jupyter] 集成到平台UI中。

**[!DNL Jupyter Notebook]**:与JupyterLab集成后，Jupyter Notebooks使您能够以各种语言（如Python、Scala和PySpark）对Experience Platform数据执行数据清理和转换、数值模拟、统计建模、数据可视化、机器学习等操作。

## K

## L

**库**:在标记上下文中，库是一组业务逻辑，其中包含有关标记库应如何在客户端设备上行为的说明。

**查找实体**:在数据建模的上下文中，查询实体表示可与个人相关联，但不能直接用于识别个人的概念。 属于此类别的实体应由基于自定义体验数据模型(XDM)类的架构来表示。

## M

**机器学习(ML)**:机器学习是一个研究领域，它使计算机能够学习而不被明确编程。

**机器学习模型**:机器学习模型是机器学习方法的一个实例，该方法使用历史数据和配置进行培训，以针对业务用例进行解析。 在Adobe Experience Platform数据科学工作区中，机器学习模型称为方法。

**必需属性**:用户启用的复选框，可确保所有配置文件记录都包含所选属性。 例如：所有导出的用户档案都包含电子邮件地址。

**映射**:数据映射是将源数据字段映射到目标中相关目标字段的过程。

**营销操作**:在数据管理框架中，营销操作（也称为营销用例）是Experience Platform数据使用者采取的操作，需要检查其是否违反了数据使用策略。

**合并方法**:使用平台UI定义合并策略时，合并方法会指定在发生冲突时数据片段的优先级。 使用实时客户资料API定义合并策略时，会使用 `attributeMerge` 对象。

**合并策略**:合并策略是Experience Platform用来确定如何合并多个来源的客户数据片段以创建单个配置文件的规则。 当发生数据冲突时，合并策略会确定哪些数据应按优先级排列，以便包含在用户档案中。

**Mixin**:请参阅“架构字段组”。

**模块**:在标记的上下文中，模块是由扩展提供的可执行JavaScript代码片段，该扩展在客户端环境中执行操作而无需创建规则。

## N

**非生产沙盒**:非生产沙箱是通常用于开发实验、测试或试验的沙箱。 与生产沙箱不同，非生产沙箱可以重置和删除。

**[!DNL Notebooks]**: [!DNL Notebooks] 使用创作 [!DNL Jupyter Notebook] 和可运行以执行数据分析。

## O

**选件**:选件是一种营销消息，其中包含面向（潜在）客户的业务或销售建议。 选件通常具有确定谁有资格查看或接收这些选件的特定规则。

**[!DNL Offer Decisioning]**: [!DNL Offer Decisioning] 在根据跨渠道和应用程序收集的数据与最终用户接触时，使营销人员能够管理选件建议的规则和经过培训的模型。

**选件库**:选件库是一个中央库，用于管理个性化和回退选件、决策规则和活动。

**网站个性化营销操作**:使用数据进行网站内容个性化的营销操作。 网站个性化是指用于推论用户兴趣的任何数据，用于根据这些推论选择提供哪些内容或广告。

**现场定位营销操作**:一种营销操作，用于使用数据进行网站广告，包括在您组织的网站或应用程序上选择和投放广告，或衡量此类广告的投放和效果。

**一次**:在计划文件导出的上下文中，安排一次性、按需的完整文件导出。

**覆盖保存策略**:“覆盖”保存策略是用于通过连接摄取第三方数据的选项，您可以在该选项中指定是否将按照指定的计划覆盖摄取的数据。

## P

**部分摄取**:部分摄取允许在指定的错误阈值内摄取批量数据的有效记录。 可以在下载或访问失败记录的错误诊断 [!UICONTROL 监控] 或 [!UICONTROL 源] 数据流运行概述。

**镶木文件**:Parquet文件是具有复杂嵌套数据结构的柱状存储文件格式。 添加数据以填充架构数据集时需要使用Parquet文件。

**个性化优惠**:个性化优惠是基于资格规则和限制的可自定义营销消息。

**植入**：植入是针对最终用户显示优惠的位置和/或上下文。

**策略工作区**:平台UI中的工作区，让数据管理员能够查看和管理贵组织的数据使用标签和策略。

**策略**:数据使用策略是一个规则，用于指定根据应用于Platform数据的使用标签的应用而限制的营销操作。

**策略执行**:允许您通过应用的营销操作强制实施数据使用策略，以防止数据操作在组织内构成违反策略的行为。

**主键**:主键是模式中用于唯一标识所有记录的指定。

**优先级**:在 [!DNL Offer Decisioning]，则优先级用于对满足所有限制（如资格、日历和上限）的选件进行排名。

**专用标识图**:专用身份图（有时称为专用图）是拼合和链接身份之间关系的专用映射，这些拼合和链接身份是根据您的第一方数据构建的，并且仅由您的组织可见。 每个组织只有一个专用图，并充当为与您的品牌进行交互的每个客户生成的单个标识图的结构蓝图。

**产品配置文件**:产品配置文件允许管理员向用户授予对与Experience Platform关联的所有服务或服务子集的访问权限。

**生产沙盒**:生产沙盒是一个用于生产环境的沙盒。 与非生产沙箱不同，生产沙箱无法重置或删除。

**用户档案**:“实时客户资料”作为一项服务，不要与“实时客户资料”混淆，该资料是单个客户的完整表示形式，由合并记录和来自多个来源的时间序列数据构建而成。

**配置文件访问**:的 `/entities` 实时客户配置文件API中的端点允许您访问配置文件数据存储中的记录数据和时序事件。 另请参阅：配置文件实体

**用户档案数据**:配置文件数据是指位于配置文件数据存储区中的任何数据。

**配置文件数据存储**:配置文件数据存储（有时称为配置文件存储）是与数据湖分开的数据存储系统，由实时客户配置文件用于创建和存储配置文件。

**配置文件实体**:用户档案实体表示与个人（通常是客户）相关的属性。 属于此类别的实体应由基于 [!DNL XDM Individual Profile] 类。 另请参阅：配置文件访问

**配置文件导出**: [!DNL Profile] “导出”是Experience Platform中两种目标类型之一。 [!DNL Profile] “导出”会生成包含用户档案和属性的文件，并将原始PII数据与电子邮件结合使用，以便与营销和电子邮件自动化平台集成。

**配置文件片段**:配置文件片段是特定客户的身份列表中仅有一个身份的配置文件信息。

**配置文件ID**:配置文件ID是与标识类型关联的自动生成的标识符，它表示配置文件。

**属性**:在标记上下文中，资产是部署一组标记所需的一切内容的容器。

## Q

**查询**:查询是从数据库表中请求数据。

**查询编辑器**:查询编辑器是用于在中编写、验证和提交SQL语句的工具 [!DNL Query Service].

## R

**Real-time Customer Data Platform**: [!DNL Real-time Customer Data Platform] 通过简化集成、智能细分和跨数字客户历程的实时激活，将已知和未知的客户数据整合在一起，创建可信的客户用户档案。

**实时客户资料**:实时客户资料（有时称为资料）通过合并来自多个渠道（包括在线、离线、CRM和第三方）的数据，提供每个客户的整体视图。 利用用户档案，可将客户数据整合到单个用户档案中，为每次客户互动提供可操作且加盖时间戳的帐户。

**方法**:方法是Adobe对模型规范的术语，是代表特定机器学习流程、AI算法、处理逻辑和配置参数的顶级容器，这些参数是构建和执行经过培训的模型所必需的，因此有助于解决特定业务问题。

**记录**:记录是作为数据集中行保留的数据。

**记录数据**:提供有关主题属性的信息。 主题可以是组织或个人。

**循环**:在 [!DNL Query Service]，循环用于定义查询是计划仅运行一次还是定期运行。

**表示**:在 [!DNL Offer Decisioning]，表示法是渠道用于显示选件的信息，如位置或语言。

**资源**:在标记的上下文中，资源是一个通用术语，它引用了标记用户可在客户端环境中配置的选项，包括扩展、数据元素和规则。

**基于角色的访问控制**:基于角色的访问控制使管理员能够向Experience Platform用户分配访问权限和权限。 权限包括查看和/或使用Experience Platform功能的功能，例如创建沙箱、定义架构和管理数据集。

**规则**:在标记的上下文中，规则是一组组件，用于定义一组应进行逻辑分组的特定事件、条件和操作。

**规则组件**:在标记的上下文中，规则组件是构成规则的事件、条件和操作。

**运行时**:运行时为机器学习方法指定运行时环境。 [!DNL Python], R， [!DNL Spark]、PySpark和Tensorflow运行时允许您为处方源输入指向Docker图像的URL。

## S

**示例数据**:示例数据是数据文件的预览，通常是前100行，它为数据科学家或工程师提供了数据文件中什么模式或数据的概念。

**沙盒**:沙盒是一种虚拟结构，用于将单个Platform实例分区为单独的虚拟环境，以帮助开发和改进数字体验应用程序。

**沙盒重置**:沙盒重置会删除沙盒内的所有数据，包括数据、用户档案和区段。 沙盒重置会影响连接到内部或外部目标的数据。

**沙盒切换器**:Experience Platform中的沙箱切换器控件允许用户在他们有权访问的沙箱之间导航。 切换沙盒将更改所有内容，并可能会根据权限更改功能访问。

**计划**:计划是用户定义的关于从第三方数据源摄取到Adobe Experience Platform的数据的频率或频率的规范。

**评分**:评分是使用经过训练的模型从数据生成洞察的过程。

**架构**:架构是一组规则，用于表示和验证数据的结构和格式。 架构由类和可选字段组组成，用于创建数据集和数据流。 一种架构可以包括行为属性、时间戳、身份、属性定义、关系等。

**架构字段组**:在体验数据模型(XDM)中，架构字段组允许用户扩展可重用字段，以定义要包含在架构中的一个或多个属性。

**架构库**:架构库包含由Adobe提供的行业标准XDM资源，以及由您的组织定义的自定义资源。

**架构注册表**:架构注册表提供了用户界面和RESTful API，用于查看和管理架构库中所有与架构相关的资源。

**密钥访问密钥**:密钥访问密钥是 [!DNL Amazon] 与访问密钥ID一起使用来对AWS请求进行签名的S3密钥。

**区段**:区段是一组规则，其中包含使多个用户档案有资格成为受众的属性和事件数据。

**区段生成器**:的 [!DNL Segment Builder] 是用于生成区段定义的可视化开发环境。 它是所有使用Experience Platform分段服务的应用程序的通用组件。

**区段定义**:区段定义是用于描述目标受众的关键特征或行为的规则集。 概念化后，区段定义中概述的规则将用于确定某个区段的合格受众成员。

**区段评价方法**:分段评估方法有两种：计划和按需。 计划评估允许定期计划在特定时间运行导出作业，而按需评估涉及创建区段作业以立即构建受众。

**区段导出**:区段导出是Experience Platform中两种类型的目标之一。 通过区段导出，您可以发送符合条件且已映射到目标的用户档案。 使用区段和用户ID以及假名数据，并且通常与社交网络和其他数字媒体目标平台集成。

**区段ID**:区段ID是与区段关联的自动生成的标识符。

**区段成员资格**:区段成员资格显示配置文件当前属于哪个区段。

**区段规则**:区段规则定义用于确定用户档案是否符合区段条件的条件。

**分段**:区段划分是将大量客户、潜在客户或消费者划分为具有相似属性且将对特定营销策略做出类似响应的较小群组的过程。

**Sensei ML框架**:Sensei ML框架是一个统一的机器学习(ML)框架，它利用Experience Platform数据，使数据科学家能够以更快、可扩展和可重用的方式开发ML驱动的智能服务。

**敏感(“S”)标签**:敏感(“S”)标签用于对被视为敏感的数据进行分类，例如您希望标记为敏感的不同类型的行为或地理数据。

**服务**:通过利用Adobe智能服务来操作AI和ML服务的强大框架。 服务可提供实时、个性化的客户体验，或操作自定义智能服务。

**单个身份个性化营销操作**:使用数据进行现场内容个性化的营销操作。 Onsite个性化是指用于推论用户兴趣的任何数据，用于根据这些推论选择提供哪些内容或广告。

**S1数据使用标签**:安 `S1` 数据使用标签用于对指定纬度和经度的数据进行分类，这些纬度和经度可用于确定设备的精确位置。

**S2数据使用标签**:安 `S2` 数据使用标签用于对可用于确定广泛定义的地理围栏区域的数据进行分类。

**来源**:源是平台中任何输入连接器的一般术语。 另请参阅：源连接器

**源属性**:源属性是源数据集中的字段。 源属性会映射到目标架构字段。

**源目录**:源目录是Experience Platform中可用的源连接器列表。

**源类别**:源类别是具有相似特征的源的组。

**源连接器**:源连接器（也称为源）可帮助用户轻松从多个源摄取数据，从而允许使用Experience Platform服务来构建、标记和增强数据。 可以从多种源摄取数据，如基于云的存储、第三方软件和CRM系统。

**流连接**:流连接是由Adobe提供的唯一端点，它绑定到客户的IMS组织以将数据流式传输到Experience Platform中。

**标准身份命名空间**:标准身份命名空间是由Adobe提供的预定义身份命名空间，它代表通常用于识别客户的行业标准解决方案。

**流式摄取**:流式摄取允许您将数据从客户端和服务器端设备发送到实时Experience Platform。

**流分段**:流式客户细分是一种持续的数据选择流程，可根据用户活动更新客户细分。 生成并保存区段后，会将区段定义应用于 [!DNL Real-time Customer Profile]. 会定期处理区段添加和移除，以确保您的目标受众仍然相关。

**系统视图**:“系统视图”是流经的源数据集的可视表示形式 [!DNL Real-time Customer Profile] 到目标。

## T

**标记**:在Adobe Experience Platform中，标记提供了用于部署、统一和管理分析、营销和广告集成的工具，这些集成是在所有客户端设备上改善相关客户体验所必需的。

**Target功能**:在特征映射中，目标特征是由模型预测的特征。

**时间序列数据**:时间序列数据在记录主体直接或间接地采取某个动作时提供系统的快照。

**训练模型**:训练模型表示模型训练过程的可执行输出，其中一组训练数据被应用到模型实例。 经过培训的模型将保留对从中创建的任何智能Web服务的引用。 训练好的模型适合于评分和创建智能Web服务。

**令牌**:令牌是一种双重身份验证安全类型，可用于授权使用 [!DNL Query Service].

## U

**并集模式**:并集架构是共享相同类且已启用的架构的合并 [!DNL Real-time Customer Profile]. 组织可以存在多个并集架构，但每个类只能有一个并集架构。

## V

## W

## X

**XDM**:请参阅体验数据模型(XDM)。

**XDM决策事件**:XDM决策事件是一个基于时间序列的类，用于捕获有关决策活动结果和上下文的观察。 这包括关于如何作出决定、何时作出决定、建议（和选择）哪些选项以及在决策过程中影响决策或可以观察到的背景状态的信息。

**XDM ExperienceEvent**:XDM ExperienceEvent是一个基于时间序列的类，用于在发生事件（或事件集）时捕获系统状态，包括所涉及主题的时间点和身份。 另请参阅：体验事件

**XDM个人配置文件**:XDM [!DNL Individual Profile] 是基于记录的类，它对已识别和部分已识别主题的属性形成单一表示。 高度识别的用户档案可用于个人通信或定向活动，并且可以包含详细的个人信息，例如姓名、性别、出生日期、地点和联系信息，包括电话号码和电子邮件地址。

**XDM系统**:XDM系统表示可操作XDM模式以用于下游Experience Platform服务的框架。

## Y

## Z
