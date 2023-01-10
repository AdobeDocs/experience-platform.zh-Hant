---
solution: Experience Platform
title: 同意字串資料類型
description: 本檔案概述同意字串XDM資料類型。
exl-id: 288ec79e-074a-4d72-9c5f-e9cd8485b804
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 4%

---

# [!UICONTROL 同意字串] 資料類型

[!UICONTROL 同意字串] 是標準XDM資料類型，可說明代表客戶同意的字串值。 其中包含內容資訊，例如同意字串的標準(例如 [IAB透明與同意架構(TCF)2.0](../field-groups/profile/iab.md))。

![](../images/data-types/consent-string.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `consentStandard` | 字串 | 同意字串的標準。 這有助於判斷同意管理服務所設定的同意字串格式。 |
| `consentStandardVersion` | 字串 | 同意標準的版本，可用來精確定義同意管理服務所設定之同意字串的格式。 |
| `consentStringValue` | 字串 | 同意管理服務提供的完整同意字串。 `consentStandard` 和 `consentStandardVersion` 幫助定義如何分析此字串。 |
| `containsPersonalData` | 布林值 | 如果此欄位為true，表示需要處理此同意字串以強制執行同意。 |
| `gdprApplies` | 布林值 | 如果此欄位為true，表示同意會隨個人資料提供。 |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
