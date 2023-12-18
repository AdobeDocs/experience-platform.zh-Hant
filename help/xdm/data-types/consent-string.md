---
solution: Experience Platform
title: 同意字串資料型別
description: 瞭解同意字串XDM資料型別。
exl-id: 288ec79e-074a-4d72-9c5f-e9cd8485b804
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 5%

---

# [!UICONTROL 同意字串] 資料型別

[!UICONTROL 同意字串] 是標準的XDM資料型別，說明代表客戶同意的字串值。 其中包含內容相關資訊，例如同意字串的標準(例如 [IAB透明與同意架構(TCF) 2.0](../field-groups/profile/iab.md))。

![](../images/data-types/consent-string.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `consentStandard` | 字串 | 同意字串的標準。 這有助於決定同意管理服務所設定的同意字串格式。 |
| `consentStandardVersion` | 字串 | 同意標準的版本，用來精確定義同意管理服務所設定的同意字串格式。 |
| `consentStringValue` | 字串 | 同意管理服務所提供的完整同意字串。 `consentStandard` 和 `consentStandardVersion` 協助定義如何剖析此字串。 |
| `containsPersonalData` | 布林值 | 當此欄位為true時，表示此同意字串需要經過處理，以達成同意執行。 |
| `gdprApplies` | 布林值 | 此欄位為true時，表示同意和個人資料會一起出現。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
