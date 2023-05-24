---
solution: Experience Platform
title: 同意字串資料類型
description: 此文檔概述了「同意字串」XDM資料類型。
exl-id: 288ec79e-074a-4d72-9c5f-e9cd8485b804
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 3%

---

# [!UICONTROL 同意字串] 資料類型

[!UICONTROL 同意字串] 是標準XDM資料類型，它描述表示客戶同意的字串值。 它包括上下文資訊，如同意字串的標準(例如， [IAB透明度和同意框架(TCF)2.0](../field-groups/profile/iab.md))。

![](../images/data-types/consent-string.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `consentStandard` | 字串 | 同意字串的標準。 這有助於確定由同意管理服務設定的同意字串的格式。 |
| `consentStandardVersion` | 字串 | 同意標準的版本，用於準確定義由同意管理服務設定的同意字串的格式。 |
| `consentStringValue` | 字串 | 由同意管理服務提供的完全同意字串。 `consentStandard` 和 `consentStandardVersion` 幫助定義如何分析此字串。 |
| `containsPersonalData` | 布林值 | 如果此欄位為true，則表示需要處理此同意字串以執行同意。 |
| `gdprApplies` | 布林值 | 如果此欄位為真，則表示個人資料會獲得同意。 |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
