---
title: 醫療保健計畫詳細資訊結構欄位組
description: 本文檔提供醫療保健計畫詳細資訊架構欄位組的概述。
exl-id: 5a480c5b-74f8-48dd-858a-5cf2628dc7f0
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 3%

---

# [!UICONTROL 醫療保健計畫詳細資訊] 方案欄位組

[!UICONTROL 醫療保健計畫詳細資訊] 是的標準架構欄位組 [[!UICONTROL 計畫] 類](../../classes/plan.md). 它提供單一物件類型欄位 `healthcarePlanDetails` 它捕獲與醫療計畫相關的屬性。

![](../../images/field-groups/plan/healthcare-plan-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `networkDetails` | 物件陣列 | 列出受益人可能尋求治療的保險商定義的提供商網路的詳細資訊，並將以「網內」費率涵蓋。 每個物件都包含下列屬性： <ul><li>`networkID`:（字串）網路的保險商專屬ID。</li><li>`networkName`:（字串）網路的保險商專屬名稱。</li></ul> |
| `affiliations` | 字串陣列 | 與計畫關聯的企業實體清單。 |
| `coverageType` | 字串 | 計畫覆蓋類型。 接受的值為：<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | 布林值 | 指示計畫是否處於活動狀態。 |
| `lastVerificationDate` | DateTime | 上次驗證計畫的日期。 |
| `payerID` | 字串 | 付款人的唯一標識符（即計畫的保險提供商）。 |
| `planLevel` | 字串 | 指示計畫層。 接受的值為：<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | 字串 | 指示計畫類型。 接受的值為：<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | 字串 | 計畫的所有者類型。 例如個人、群組、組織等。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json).
