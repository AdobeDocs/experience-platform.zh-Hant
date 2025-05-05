---
title: 藥物結構描述欄位群組
description: 瞭解藥物結構描述欄位群組。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e1f53ff8-3079-4b2f-9e73-31a773907a63
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 6%

---

# [!UICONTROL 藥物]結構描述欄位群組

[!UICONTROL 藥物]是[[!DNL Medication] 類別](../../../classes/medication.md)的標準結構描述欄位群組。 它提供擷取藥物資訊的單一物件型別欄位`healthcareMedication`。

![欄位群組結構](../../../images/healthcare/field-groups/medication/medication.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| ---|  --- | --- | --- |
| [!UICONTROL 批次] | `batch` | 物件 | 封裝藥物的詳細資訊。 包含兩個屬性： <li>`lotNumber`：指派給批次的識別碼字串值。</li> <li>`expirationDate`：批次到期時的DateTime值。</li> |
| [!UICONTROL 代碼] | `code` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 識別此藥物的程式碼。 |
| [!UICONTROL 定義] | `definition` | [[!UICONTROL 參考]](../data-types/reference.md) | 藥物定義。 |
| [!UICONTROL 劑量表單] | `doseForm` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 說明藥物的劑型，如片劑或膠囊。 |
| [!UICONTROL 識別碼] | `identifier` | [[!UICONTROL 識別碼]](../data-types/identifier.md)的陣列 | 適用於藥物的識別碼。 |
| [!UICONTROL 成分] | `ingredient` | 物件陣列 | 描述藥物的成分資訊。 如需詳細資訊，請參閱[&#128279;](#ingredient)下方的區段。 |
| [!UICONTROL 行銷授權持有者] | `marketingAuthorizationHolder` | [[!UICONTROL 參考]](../data-types/reference.md) | 擁有授權以行銷藥物的組織。 |
| [!UICONTROL 總磁碟區] | `totalVolume` | [[!UICONTROL 數量]](../data-types/quantity.md) | 當產品代碼未推斷封裝大小時，藥物中提供的產品金額。 |
| [!UICONTROL 狀態] | `status` | 字串 | 藥物狀態。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `active` </li> <li> `inactive` </li> <li> `entered-in-error` </li> |

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medication.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medication.schema.json)

## `ingredient` {#ingredient}

`ingredient`是以物件陣列的形式提供。 每個物件的結構如下所述。

![成分結構](../../../images/healthcare/field-groups/medication/ingredient.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 專案] | `item` | [[!UICONTROL 可程式碼參考]](../data-types/codeable-reference.md) | 描述的成分。 |
| [!UICONTROL 強度可程式碼概念] | `strengthCodeableConcept` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 以系統定義的術語表示的成分數量。 |
| [!UICONTROL 強度數量] | `strengthQuantity` | [[!UICONTROL 數量]](../data-types/quantity.md) | 存在的配料數量。 |
| [!UICONTROL 強度比例] | `strengthRatio` | [[!UICONTROL 比例]](../data-types/ratio.md) | 成分存在的比率。 |
| [!UICONTROL 為作用中] | `isActive` | 布林值 | 表示成分是否有效。 |
