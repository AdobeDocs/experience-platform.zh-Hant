---
title: 地址資料型別
description: 瞭解地址體驗資料模型(XDM)資料型別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 21213bd5-00f4-43cc-80cf-2c0dcf878a23
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 9%

---

# [!UICONTROL 位址]資料型別

[!UICONTROL 地址]是標準的體驗資料模型(XDM)資料型別，描述使用郵遞區號慣例（而非GPS或其他位置定義格式）表示的地址。 此資料型別是根據HL7 FHIR Release 5規格建立的。

![位址資料型別結構](../../../images/healthcare/data-types/address.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 週期] | `period` | [[!UICONTROL 週期]](../data-types/period.md) | 位址使用中的時段。 |
| [!UICONTROL 城市] | `city` | 字串 | 城市名稱。 |
| [!UICONTROL 國家/地區] | `country` | 字串 | ISO 3166國際標準中說明的國家代碼。 程式碼可以是alpha-2或alpha-3。 |
| [!UICONTROL 地區] | `district` | 字串 | 地區名稱。 |
| [!UICONTROL 行] | `line` | 字串 | 街道名稱、編號、方向、郵政信箱或類似專案。 |
| [!UICONTROL 郵遞區號] | `postalCode` | 字串 | 郵遞區號。 |
| [!UICONTROL 狀態] | `state` | 字串 | 國家/地區的子單位。 可接受縮寫。 |
| [!UICONTROL 文字] | `text` | 字串 | 地址的文字表示。 |
| [!UICONTROL 類型] | `type` | 字串 | 地址型別。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `postal` </li> <li> `physical` </li> <li> `both` </li> |
| [!UICONTROL 使用] | `use` | 字串 | 地址的用途。 此屬性的值必須等於下列其中一個已知列舉值。 <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `billing`</li> |

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.schema.json)
