---
keywords: Experience Platform；首頁；熱門主題；綱要；綱要；XDM；個別設定檔；欄位；綱要；綱要設計；欄位群組；欄位群組；iab；tcf；同意；
solution: Experience Platform
title: 設定檔結構描述的IAB TCF 2.0同意欄位群組
description: 瞭解XDM個別設定檔類別的IAB TCF 2.0同意結構描述欄位群組。
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 1%

---

# 設定檔結構描述的[!UICONTROL IAB TCF 2.0同意]欄位群組

>[!NOTE]
>
>本文介紹XDM個人設定檔類別的[!UICONTROL IAB TCF 2.0同意]結構描述欄位群組。 若是用於XDM ExperienceEvent類別的欄位群組，請改為參閱下列[檔案](../event/iab.md)。

[!UICONTROL IAB TCF 2.0同意]是[[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md)的標準結構描述欄位群組，用於擷取時間戳記系列IAB同意字串，以追蹤一段時間的同意變更模式。

![](../../images/field-groups/iab-profile.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `identityPrivacyInfo` | 地圖 | 對應型別物件，將客戶的個別身分值與不同的TCF同意字串建立關聯。 以下提供此物件結構的範例。 |

{style="table-layout:auto"}

下列JSON示範`identityPrivacyInfo`對應的結構。

```json
{
  "identityPrivacyInfo": {
    "ECID": {
      "13782522493631189": {
        "identityIABConsent": {
          "consentTimestamp": "2020-04-11T05:05:05Z",
          "consentString": {
            "consentStandard": "IAB TCF",
            "consentStandardVersion": "2.0",
            "consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
            "gdprApplies": true,
            "containsPersonalData": false
          }
        }
      }
    }
  }
}
```

如範例所示，`xdm:identityPrivacyInfo`的每個根層級索引鍵都與識別服務所識別的識別名稱空間相對應。 反過來，每個名稱空間屬性必須至少有一個子屬性，其索引鍵符合該名稱空間中客戶對應的身分值。 在此範例中，客戶以`13782522493631189`的Experience Cloud ID (`ECID`)值識別。

>[!NOTE]
>
>雖然上述範例使用單一名稱空間/值組來代表客戶的身分，但您可以為其他名稱空間新增其他金鑰，而每個名稱空間可以有多個身分值，每個值都有自己的TCF同意偏好設定集。

必須為每個身分識別值提供`identityIABConsent`屬性，以提供身分識別的TCF同意值。 這個屬性的值必須符合[[!UICONTROL 同意字串]資料型別](../../data-types/consent-string.md)。

如需此欄位群組使用案例的詳細資訊，請參閱Experience Platform[&#128279;](../../../landing/governance-privacy-security/consent/iab/overview.md)中IAB TCF 2.0支援指南。 如需欄位群組本身的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
