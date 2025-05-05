---
title: 藥物請求結構描述欄位群組
description: 瞭解藥物請求結構描述欄位群組。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8502380f-9557-4ca6-84bc-65010dfc6066
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 3%

---

# [!UICONTROL 藥物要求]結構描述欄位群組

[!UICONTROL 藥物要求]是[[!DNL Medication] 類別](../../../classes/medication.md)、[[!DNL XDM Individual Profile] 類別](../../../classes/individual-profile.md)和[[!DNL Provider class]](../../../classes/provider.md)的標準結構描述欄位群組。 它提供單一物件型別欄位`healthcareMedicationDispense`，可擷取提供藥物和向病人管理藥物指示的訂單或請求。

![欄位群組結構](../../../images/healthcare/field-groups/medication-request/medication-request.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 根據] | `basedOn` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 此藥物要求所履行的計畫或要求。 |
| [!UICONTROL 類別] | `category` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md)的陣列 | 藥物請求的分類或群組。 |
| [!UICONTROL 治療課程型別] | `courseOfTherapyType` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 對病人用藥管理的整體模式說明。 |
| [!UICONTROL 裝置] | `device` | [[!UICONTROL 可程式碼參考的陣列]](../data-types/codeable-reference.md) | 用於藥物管理的裝置型別。 |
| [!UICONTROL 分配要求] | `dispenseRequest` | 物件 | 表示分配要求的特定細節，通常稱為藥物訂單。 如需詳細資訊，請參閱[&#128279;](#dispense-request)下方的區段。 |
| [!UICONTROL 劑量指示] | `dosageInstructions` | [[!UICONTROL 劑量陣列]](../data-types/dosage.md) | 病人要如何使用藥物的具體指示。 |
| [!UICONTROL 有效劑量期間] | `effectiveDosePeriod` | [[!UICONTROL 週期]](../data-types/period.md) | 接受藥物的時間。 有多個`dosageInstruction`行的地方（例如，當逐漸減少劑量時），這是劑量指示的最早日期和最晚日期。 |
| [!UICONTROL 相遇] | `encounter` | [[!UICONTROL 參考]](../data-types/reference.md) | 建立請求時的遭遇。 |
| [!UICONTROL 事件歷史記錄] | `eventHistory` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 與藥物請求相關的事件記錄連結，例如完成請求、關鍵狀態轉變時間或相關更新。 |
| [!UICONTROL 群組識別碼] | `groupIdentifier` | [[!UICONTROL 識別碼]](../data-types/identifier.md) | 由單一作者啟動的多個獨立請求執行個體的共用識別碼。 |
| [!UICONTROL 識別碼] | `identifier` | [[!UICONTROL 識別碼]](../data-types/identifier.md)的陣列 | 與藥物請求關聯的識別碼，由業務流程定義，和/或用來在直接URL參考資源本身不合適時參考它。 |
| [!UICONTROL 資訊Source] | `informationSource` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 如果來源不是`requester`，則為請求提供資訊的人員或組織。 |
| [!UICONTROL 保險] | `insurance` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 提供要求的服務所需的保險計畫、承保範圍延伸、預先授權及/或預先決定。 |
| [!UICONTROL 藥物] | `medication` | [[!UICONTROL 可程式碼參考]](../data-types/codeable-reference.md) | 識別所請求的藥物。 這應該是代表藥物詳細資訊的資源的連結，或是識別藥物的程式碼。 |
| [!UICONTROL 備註] | `note` | [[!UICONTROL 註解]](../data-types/annotation.md)的陣列 | 其他屬性無法傳達處方的其他相關資訊。 |
| [!UICONTROL 執行者] | `performer` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 藥物治療/管理的指定執行者。 若是裝置，這是用於執行藥物管理的裝置。 |
| [!UICONTROL 執行者型別] | `performerType` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 指示藥物管理的執行者型別。 |
| [!UICONTROL 先前的處方] | `priorPrescription` | [[!UICONTROL 參考]](../data-types/reference.md) | 此要求所取代的訂單或處方參考。 |
| [!UICONTROL 原因] | `reason` | [[!UICONTROL 可程式碼參考的陣列]](../data-types/reference.md) | 訂購或不訂購藥物的原因或指示。 |
| [!UICONTROL 錄製器] | `recorder` | [[!UICONTROL 參考]](../data-types/reference.md) | 代表其他人輸入訂單的人員。 |
| [!UICONTROL 請求者] | `requester` | [[!UICONTROL 參考]](../data-types/reference.md) | 起始要求並負責啟用的個人、組織或裝置。 |
| [!UICONTROL 狀態原因] | `statusReason` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 要求目前狀態的原因。 |
| [!UICONTROL 主旨] | `subject` | [[!UICONTROL 參考]](../data-types/reference.md) | 要求藥物的個人或群組。 |
| [!UICONTROL 替代] | `substitution` | 物件 | 指示替代是否可以或應該成為分配的一部分。 包含三個屬性： <li>`allowedBoolean`：如果處方允許替代，則布林值為true。</li> <li>`allowedCodeableConcept`：在處方程式允許替代時，提供程式碼的[[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md)值。</li> <li>`reason`：表示替代原因的[[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md)值。</li> |
| [!UICONTROL 支援資訊] | `supportingInformation` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 支援滿足藥物需求的資訊，例如患者的身高和體重。 |
| [!UICONTROL 編寫於] | `authoredOn` | 日期時間 | 處方撰寫的日期（以及選擇性的時間）。 |
| [!UICONTROL 不執行] | `doNotPerform` | 布林值 | True的布林值指示器是病人應該停止（或不開始）服用藥物。 |
| [!UICONTROL 意圖] | `intent` | 字串 | 請求的目的。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `original-order` </li> <li> `reflex-order` </li> <li> `filler-order` </li> <li> `instance-order` </li> <li> `option` </li> |
| [!UICONTROL 優先順序] | `priority` | 字串 | 請求的優先順序。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `routine` </li> <li> `urgent` </li> <li> `asap` </li> <li> `stat` </li> |
| [!UICONTROL 演算後的劑量指示] | `renderedDosageInstruction` | 字串 | 所有劑量說明中包含的劑量完整表示法。 包含多個劑量指示時使用，以表示複雜劑量，例如增加或遞減劑量。 |
| [!UICONTROL 已回報] | `reported` | 布林值 | 表示此記錄是否被擷取為次要報告的記錄，而不是原始的主要真相來源記錄。 |
| [!UICONTROL 狀態] | `status` | 字串 | 分配的狀態。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL 狀態已變更] | `statusChanged` | 日期時間 | 狀態變更的日期（以及可選時間）。 |

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.schema.json)

## `dispenseRequest` {#dispense-request}

`dispenseRequest`是以物件陣列的形式提供。 每個物件的結構如下所述。

![分配要求結構](../../../images/healthcare/field-groups/medication-request/dispense-request.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 分配間隔] | `dispenseInterval` | [[!UICONTROL 持續時間]](../data-types/duration.md) | 藥物配發之間必須發生的最短時間。 |
| [!UICONTROL 分配器] | `dispenser` | [[!UICONTROL 參考]](../data-types/reference.md) | 按照處方者指定將配發藥物的目標組織。 |
| [!UICONTROL 分配器指示] | `dispenserInstruction` | [[!UICONTROL 註解]](../data-types/annotation.md)的陣列 | 針對分配器的其他資訊，例如要向患者提供的諮詢 |
| [!UICONTROL 劑量管理輔助] | `doseAdministrationAid` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 為藥物配發提供的粘合包裝型別相關資訊。 |
| [!UICONTROL 預期供給持續時間] | `expectedSupplyDuration` | [[!UICONTROL 持續時間]](../data-types/duration.md) | 預期使用所供應產品的期間時間，或預期分配持續的時間長度。 |
| [!UICONTROL 初始填滿] | `initialFill` | 物件 | 初始填充的資訊。 包含兩個屬性： <li>`quantity`： [[!UICONTROL 簡單數量]](../data-types/simple-quantity.md)值，提供第一次分配期間要提供的金額。</li> <li>`duration`： [[!UICONTROL Duration]](../data-types/duration.md)值，提供第一個分配預期持續的時間長度。</li> |
| [!UICONTROL 數量] | `quantity` | [[!UICONTROL 簡單數量]](../data-types/simple-quantity.md) | 要為填色分配的金額。 |
| [!UICONTROL 有效期間] | `validityPeriod` | [[!UICONTROL 週期]](../data-types/period.md) | 處方的有效期。 |
| [!UICONTROL 允許的重複專案數] | `numberOfRepeatsAllowed` | 整數 | 已授權的重新填入次數，最小值為0。 |
