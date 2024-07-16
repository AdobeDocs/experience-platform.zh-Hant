---
title: 醫療保健藥物結構欄位群組
description: 瞭解Healthcare藥物方案欄位群組。
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 7%

---

# [!UICONTROL 醫療保健]結構描述欄位群組

[!UICONTROL 醫療保健]是[[!UICONTROL 醫療保健]類別](../../classes/medication.md)的標準結構描述欄位群組。 它提供單一物件型別欄位`medication`，可擷取品牌名稱、批號及數量等詳細資訊。

![](../../images/field-groups/healthcare-medication.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `ingredients` | 物件陣列 | 列出藥物中的成分。 每個物件包含下列屬性： <ul><li>`isActive`： （布林值）指出此藥物中是否仍在使用這個成分。</li><li>`name`： （字串）成份的名稱。</li><li>`quantity`： （字串）藥物中存在的配料數量。</li></ul> |
| `brandName` | 字串 | 藥物的品牌名稱。 |
| `codes` | 字串陣列 | 可識別此藥物的程式碼清單。 |
| `dosageUnitNumber` | 雙精度 | 適用於藥物的劑量單位編號。 |
| `dosageUnitOfMeasurement` | 字串 | 劑量數的測量單位。 |
| `expiryDate` | 日期時間 | 藥物有效期。 |
| `genericName` | 字串 | 藥物的通用名稱。 |
| `lotNumber` | 字串 | 藥物批次的唯一識別碼。 |
| `manufacturerName` | 字串 | 藥品製造商的名稱。 |
| `quantity` | 雙精度 | 包裝中的藥物量。 |
| `status` | 字串 | 表示藥物/藥物是否有效的一般狀態。 |
| `volume` | 雙精度 | 藥物的體積。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱[公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json)。
