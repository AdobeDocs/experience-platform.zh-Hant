---
title: 排程結構描述欄位群組
description: 瞭解排程結構欄位群組。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: fcabef50-203c-4239-81b4-210aaf5b26ca
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 5%

---

# [!UICONTROL 排程]結構描述欄位群組

[!UICONTROL 排程]是[[!DNL XDM Individual Profile] 類別](../../../classes/individual-profile.md)和[[!DNL Provider class]](../../../classes/provider.md)的標準結構描述欄位群組。 它提供單一物件型別欄位`healthcareSchedule`，這是可用於預約約會的時段容器。

![欄位群組結構](../../../images/healthcare/field-groups/schedule.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 執行者] | `actor` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 參考此排程的槽，可提供這些參考資源的可用性詳細資料。 |
| [!UICONTROL 識別碼] | `identifier` | [[!UICONTROL 識別碼]](../data-types/identifier.md)的陣列 | 排程的外部識別碼。 |
| [!UICONTROL 規劃總時程] | `planningHorizon` | [[!UICONTROL 週期]](../data-types/period.md) | 參考此排程的插槽涵蓋的時間期間（即使不存在任何時段）。 |
| [!UICONTROL 服務類別] | `serviceCategory` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md)的陣列 | 在約會期間要執行之服務的廣泛分類。 |
| [!UICONTROL 服務型別] | `serviceType` | [[!UICONTROL 可程式碼參考的陣列]](../data-types/codeable-reference.md) | 在約會期間要執行的特定服務。 |
| [!UICONTROL 專業] | `specialty` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md)的陣列 | 執行約會中所要求之服務所需的從業人員專業。 |
| [!UICONTROL 作用中] | `active` | 布林值 | 表示排程記錄是否在使用中。 |
| [!UICONTROL 註解] | `comment` | 字串 | 可用性相關註解，旨在說明任何擴充資訊，例如插槽的自訂限制。 |
| [!UICONTROL 名稱] | `name` | 字串 | 搜尋時向消費者呈現之排程的說明。 |

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.schema.json)
