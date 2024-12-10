---
title: 目標結構描述欄位群組
description: 瞭解目標結構描述欄位群組。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 87715274-cc9d-41da-9ca7-1634903b4e8f
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 5%

---

# [!UICONTROL 目標]結構描述欄位群組

[!UICONTROL 目標]是[[!DNL XDM Individual Profile] 類別](../../../classes/individual-profile.md)和[[!DNL Provider class]](../../../classes/provider.md)的標準結構描述欄位群組。 它提供單一物件型別欄位`healthcareGoal`，說明患者、群組或組織護理的預定目標。

![欄位群組結構](../../../images/healthcare/field-groups/goal/goal.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 達成狀態] | `achievementStatus` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 說明相對於目標的目標進度，或缺乏進度。 |
| [!UICONTROL 個地址] | `addresses` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 目標所要處理的條件和其他健康情況記錄元素。 |
| [!UICONTROL 類別] | `category` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md)的陣列 | 指出目標所屬的類別，例如飲食或行為。 |
| [!UICONTROL 說明] | `description` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 說明目標的程式碼或文字。 |
| [!UICONTROL 識別碼] | `identifier` | [[!UICONTROL 識別碼]](../data-types/identifier.md)的陣列 | 執行者或其他系統指派給此目標的商業識別碼，在資源更新時保持不變，並會從伺服器傳播到伺服器。 |
| [!UICONTROL 備註] | `note` | [[!UICONTROL 註解]](../data-types/annotation.md)的陣列 | 有關目標的註解。 |
| [!UICONTROL 結果] | `outcome` | [[!UICONTROL 可程式碼參考的陣列]](../data-types/codeable-reference.md) | 在評估目標的狀態時識別變更（或缺少變更）。 |
| [!UICONTROL 優先順序] | `priority` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 識別達成或維持目標相關之相互認可的重要程度。 |
| [!UICONTROL Source] | `source` | [[!UICONTROL 參考]](../data-types/reference.md) | 指示目標的來源，例如病人或從業人員。 |
| [!UICONTROL 開始可程式碼的概念] | `startCodeableConcept` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 之後應說服目標的事件。 |
| [!UICONTROL 主旨 |]`subject` | [[!UICONTROL 參考]](../data-types/reference.md) | 識別正在建立目標的患者、群組或組織。 |
| [!UICONTROL Target] | `target` | 物件陣列 | 表示目標中特定步驟的時間表。 如需詳細資訊，請參閱](#target)下方的[區段。 |
| [!UICONTROL 連續] | `continous` | 布林值 | 表示達成目標後是否需要持續進行活動以維持目標目標。 |
| [!UICONTROL 生命週期狀態] | `lifecycleStatus` | 字串 | 目標生命週期的狀態。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `proposed` </li> <li> `planned` </li> <li> `accepted` </li> <li> `active` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `cancelled` </li> <li> `entered-in-error` </li> <li> `rejected` </li> |
| [!UICONTROL 開始日期] | `startDate` | 日期 | 開始追求目標的日期。 |
| [!UICONTROL 狀態日期] | `statusDate` | 日期 | 識別建立狀態的時間。 |
| [!UICONTROL 狀態原因] | `statusReason` | 字串 | 擷取目前狀態的原因。 |

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)

## `target` {#target}

`target`是以物件陣列的形式提供。 每個物件的結構如下所述。

![目標結構](../../../images/healthcare/field-groups/goal/target.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 詳細可程式碼概念] | `detailCodeableConcept` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 表示達成目標所應達成的目的碼。 |
| [!UICONTROL 詳細數量] | `detailQuantity` | [[!UICONTROL 數量]](../data-types/quantity.md) | 要達到的目標數量，表示已達成目標。 |
| [!UICONTROL 詳細資料範圍] | `detailRange` | [[!UICONTROL Range]](../data-types/range.md) | 要達到的目標範圍，表示已達成目標。 |
| [!UICONTROL 詳細比率] | `detailRatio` | [[!UICONTROL 比例]](../data-types/ratio.md) | 要達到的目標比率，表示已達成目標。 |
| [!UICONTROL 量值] | `measure` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 正在追蹤作為值的引數。 |
| [!UICONTROL 詳細布林值] | `detailBoolean` | 布林值 | 表示目標的達成。 |
| [!UICONTROL 詳細整數] | `detailInteger` | 整數 | 要達到的目標編號，表示已達成目標。 |
| [!UICONTROL 詳細資料字串] | `detailString` | 字串 | 要達到的目標值，表示已達成目標。 |
| [!UICONTROL 到期日期] | `dueDate` | 日期 | 應達成目標的日期。 |
