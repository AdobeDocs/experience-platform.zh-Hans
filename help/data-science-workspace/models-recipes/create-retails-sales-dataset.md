---
keywords: Experience Platform；零售销售菜谱；数据科学工作区；热门主题；菜谱
solution: Experience Platform
title: 创建零售销售模式和数据集
topic-legacy: tutorial
type: Tutorial
description: 本教程为您提供了所有其他Adobe Experience Platform数据科学工作区教程所需的先决条件和资源。 完成后，您和您的IMS组织成员将可以使用零售销售模式和数据集进行Experience Platform。
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# 创建零售销售模式和数据集

本教程为您提供了所有其他[!DNL Adobe Experience Platform] [!DNL Data Science Workspace]教程所需的入门项目和资源。 完成后，您和[!DNL Experience Platform]上IMS组织的成员将可以使用零售销售模式和数据集。

## 入门指南

在开始本教程之前，您必须具备以下先决条件：
- 访问[!DNL Adobe Experience Platform]。 如果您无权访问[!DNL Experience Platform]中的IMS组织，请在继续操作之前与您的系统管理员联系。
- 进行[!DNL Experience Platform] API调用的授权。 请完成[验证和访问Adobe Experience Platform API](https://www.adobe.com/go/platform-api-authentication-en)教程，以获得以下值，以成功完成本教程：
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key:`{API_KEY}`
   - x-gw-ims-org-id:`{IMS_ORG}`
   - 客户机密：`{CLIENT_SECRET}`
   - 客户端证书：`{PRIVATE_KEY}`
- [零售销售方法](../pre-built-recipes/retail-sales.md)的示例数据和源文件。 从[Adobe公共Git存储库](https://github.com/adobe/experience-platform-dsw-reference/)下载此教程和其他[!DNL Data Science Workspace]教程所需的资源。
- [Python >= 2.7](https://www.python.org/downloads/) 和以下 [!DNL Python] 包：
   - [pi](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- 了解本教程中使用的以下概念：
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [模式合成基础](../../xdm/schema/field-dictionary.md)

## 创建零售销售模式和数据集

零售销售模式和数据集是使用提供的引导脚本自动创建的。 请按照以下步骤操作：

### 配置文件

1. 在[!DNL Experience Platform]教程资源包中，导航到目录`bootstrap`，然后使用相应的文本编辑器打开`config.yaml`。
2. 在`Enterprise`部分下，输入以下值：

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. 编辑`Platform`部分下的值，示例如下：

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` :API调用的基本路径。请勿修改此值。
   - `ims_token` :你 `{ACCESS_TOKEN}` 来这。
   - `ingest_data` :在本教程中，请将此值设置为， `"True"` 以创建零售销售模式和数据集。值`"False"`将仅创建模式。
   - `build_recipe_artifacts` :为在本教程中起作用，将此值设置为 `"False"` 防止脚本生成Recipe项目。
   - `kernel_type` :Recipe对象的执行类型。如果将`build_recipe_artifacts`设置为`"False"`，则将此值保留为`Python`，否则请指定正确的执行类型。

4. 在`Titles`部分下，为零售销售示例数据提供相应的以下信息，在编辑到位后保存并关闭文件。 示例如下：

   ```yaml
   Titles:
       input_class_title: retail_sales_input_class
       input_mixin_title: retail_sales_input_mixin
       input_mixin_definition_title: retail_sales_input_mixin_definition
       input_schema_title: retail_sales_input_schema
       input_dataset_title: retail_sales_input_dataset
       file_replace_tenant_id: DSWRetailSalesForXDM0.9.9.9.json
       file_with_tenant_id: DSWRetailSales_with_tenant_id.json
       is_output_schema_different: "True"
       output_mixin_title: retail_sales_output_mixin
       output_mixin_definition_title: retail_sales_output_mixin_definition
       output_schema_title: retail_sales_output_title
       output_dataset_title: retail_sales_output_dataset
   ```

### 运行引导脚本

1. 打开您的终端应用程序并导航到[!DNL Experience Platform]教程资源目录。
2. 将`bootstrap`目录设置为当前工作路径，并输入以下命令运行`bootstrap.py` [!DNL Python]脚本：

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >完成脚本可能需要几分钟。

## 后续步骤

成功完成引导脚本后，可在[!DNL Experience Platform]上查看零售销售输入和输出模式及数据集。 请参阅[预览模式数据教程](./preview-schema-data.md)
。

您还使用提供的引导脚本成功将零售销售示例数据引入[!DNL Experience Platform]。

要继续使用摄取的数据，请执行以下操作：
- [使用Jupyter笔记本分析数据](../jupyterlab/analyze-your-data.md)
   - 使用数据科学工作区中的Jupyter Notebooks访问、探索、可视化和了解您的数据。
- [将源文件打包到菜谱中](./package-source-files-recipe.md)
   - 请按照本教程学习如何通过将源文件打包到可导入的处方文件中，将您自己的模型引入[!DNL Data Science Workspace]中。
