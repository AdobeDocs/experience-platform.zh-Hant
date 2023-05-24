---
keywords: Experience Platform；零售處方；資料科學工作區；熱門主題；配方
solution: Experience Platform
title: 建立零售銷售架構和資料集
type: Tutorial
description: 本教程為您提供了所有其他Adobe Experience Platform資料科學工作區教程所需的先決條件和資產。 完成後，您和您的組織成員將可以使用Retail Sales架構和資料集進行Experience Platform。
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---


# 建立零售銷售架構和資料集

本教程為您提供所有其他元件所需的必備元件和資產 [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] 教程。 完成後，您和您組織的成員將可以使用零售銷售架構和資料集 [!DNL Experience Platform]。

## 快速入門

在啟動本教程之前，您必須具備以下先決條件：
- 訪問 [!DNL Adobe Experience Platform]。 如果您沒有訪問 [!DNL Experience Platform]，請在繼續之前與系統管理員聯繫。
- 授權 [!DNL Experience Platform] API調用。 完成 [驗證和訪問Adobe Experience PlatformAPI](https://www.adobe.com/go/platform-api-authentication-en) 教程：獲取以下值以成功完成本教程：
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - 客戶端密碼： `{CLIENT_SECRET}`
   - 客戶端證書： `{PRIVATE_KEY}`
- 示例資料和源檔案 [零售銷售處方](../pre-built-recipes/retail-sales.md)。 下載此和其他項所需的資產 [!DNL Data Science Workspace] 教程 [Adobe公共Git儲存庫](https://github.com/adobe/experience-platform-dsw-reference/)。
- [Python >= 2.7](https://www.python.org/downloads/) 以下 [!DNL Python] 包：
   - [畫](https://pypi.org/project/pip/)
   - [皮亞姆](https://pyyaml.org/)
   - [聽診器](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- 對本教程中使用的以下概念的有效理解：
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [架構組合的基礎](../../xdm/schema/field-dictionary.md)

## 建立零售銷售架構和資料集

Retail Sales架構和資料集是使用提供的引導指令碼自動建立的。 按順序執行以下步驟：

### 配置檔案

1. 在 [!DNL Experience Platform] 教程資源包，導航到目錄 `bootstrap`，開啟 `config.yaml` 使用適當的文本編輯器。
2. 在 `Enterprise` ，輸入以下值：

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. 編輯在 `Platform` 部分，示例如下：

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`:API調用的基路徑。 不要修改此值。
   - `ims_token`:您 `{ACCESS_TOKEN}` 到這裡。
   - `ingest_data`:在本教程中，將此值設定為 `"True"` 以建立Retail Sales架構和資料集。 值 `"False"` 將僅建立架構。
   - `build_recipe_artifacts`:在本教程中，將此值設定為 `"False"` 來防止指令碼生成處方對象。
   - `kernel_type`:處方對象的執行類型。 將此值保留為 `Python` 如果 `build_recipe_artifacts` 設定為 `"False"`，否則指定正確的執行類型。

4. 在 `Titles` 部分，為零售銷售示例資料提供相應的以下資訊，在編輯到位後保存並關閉檔案。 下面所示的示例：

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

### 運行引導指令碼

1. 開啟您的終端應用程式並導航到 [!DNL Experience Platform] 教程資源目錄。
2. 設定 `bootstrap` 目錄作為當前工作路徑並運行 `bootstrap.py` [!DNL Python] 指令碼：

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >指令碼可能需要幾分鐘才能完成。

## 後續步驟

成功完成引導指令碼後，可以在上查看零售銷售的輸入和輸出架構以及資料集 [!DNL Experience Platform]。 查看 [預覽架構資料教程](./preview-schema-data.md)
的子菜單。

您還成功地將零售銷售示例資料 [!DNL Experience Platform] 使用提供的引導指令碼。

要繼續處理所攝取的資料：
- [使用Jupyter筆記本分析資料](../jupyterlab/analyze-your-data.md)
   - 使用Data Science Workspace中的Jupyter筆記本訪問、瀏覽、可視化和瞭解資料。
- [將源檔案打包到配方](./package-source-files-recipe.md)
   - 按照本教程學習如何將您自己的模型引入 [!DNL Data Science Workspace] 將源檔案打包到可導入的配方檔案中。
