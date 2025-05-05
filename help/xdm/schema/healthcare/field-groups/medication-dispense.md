---
title: 藥物配發結構描述欄位群組
description: 瞭解Media Dispense結構描述欄位群組。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e897c4e0-23ad-4d79-834f-cfbe2dbec771
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 3%

---

# [!UICONTROL 藥物配發]結構描述欄位群組

[!UICONTROL Media Dispense]是[[!DNL Medication] 類別](../../../classes/medication.md)、[[!DNL XDM Individual Profile] 類別](../../../classes/individual-profile.md)和[[!DNL Provider class]](../../../classes/provider.md)的標準結構描述欄位群組。 它提供單一物件型別欄位`healthcareMedicationDispense`，可擷取即將或已經為具名人員/病人分配的藥物相關資訊。

![欄位群組結構](../../../images/healthcare/field-groups/medication-dispense/medication-dispense.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 授權處方] | `authorizingPrescription` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 允許配方的訂單。 |
| [!UICONTROL 根據] | `basedOn` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 配發藥物所根據的計畫。 |
| [!UICONTROL 類別] | `category` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md)的陣列 | 要配發的藥物類別，如藥物的法律類別或藥物類別。 |
| [!UICONTROL 天供給] | `daysSupply` | [[!UICONTROL 簡單數量]](../data-types/simple-quantity.md) | 藥物供應給患者的天數。 |
| [!UICONTROL 目的地] | `destination` | [[!UICONTROL 參考]](../data-types/reference.md) | 藥物運送至或將要運送至的設施或地點，作為配發事件的一部分。 |
| [!UICONTROL 劑量指示] | `dosageInstruction` | [[!UICONTROL 劑量陣列]](../data-types/dosage.md) | 說明病人要如何使用藥物。 |
| [!UICONTROL 相遇] | `encounter` | [[!UICONTROL 參考]](../data-types/reference.md) | 建立此事件內容的遭遇。 |
| [!UICONTROL 事件歷史記錄] | `eventHistory` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 配發周邊所發生事件的摘要。 |
| [!UICONTROL 識別碼] | `identifier` | [[!UICONTROL 識別碼]](../data-types/identifier.md)的陣列 | 與分配相關聯的識別碼。 識別碼應由業務流程定義，和/或在直接URL參考不合適時用來參考它。 |
| [!UICONTROL 位置] | `location` | [[!UICONTROL 參考]](../data-types/reference.md) | 配發藥物的主要實體位置。 |
| [!UICONTROL 藥物] | `medication` | [[!UICONTROL 可程式碼參考]](../data-types/codeable-reference.md) | 識別所請求的藥物。 這應該是代表藥物詳細資訊的資源的連結，或是識別藥物的程式碼。 |
| [!UICONTROL 未執行原因] | `notPerformedReason` | [[!UICONTROL 可程式碼參考]](../data-types/codeable-reference.md) | 未配發藥物的原因。 |
| [!UICONTROL 備註] | `note` | [[!UICONTROL 註解]](../data-types/annotation.md)的陣列 | 有關分配的額外資訊。 |
| [!UICONTROL 部分，共] | `partOf` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 觸發分配的程式或藥物請求。 |
| [!UICONTROL 執行者] | `performer` | 物件陣列 | 表示執行分配事件的人員或人員。 如需詳細資訊，請參閱[&#128279;](#performer)下方的區段。 |
| [!UICONTROL 數量] | `quantity` | [[!UICONTROL 簡單數量]](../data-types/simple-quantity.md) | 已分配的藥物量，包括測量單位。 |
| [!UICONTROL 接收者] | `receiver` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 識別擷取藥物的人或藥物遞送的位置。 |
| [!UICONTROL 主旨] | `subject` | [[!UICONTROL 參考]](../data-types/reference.md) | 代表接受藥物之人員或群組的資源連結。 |
| [!UICONTROL 替代] | `substitution` | 物件 | 表示是否作為配發的一部分進行替代。 包含四個屬性： <li>`wasSubstituted`：如果分配器要求替代，則布林值為true。</li> <li>`type`： [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md)值，提供表示是否已進行替代的程式碼。</li> <li>`reason`：包含替代原因的[[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md)值的陣列。</li> <li>`responsibleParty`：提供負責替代的人員或當事人的[[!UICONTROL Reference]](../data-types/reference.md)值。 </li> |
| [!UICONTROL 支援資訊] | `supportingInformation` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 支援所配發藥物的其他資訊。 |
| [!UICONTROL 類型] | `type` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 說明所執行的分配事件型別，例如緊急填色或區域性填色。 |
| [!UICONTROL 已錄製] | `recorded` | 日期時間 | 如果未填入`whenPrepared`或`whenHandedOver`，則為分配活動開始的日期和時間。 |
| [!UICONTROL 演算後的劑量指示] | `renderedDosageInstruction` | 字串 | 所有劑量說明中包含的劑量完整表示法。 包含多個劑量指示時使用，以表示複雜劑量，例如增加或遞減劑量。 |
| [!UICONTROL 狀態] | `status` | 字串 | 分配的狀態。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL 狀態已變更] | `statusChanged` | 日期時間 | 配發記錄的狀態變更的日期和時間。 |
| 移交時 | `whenHandedOver` | 日期時間 | 將配發藥物提供給患者的日期和時間。 |
| [!UICONTROL 準備時] | `whenPrepared` | 日期時間 | 配發的藥物被封裝和稽核的日期和時間。 |

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.schema.json)

## `performer` {#performer}

`performer`是以物件陣列的形式提供。 每個物件的結構如下所述。

![執行者結構](../../../images/healthcare/field-groups/medication-dispense/performer.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 執行者] | `actor` | [[!UICONTROL 參考]](../data-types/reference.md) | 執行此動作的從業人員（或類似人員）。 應該假設該執行者是藥物的分配器。 |
| [!UICONTROL 函式] | `function` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 分發中的執行者型別，例如日期輸入者、封裝者或最終檢查者。 |
