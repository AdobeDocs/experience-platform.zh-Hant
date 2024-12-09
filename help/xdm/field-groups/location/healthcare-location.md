---
title: 位置結構描述欄位群組
description: 瞭解位置結構描述欄位群組。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 5%

---

# [!UICONTROL 位置]結構描述欄位群組

[!UICONTROL 位置]是[[!DNL Location] 類別](../../classes/location.md)的標準結構描述欄位群組。 它提供單一物件型別欄位`healthcareLocation`，可擷取地點的詳細資料和位置資訊。

![欄位群組結構](../../images/field-groups/location.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 位址] | `address` | [[!UICONTROL 位址]](../../data-types/healthcare/address.md) | 實體地點的地址。 |
| [!UICONTROL 特性] | `characteristic` | [[!UICONTROL 可程式碼概念]](../../data-types/healthcare/codeable-concept.md)的陣列 | 位置特性的集合。 |
| [!UICONTROL 連絡人] | `contact` | [[!UICONTROL 延伸連絡人詳細資料]](../../data-types/healthcare/extended-contact-detail.md)的陣列 | 地點的聯絡詳細資訊。 |
| [!UICONTROL 端點] | `endpoint` | [[!UICONTROL 參考]](../../data-types/healthcare/reference.md)的陣列 | 提供位置作業服務存取權的技術端點。 |
| [!UICONTROL 表單] | `form` | [[!UICONTROL 可程式碼概念]](../../data-types/healthcare/codeable-concept.md) | 地點的實體形式。 |
| [!UICONTROL 小時作業] | `hoursOfOperation` | [[!UICONTROL 可用性]](../../data-types/healthcare/availability.md)的陣列 | 此地點通常會在哪些日期和時間開放（包括例外）。 |
| [!UICONTROL 識別碼] | `identifier` | [[!UICONTROL 識別碼]](../../data-types/healthcare/identifier.md)的陣列 | 識別地點的唯一代碼或編號。 |
| [!UICONTROL 管理組織] | `managingOrganization` | [[!UICONTROL 參考]](../../data-types/healthcare/reference.md) | 負責布建和維護的組織。 |
| [!UICONTROL 操作狀態] | `operationalStatus` | [[!UICONTROL 編碼]](../../data-types/healthcare/coding.md) | 位置的作業狀態。 |
| [!UICONTROL 部分位置] | `partOf` | [[!UICONTROL 參考]](../../data-types/healthcare/reference.md) | 此位置所屬的位置。 |
| [!UICONTROL 位置] | `position` | 物件 | 絕對地理位置。 包含雙重格式的三個屬性： <li>`longitude`：含WGS84資料的經度</li> <li>`latitude`：緯度與WGS84基準。</li> <li>`altitude`：高度與WGS84基準。</li> |
| [!UICONTROL 類型] | `type` | [[!UICONTROL 可程式碼概念]](../../data-types/healthcare/codeable-concept.md)的陣列 | 在該位置執行的函式型別。 |
| [!UICONTROL 虛擬服務] | `virtualService` | [[!UICONTROL 虛擬服務詳細資料]](../../data-types/healthcare/virtual-service-detail.md)的陣列 | 虛擬服務的連線詳細資料。 |
| [!UICONTROL 別名] | `alias` | 字串陣列 | 位置為或稱為的替代名稱清單。 |
| [!UICONTROL 說明] | `description` | 字串 | 進一步資訊可識別名稱以外的位置。 |
| [!UICONTROL 模式] | `mode` | 字串 | 位置的模式。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `instance` </li> <li> `kind` </li> |
| [!UICONTROL 名稱] | `name` | 字串 | 位置的名稱。 |
| [!UICONTROL 狀態] | `status` | 字串 | 位置的狀態。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `active` </li> <li> `inactive` </li> <li> `suspended` </li> |

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.schema.json)
