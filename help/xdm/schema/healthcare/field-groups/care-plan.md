---
title: 服務計畫結構描述欄位群組
description: 瞭解關於服務計畫結構描述欄位群組。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e6cbf44f-6c39-42bd-b083-a975860a64db
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 4%

---

# [!UICONTROL 服務計畫]結構描述欄位群組

[!UICONTROL 服務計畫]是[[!DNL XDM Individual Profile] 類別](../../../classes/individual-profile.md)的標準結構描述欄位群組。 它提供單一物件型別欄位`healthcareCarePlan`，擷取病人或群組的醫療保健計畫。

![欄位群組結構](../../../images/healthcare/field-groups/care-plan/care-plan.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 活動] | `activity` | 物件陣列 | 識別已發生或計畫作為計畫的一部分發生的動作。 如需詳細資訊，請參閱](#activity)下方的[區段。 |
| [!UICONTROL 個地址] | `addresses` | [[!UICONTROL 可程式碼參考的陣列]](../data-types/codeable-reference.md) | 識別照護計畫處理的條件或疑慮。 |
| [!UICONTROL 根據] | `basedOn` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 由此照護計畫全部或部分履行的較高層級要求資源。 |
| [!UICONTROL 服務團隊] | `careTeam` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 識別預期將參與此計畫所設想的照護的所有人員和組織。 |
| [!UICONTROL 類別] | `category` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md)的陣列 | 識別此計畫是哪一種計畫，以支援多重共存計畫之間的差異。 |
| [!UICONTROL 參與者] | `contributor` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 識別提供護理計畫內容的個人、組織或裝置。 |
| [!UICONTROL 保管人] | `custodian` | [[!UICONTROL 參考]](../data-types/reference.md) | 一旦填入，託管人即須負責並歸屬於該照護計畫。 |
| [!UICONTROL 相遇] | `encounter` | [[!UICONTROL 參考]](../data-types/reference.md) | 建立照護計畫的遭遇。 |
| [!UICONTROL 目標] | `goal` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 執行計畫的預定目標。 |
| [!UICONTROL 識別碼] | `identifier` | [[!UICONTROL 識別碼]](../data-types/identifier.md)的陣列 | 執行者或其他系統指派給此照護計畫的企業識別碼會隨著資源的更新及從伺服器傳播而保持恆定。 |
| [!UICONTROL 備註] | `note` | [[!UICONTROL 註解]](../data-types/annotation.md)的陣列 | 有關其他屬性未涵蓋的護理計畫的一般附註。 |
| [!UICONTROL 部分，共] | `partOf` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 此特定照護計畫為元件或步驟的大型照護計畫。 |
| [!UICONTROL 週期] | `period` | [[!UICONTROL 週期]](../data-types/period.md) | 表示計畫已經（或意圖）生效及結束的時間。 |
| [!UICONTROL 取代] | `replaces` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 已完成或已終止的照護計畫，其功能已由此照護計畫接管。 |
| [!UICONTROL 主旨] | `subject` | [[!UICONTROL 參考]](../data-types/reference.md) | 識別計畫描述其預期護理的病人或群組。 |
| [!UICONTROL 支援資訊] | `supportingInfo` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 識別影響計畫形成的患者記錄部分。 這些可能包括共病、最近的程式、限制或最近的評估。 |
| [!UICONTROL 已建立] | `created` | 日期時間 | 代表此照護計畫在系統中建立的時間，這通常是系統產生的日期。 |
| [!UICONTROL 說明] | `description` | 字串 | 計畫範圍與性質的說明。 |
| [!UICONTROL 具現化Canonical] | `instantiatesCanonical` | 字串陣列 | 此URL指向FHIR定義的通訊協定、指引、問卷或此計畫完全或部分遵守的其他定義。 |
| [!UICONTROL 具現化URI] | `instantiatesUri` | 字串陣列 | 指向外部維護的通訊協定、指引、問卷或此計畫完全或部分遵守的其他定義的URL，表示為URI。 |
| [!UICONTROL 意圖] | `intent` | 字串 | 照護計畫的目的。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `option` </li> <li> `directive` </li> |
| [!UICONTROL 狀態] | `status` | 字串 | 照護計畫的狀態。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `draft` </li> <li> `active` </li> <li> `on-hold` </li> <li> `revoked` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `unknown` </li> |
| [!UICONTROL 標題] | `title` | 字串 | 服務計畫的名稱。 |

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.schema.json)

## `activity` {#activity}

`activity`是以物件陣列的形式提供。 每個物件的結構如下所述。

![活動結構](../../../images/healthcare/field-groups/care-plan/activity.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 已執行的活動] | `performedActivity` | [[!UICONTROL 可程式碼參考的陣列]](../data-types/codeable-reference.md) | 活動的結果，例如約會或程式。 |
| [!UICONTROL 計畫活動參考] | `plannedActivityReference` | [[!UICONTROL 參考]](../data-types/reference.md) | 建議活動的詳細資訊。 |
| [!UICONTROL 進度] | `progress` | [[!UICONTROL 註解]](../data-types/annotation.md)的陣列 | 有關活動的遵守、狀態或進度的附註。 |
