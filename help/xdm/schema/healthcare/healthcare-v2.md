---
title: 醫療保健資料模型V2
description: 瞭解一些常見的醫療保健使用案例和要使用的最佳類別、相關欄位群組和資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a796b58b-b36f-4277-870b-0d3939af8061
source-git-commit: 6d1745b93d2ad7cf6ef96510bd5128a43de9ef03
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 3%

---

# [!UICONTROL 醫療保健]資料模型V2

## 欄位群組和類別 {#field-groups}

下表概述幾種常見醫療保健使用案例的建議類別和結構描述欄位群組。

| 使用實例 | 欄位群組和相容類別 |
| --- | --- |
| **建立/更新病人**：當病人到達醫院服務檯時，會建立病人記錄，包括人口統計細節，例如識別碼（選擇性）、病人姓名、出生日期、性別和地址。 這是醫療保健IT的重要元件。 | <ul><li>**[XDM個別設定檔](../../classes/individual-profile.md)**：<ul><li>[病人](./field-groups/patient.md)</li></ul></li></ul> |
| **疫苗接種**：加速疫苗接種程式、管理病人免疫記錄，以及將EMR與疫苗管理系統整合。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[免疫](./field-groups/immunization.md)</li></ul></li><li>**[XDM個別設定檔](../../classes/individual-profile.md)**：<ul><li>[藥物配發](./field-groups/medication-dispense.md)</li><li>[藥物要求](./field-groups/medication-request.md)</li><li>[病人](./field-groups/patient.md)</li></ul></li><li>**[位置](./classes/location.md)**：<ul><li>[位置](./field-groups/location.md)</li></ul><li>**[藥物](../../classes/medication.md)**：<ul><li>[藥物](./field-groups/medication.md)</li><li>[藥物配發](./field-groups/medication-dispense.md)</li><li>[藥物要求](./field-groups/medication-request.md)</li></ul></li><li>**[提供者](../../classes/provider.md)**：<ul><li>[藥物配發](./field-groups/medication-dispense.md)</li><li>[藥物要求](./field-groups/medication-request.md)</li></ul></li></ul> |
| **照護後守約**：激勵病人和照護者完成他們的治療計畫，並降低匯款率。 | <ul><li>**[XDM個別設定檔](../../classes/individual-profile.md)**：<ul><li>[服務計畫](./field-groups/care-plan.md)</li><li>[目標](./field-groups/goal.md)</li><li>[病人](./field-groups/patient.md)</li></ul></li><li>**[位置](./classes/location.md)**：<ul><li>[位置](./field-groups/location.md)</li></ul><li>**[提供者](../../classes/provider.md)**：<ul><li>[目標](./field-groups/goal.md)</li></ul></li></ul> |
| **保險的消費者體驗**：改善購買保險的消費者的數位贏取和體驗。 例如： <li> 了解消費者行為，向存取包含一般資訊（例如計畫、計畫名稱/層級、Medicaid或健康計畫）之頁面的使用者傳送促銷電子郵件或目標第三方廣告</li><li> 傳送心臟健康的疫苗相關資訊，以建立品牌獎勵或請求排程疫苗給搜尋心臟健康和疫苗資訊的人。 </li> | <ul><li>**[XDM個別設定檔](../../classes/individual-profile.md)**：<ul><li>[帳戶](./field-groups/account.md)</li><li>[藥物配發](./field-groups/medication-dispense.md)</li><li>[藥物要求](./field-groups/medication-request.md)</li><li>[病人](./field-groups/patient.md)</li></ul></li><li>**[位置](./classes/location.md)**：<ul><li>[位置](./field-groups/location.md)</li></ul><li>**[藥物](../../classes/medication.md)**：<ul><li>[藥物](./field-groups/medication.md)</li><li>[藥物配發](./field-groups/medication-dispense.md)</li><li>[藥物要求](./field-groups/medication-request.md)</li></ul></li><li>**[提供者](../../classes/provider.md)**：<ul><li>[帳戶](./field-groups/account.md)</li><li>[藥物配發](./field-groups/medication-dispense.md)</li><li>[藥物要求](./field-groups/medication-request.md)</li></ul><li>**[計畫](../../classes/plan.md)**：<ul><li>[目標](./field-groups/coverage.md)</li></ul></li></ul> |
| **增強型提供者經驗**：使用EMR系統的提供者資料，根據預約可用性、地點和專業來建議替代提供者。<br> <br>改善提供者搜尋，以顯示具有所需可用性的結果，驗證選取的提供者是否為付款者網路的一部分，並提供成本預估。 | <ul><li>**[XDM個別設定檔](../../classes/individual-profile.md)**：<ul><li>[約會](./field-groups/appointment.md)</li><li>[組織](./field-groups/organization.md)</li><li>[病人](./field-groups/patient.md)</li><li>[從業者](./field-groups/practioner.md)</li><li>[排程](./field-groups/schedule.md)</li></ul></li><li>**[位置](./classes/location.md)**：<ul><li>[位置](./field-groups/location.md)</li></ul><li>**[提供者](../../classes/provider.md)**：<ul><li>[約會](./field-groups/appointment.md)</li><li>[組織](./field-groups/organization.md)</li><li>[從業者](./field-groups/practioner.md)</li><li>[排程](./field-groups/schedule.md)</li></ul></li></ul> |

{style="table-layout:fixed"}

## 資料類型 {#data-types}

下表概述根據[!DNL HL7 FHIR Release 5]規格建立的資料型別。

| 名稱 | 說明 |
| --- | --- |
| [[!UICONTROL 位址]](./data-types/address.md) | 說明使用郵遞區號慣例（而非GPS或其他位置定義格式）表示的地址。 |
| [[!UICONTROL 註解]](./data-types/annotation.md) | 歸因於作者的文位元組點。 |
| [[!UICONTROL 可用性]](./data-types/availability.md) | 專案的可用性資料。 |
| [[!UICONTROL 可程式碼概念]](./data-types/codeable-concept.md) | 從一種資源到另一種資源的參考。 |
| [[!UICONTROL 可程式碼參考]](./data-types/codeable-reference.md) | 對資源或概念的參照。 |
| [[!UICONTROL 編碼]](./data-types/coding.md) | 術語系統定義的程式碼參考。 |
| [[!UICONTROL 聯絡視窗]](./data-types/contact-point.md) | 個人的聯絡詳細資訊。 |
| [[!UICONTROL 劑量]](./data-types/dosage.md) | 用藥方式或應如何服用。 |
| [[!UICONTROL 持續時間]](./data-types/duration.md) | 時間長度。 |
| [[!UICONTROL 延伸連絡人詳細資料]](./data-types/extended-contact-detail.md) | 延伸連絡人的資訊。 |
| [[!UICONTROL 人名]](./data-types/human-name.md) | 有關人類或其他生命實體名稱的資訊。 |
| [[!UICONTROL 識別碼]](./data-types/identifier.md) | 用於計算的識別碼。 |
| [[!UICONTROL 金額]](./data-types/money.md) | 以某些公認的貨幣表示的經濟公用程式金額。 |
| [[!UICONTROL 週期]](./data-types/period.md) | 由開始和結束日期/時間定義的時間期間。 |
| [[!UICONTROL 人員]](./data-types/person.md) | 有關一般人員記錄的資訊。 |
| [[!UICONTROL 數量]](./data-types/quantity.md) | 測量或可測量的金額。 |
| [[!UICONTROL Range]](./data-types/range.md) | 由低值和高值繫結的一組值。 |
| [[!UICONTROL 比例]](./data-types/ratio.md) | 透過分子和分母的兩個[[!UICONTROL 數量]](./data-types/quantity.md)值的比例。 |
| [[!UICONTROL 參考]](./data-types/reference.md) | 從一種資源到另一種資源的參考。 |
| [[!UICONTROL 重複]](./data-types/repeat.md) | 說明事件排程時間的一組規則。 |
| [[!UICONTROL 簡單數量]](./data-types/simple-quantity.md) | 測量或可測量的金額。 |
| [[!UICONTROL 計時]](./data-types/timing.md) | 關於可能發生多次之事件的資訊。 |
| [[!UICONTROL 虛擬服務詳細資料]](./data-types/virtual-service-detail.md) | 虛擬服務連絡人詳細資料。 |

