---
title: 醫療保健藥物方案欄位組
description: 本文檔提供醫療保健藥物方案欄位組的概述。
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 5%

---

# [!UICONTROL 保健藥物] 方案欄位組

[!UICONTROL 保健藥物] 是的標準架構欄位組 [[!UICONTROL 藥物] 類](../../classes/medication.md). 它提供單一物件類型欄位 `medication` 會擷取品牌名稱、批號和數量等詳細資訊。

![](../../images/field-groups/healthcare-medication.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `ingredients` | 物件陣列 | 列出藥物中的成分。 每個物件都包含下列屬性： <ul><li>`isActive`:（布林值）指示此成分是否仍在此藥物中被積極使用。</li><li>`name`:（字串）配料名稱。</li><li>`quantity`:（字串）藥物中的成分的數量。</li></ul> |
| `brandName` | 字串 | 藥品的品牌名稱。 |
| `codes` | 字串陣列 | 一個代碼清單，用於識別這種藥物。 |
| `dosageUnitNumber` | 雙倍 | 用於治療的劑量單位號。 |
| `dosageUnitOfMeasurement` | 字串 | 劑量數的測量單位。 |
| `expiryDate` | DateTime | 藥物的到期日。 |
| `genericName` | 字串 | 藥物的通用名稱。 |
| `lotNumber` | 字串 | 藥物批的唯一標識符。 |
| `manufacturerName` | 字串 | 藥廠的名字。 |
| `quantity` | 雙倍 | 包裝中的藥量。 |
| `status` | 字串 | 指示藥物/藥物是否活動的一般狀態。 |
| `volume` | 雙倍 | 毒品的數量。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
