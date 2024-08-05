---
keywords: Experience Platform；零售配方；資料科學Workspace；熱門主題；配方
solution: Experience Platform
title: 建立零售銷售結構描述和資料集
type: Tutorial
description: 本教學課程提供所有其他Adobe Experience Platform資料科學Workspace教學課程所需的先決條件和資產。 完成後，您和貴組織成員將可透過Experience Platform使用零售銷售結構和資料集。
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 2%

---


# 建立零售銷售綱要及資料集

>[!NOTE]
>
>不再提供 Data Science 工作環境 購買。
>
>本文檔適用於先前有權使用數據科學工作環境的現有客戶。

此教學課程提供所有其他[!DNL Adobe Experience Platform][!DNL Data Science Workspace]教程所需的先決条件和資產。完成後，[!DNL Experience Platform]上的零售銷售結構描述和資料集將可供您和組織成員使用。

## 快速入門

開始進行本教學課程前，您必須具備下列必要條件：
- 存取 [!DNL Adobe Experience Platform]。 如果您無權存取 中的 [!DNL Experience Platform]組織，請在繼續操作前與系統管理員聯繫。
- 進行 [!DNL Experience Platform] API 呼叫的授權。 [完整應用程式身份驗證和訪問 Adobe Experience Platform API](https://www.adobe.com/go/platform-api-authentication-en) 教學課程以獲取以下值，以便成功完成此教學課程：
   - 授權： `{ACCESS_TOKEN}`
   - x-api-key： `{API_KEY}`
   - x-gw-ims-org-id： `{ORG_ID}`
   - 使用者端密碼： `{CLIENT_SECRET}`
   - 使用者端憑證： `{PRIVATE_KEY}`
- [零售銷售方式](../pre-built-recipes/retail-sales.md)的範例資料和來源檔案。 從[Adobe公用Git存放庫](https://github.com/adobe/experience-platform-dsw-reference/)下載此教學課程和其他[!DNL Data Science Workspace]教學課程所需的資產。
- [Python >= 2.7](https://www.python.org/downloads/)和下列[!DNL Python]個套件：
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [聽寫器](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- 實際瞭解本教學課程中所使用的下列概念：
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [結構描述構成的基礎知識](../../xdm/schema/field-dictionary.md)

## 建立零售銷售綱要和資料集

使用提供的啟動程式指令碼，會自動建立零售銷售結構描述和資料集。 請依序遵循下列步驟：

### 設定檔案

1. 在[!DNL Experience Platform]教學課程資源套件中，導覽至目錄`bootstrap`，並使用適當的文字編輯器開啟`config.yaml`。
2. 在該 `Enterprise` 部分下，輸入以下值：

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. 編輯在“示例”部分下 `Platform` 找到的值，如下所示：

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`： API 呼叫的基本路徑。 請勿修改此值。
   - `ims_token`：你的 `{ACCESS_TOKEN}` 去這裡。
   - `ingest_data`：出於此教學課程的目的，請將此值設置為 為了 `"True"` 創建零售銷售架構和數據集。 `"False"`的值只會建立結構描述。
   - `build_recipe_artifacts`：在本教學課程中，請將此值設為`"False"`以防止指令碼產生配方成品。
   - `kernel_type`：配方成品的執行型別。 如果`build_recipe_artifacts`設為`"False"`，則此值保持為`Python`，否則請指定正確的執行型別。

4. 在`Titles`區段下，為零售範例資料適當地提供下列資訊，並在編輯完成後儲存並關閉檔案。 範例如下：

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

### 執行啟動程式指令碼

1. 打開終端應用程式並導航到 [!DNL Experience Platform] 教學課程 資源目錄。
2. 將`bootstrap`目錄設定為當前工作路徑，並通過`bootstrap.py`[!DNL Python]輸入以下命令運行文稿：

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >完成腳本可能需要幾分鐘時間。

## 後續步驟

成功完成引導文本后，可以在 上 [!DNL Experience Platform]查看零售銷售輸入和輸出架構和數據集。 請参閱 [「預覽 綱要数据」教學課程](./preview-schema-data.md)
以取得更多資訊。

您還使用提供的引導文本成功引入零售銷售示例數據 [!DNL Experience Platform] 。

要繼續使用引入的數據，請執行以下操作：
- [使用 Jupyter Notebooks 分析您的資料](../jupyterlab/analyze-your-data.md)
   - 在數據科學工作環境中使用 Jupyter 筆記本來訪問、流覽、可視化和理解數據。
- [將源檔打包到配方中](./package-source-files-recipe.md)
   - 按照本教學課程瞭解如何將您自己的模型封裝在可匯入的「配方」檔案中，並帶入[!DNL Data Science Workspace]。
