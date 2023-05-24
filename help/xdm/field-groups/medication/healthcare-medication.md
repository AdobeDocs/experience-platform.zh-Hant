---
title: 醫療保健藥物方案欄位組
description: 本文檔概述了醫療保健藥物方案欄位組。
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 5%

---

# [!UICONTROL 一種保健藥物] 架構欄位組

[!UICONTROL 一種保健藥物] 是標準架構欄位組 [[!UICONTROL 藥物] 類](../../classes/medication.md)。 它提供單個對象類型欄位 `medication` 它捕獲品牌名稱、批號和數量等詳細資訊。

![](../../images/field-groups/healthcare-medication.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `ingredients` | 對象陣列 | 列出藥物中的成分。 每個對象都包括以下屬性： <ul><li>`isActive`:（布爾值）指示此配料是否仍在此藥物中使用。</li><li>`name`:（字串）配料的名稱。</li><li>`quantity`:（字串）藥物中的成分數量。</li></ul> |
| `brandName` | 字串 | 藥品的品牌。 |
| `codes` | 字串陣列 | 識別這種藥物的密碼清單。 |
| `dosageUnitNumber` | 雙倍 | 藥物的劑量單位號。 |
| `dosageUnitOfMeasurement` | 字串 | 劑量號的測量單位。 |
| `expiryDate` | 日期時間 | 藥物的到期日。 |
| `genericName` | 字串 | 藥物的通用名稱。 |
| `lotNumber` | 字串 | 藥物批的唯一標識符。 |
| `manufacturerName` | 字串 | 藥廠的名字。 |
| `quantity` | 雙倍 | 包裝中的藥量。 |
| `status` | 字串 | 指示藥物/藥物是否有效的一般狀態。 |
| `volume` | 雙倍 | 藥量。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json)。
