---
title: 涵蓋範圍結構描述欄位群組
description: 瞭解涵蓋範圍結構欄位群組。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 7b84c0cf-3bd4-4ba8-a8cc-85e6b3f2b59e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 6%

---

# [!UICONTROL 涵蓋範圍]結構描述欄位群組

[!UICONTROL 涵蓋範圍]是[[!DNL Plan] 類別](../../../classes/plan.md)的標準結構描述欄位群組。 它提供單一物件型別欄位`healthcareCoverage`，用於提供保險計畫的高階識別碼和描述元，通常是出現在保險卡上的資訊，可能用於支付提供醫療保健產品及服務的部分或全部費用。

![欄位群組結構](../../../images/healthcare/field-groups/coverage/coverage.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 計畫受益人] | `beneficiary` | [[!UICONTROL 參考]](../data-types/reference.md) | 提供產品或服務時，享受保險保障的一方和患者。 |
| [!UICONTROL 類別] | `class` | 物件陣列 | 包銷商特定分類器的套件。 如需詳細資訊，請參閱[&#128279;](#class)下方的區段。 |
| [!UICONTROL 連絡人] | `contract` | [[!UICONTROL 參考]](../data-types/reference.md)的陣列 | 構成此保險的保單。 |
| [!UICONTROL 受益人成本] | `costToBeneficiary` | 物件陣列 | 表示成本類別和相關金額的代碼套裝，已在政策中詳細說明，可能包含在健康情況卡上。 如需詳細資訊，請參閱[&#128279;](#cost-to-beneficiary)下方的區段。 |
| [!UICONTROL 例外狀況] | `exception` | 物件陣列 | 表示病患成本及其有效期間例外或減少的代碼套裝。 如需詳細資訊，請參閱[&#128279;](#exception)下方的區段。 |
| [!UICONTROL 識別碼] | `identifier` | [[!UICONTROL 識別碼]](../data-types/identifier.md)的陣列 | 由保險公司所核發的保險範圍的識別碼。 |
| [!UICONTROL 保險方案] | `insurancePlan` | [[!UICONTROL 參考]](../data-types/reference.md) | 保險計畫明細、福利及構成此保險範圍的成本。 |
| [!UICONTROL 保險公司] | `insurer` | [[!UICONTROL 參考]](../data-types/reference.md) | 方案或計畫承保人、付款人或保險公司。 |
| [!UICONTROL 付款者] | `paymentBy` | 物件陣列 | 付款方的連結，以及付款方所應承擔的責任（選擇性）。 如需詳細資訊，請參閱[&#128279;](#payment-by)下方的區段。 |
| [!UICONTROL 涵蓋範圍的開始和結束日期] | `period` | [[!UICONTROL 週期]](../data-types/period.md) | 有效涵蓋範圍的時段。 缺少開始日期表示開始日期不明，缺少結束日期表示承保範圍仍在進行中。 |
| [!UICONTROL 原則持有者] | `policyHolder` | [[!UICONTROL 參考]](../data-types/reference.md) | 持有保單的一方。 |
| [!UICONTROL 受益人關係] | `relationship` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 受益人與訂閱者的關係。 |
| [!UICONTROL 訂閱者] | `subscriber` | [[!UICONTROL 參考]](../data-types/reference.md) | 與原則保持合約關係的一方。 |
| [!UICONTROL 訂閱者識別碼] | `subscriberId` | [[!UICONTROL 識別碼]](../data-types/identifier.md)的陣列 | 訂閱者的保險公司指派識別碼。 |
| [!UICONTROL 類型] | `type` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 涵蓋範圍型別。 |
| [!UICONTROL 相依號碼] | `dependent` | 字串 | 承保範圍下家屬的指示項。 |
| [!UICONTROL 種類] | `kind` | 字串 | 涵蓋範圍型別。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `insurance` </li> <li> `self-pay` </li> <li> `other` </li> |
| [!UICONTROL 保險公司網路] | `network` | 字串 | 受益人可能尋求治療的提供者網路，將依網路內費率承保，否則將適用網路外條款與條件。 |
| [!UICONTROL 涵蓋範圍訂單] | `order` | 整數 | 涵蓋範圍的相對順序，最小值為`0`。 |
| [!UICONTROL 狀態] | `status` | 字串 | 涵蓋範圍的狀態。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `active` </li> <li> `cancelled` </li> <li> `draft` </li> <li> `entered-in-error` </li> |
| [!UICONTROL 代位權] | `subrogation` | 布林值 | 當`true`時，此保險執行個體並未納入裁決，而是為了向保險公司提供詳細資料以收回成本。 |

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.schema.json)

## `class` {#class}

`class`是以物件陣列的形式提供。 每個物件的結構如下所述。

![類別結構](../../../images/healthcare/field-groups/coverage/class.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 類型] | `type` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md)的陣列 | 提供保險公司特定類別標籤（或編號與選擇性名稱）的分類型別。 例如，型別可用來識別承保類別、僱主群組、原則或計畫。 |
| [!UICONTROL 值] | `value` | [[!UICONTROL 識別碼]](../data-types/identifier.md) | 與保險公司簽發的標籤相關聯的英數字元識別碼。 |
| [!UICONTROL 名稱] | `name` | 字串 | 類別的簡短說明。 |

## `costToBeneficiary` {#cost-to-beneficiary}

`costToBeneficiary`是以物件陣列的形式提供。 每個物件的結構如下所述。

![受益人結構的成本](../../../images/healthcare/field-groups/coverage/cost-to-beneficiary.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 類別] | `category` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 此程式碼用於識別所提供產品和服務之權益的一般型別。 |
| [!UICONTROL 網路] | `network` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 此程式碼可指出權益是指網路內或網路外提供者。 |
| [!UICONTROL 字詞] | `term` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 值的辭彙，例如最大期限權益。 |
| [!UICONTROL 類型] | `type` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 與治療相關的以病人為中心的成本類別。 |
| [!UICONTROL 單位] | `unit` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 指示福利是否適用於個人或家庭。 |

## `exception` {#exception}

`exception`是以物件陣列的形式提供。 每個物件的結構如下所述。

![例外狀況結構](../../../images/healthcare/field-groups/coverage/exception.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 類型] | `type` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 特定例外狀況的代碼。 |
| [!UICONTROL 週期] | `period` | [[!UICONTROL 週期]](../data-types/period.md) | 例外狀況為作用中的時間範圍。 |

## `paymentBy` {#payment-by}

`paymentBy`是以物件陣列的形式提供。 每個物件的結構如下所述。

![依結構付款](../../../images/healthcare/field-groups/coverage/payment-by.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 派對] | `party` | [[!UICONTROL 參考]](../data-types/reference.md) | 為處理成本提供非保險付款的當事人清單。 |
| [!UICONTROL 責任] | `responsibility` | 字串 | 財務責任的摘要。 |
