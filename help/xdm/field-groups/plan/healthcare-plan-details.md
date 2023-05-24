---
title: 醫療保健計畫詳細資訊架構欄位組
description: 本文檔概述了醫療保健計畫詳細資訊架構欄位組。
exl-id: 5a480c5b-74f8-48dd-858a-5cf2628dc7f0
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 3%

---

# [!UICONTROL 醫療保健計畫詳細資訊] 架構欄位組

[!UICONTROL 醫療保健計畫詳細資訊] 是標準架構欄位組 [[!UICONTROL 計畫] 類](../../classes/plan.md)。 它提供單個對象類型欄位 `healthcarePlanDetails` 捕獲與醫療計畫相關的屬性。

![](../../images/field-groups/plan/healthcare-plan-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `networkDetails` | 對象陣列 | 列出受益人可能尋求治療的保險商定義的提供商網路的詳細資訊，並將按&quot;網路內&quot;費率提供。 每個對象都包括以下屬性： <ul><li>`networkID`:（字串）網路的保險人特定ID。</li><li>`networkName`:（字串）網路的保險人特定名稱。</li></ul> |
| `affiliations` | 字串陣列 | 與計畫相關的業務實體清單。 |
| `coverageType` | 字串 | 計畫覆蓋類型。 接受的值為：<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | 布林值 | 指示計畫是否處於活動狀態。 |
| `lastVerificationDate` | 日期時間 | 上次驗證計畫的日期。 |
| `payerID` | 字串 | 付款人的唯一標識符（即計畫的保險承保人）。 |
| `planLevel` | 字串 | 指示計畫層。 接受的值為：<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | 字串 | 指示計畫類型。 接受的值為：<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | 字串 | 計畫的所有者類型。 示例包括個人、組、組織等。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json)。
