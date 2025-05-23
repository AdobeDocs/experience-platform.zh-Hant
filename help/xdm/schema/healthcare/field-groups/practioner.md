---
title: 從業人員結構描述欄位群組
description: 瞭解從業人員結構描述欄位群組。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 71210303-a3dd-458c-9c8a-ac8b546c2b1d
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 7%

---

# [!UICONTROL 從業者]結構描述欄位群組

[!UICONTROL Practioner]是[[!DNL XDM Individual Profile] 類別](../../../classes/individual-profile.md)和[[!DNL Provider class]](../../../classes/provider.md)的標準結構描述欄位群組。 它提供單一物件型別欄位`healthcarePractioner`，其中包含直接或間接參與提供醫療保健或相關服務之人員的相關資訊。

![欄位群組結構](../../../images/healthcare/field-groups/practitioner/practitioner.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 位址] | `address` | [[!UICONTROL 位址]](../data-types/address.md)的陣列 | 超出工作地點的從業人員地址，例如住家地址。 |
| [!UICONTROL 通訊] | `communication` | 物件陣列 | 可用來與從業人員溝通的語言。 如需詳細資訊，請參閱下方的[區段](#communication) |
| [!UICONTROL 識別碼] | `identifier` | [[!UICONTROL 識別碼]](../data-types/identifier.md)的陣列 | 適用於此角色中之人員的識別碼。 |
| [!UICONTROL 名稱] | `name` | [[!UICONTROL 人類名稱]](../data-types/human-name.md)的陣列 | 與從業人員相關聯的名稱。 |
| [!UICONTROL 資格] | `qualification` | 物件陣列 | 官方資格、認證、認證、培訓、授權或類似專案，授權或涉及從業人員提供的護理。 如需詳細資訊，請參閱[&#128279;](#qualification)下方的區段。 |
| [!UICONTROL 連絡人詳細資料] | `telecom` | [[!UICONTROL 聯絡點]](../data-types/contact-point.md)的陣列 | 從業者的聯絡詳細資訊。 |
| [!UICONTROL 作用中] | `active` | 布林值 | 表示從業者記錄是否在使用中。 |
| [!UICONTROL 出生日期] | `birthDate` | 日期 | 從業人員的出生日期。 |
| [!UICONTROL 已死亡的指標] | `deceasedBoolean` | 布林值 | 表示從業者是否死亡。 |
| [!UICONTROL 去世的日期時間] | `deceasedDateTime` | 日期時間 | 從業者死亡的日期和時間。 |
| [!UICONTROL 性別] | `gender` | 字串 | 個人的性別識別。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/practitioner.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/practitioner.schema.json)

## `communication` {#communication}

`communication`是以物件陣列的形式提供。 每個物件的結構如下所述。

![通訊結構](../../../images/healthcare/field-groups/practitioner/communication.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 語言] | `language` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 可用來與個人溝通其健康狀況的語言。 |
| [!UICONTROL 是慣用語言] | `preferred` | 布林值 | 指示語言是否為他們的偏好語言。 |

## `qualification` {#qualification}

`qualification`是以物件陣列的形式提供。 每個物件的結構如下所述。

![資格結構](../../../images/healthcare/field-groups/practitioner/qualification.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 代碼] | `code` | [[!UICONTROL 可程式碼概念]](../data-types/codeable-concept.md) | 資格的編碼表示。 |
| [!UICONTROL 識別碼] | `identifier` | [[!UICONTROL 識別碼]](../data-types/identifier.md)的陣列 | 適用於資格的識別碼。 |
| [!UICONTROL 簽發者] | `issuer` | [[!UICONTROL 參考]](../data-types/reference.md) | 監管並簽發資格的組織。 |
| [!UICONTROL 週期] | `period` | [[!UICONTROL 週期]](../data-types/period.md) | 資格的有效期間。 |
