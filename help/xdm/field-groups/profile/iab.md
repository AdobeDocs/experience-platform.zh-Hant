---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；個別設定檔；欄位；結構；結構；結構；結構設計；欄位群組；欄位群組；iab;tcf；同意；
solution: Experience Platform
title: IAB TCF 2.0同意結構欄位群組
topic-legacy: overview
description: 本檔案概述XDM個別設定檔類別的IAB TCF 2.0同意結構欄位群組。
source-git-commit: 9b75a69cc6e31ea0ad77048a6ec1541df2026f27
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 1%

---


# [!UICONTROL IAB TCF 2.0同意] 方案欄位群組

>[!NOTE]
>
>本檔案涵蓋XDM個別設定檔類別的[!UICONTROL  IAB TCF 2.0同意]結構欄位群組。 對於用於XDM ExperienceEvent類的欄位組，請改為參閱以下[document](../event/iab.md)。

[!UICONTROL IAB TCF 2.0同意] 是類別的標準結構欄位群組， [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) 用於擷取時間戳記系列IAB同意字串，以追蹤隨時間變化的同意變更模式。

![](../../images/field-groups/iab-profile.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `identityPrivacyInfo` | 地圖 | 將客戶的個別身分值與不同TCF同意字串建立關聯的對應類型物件。 以下提供此物件結構的範例。 |

{style=&quot;table-layout:auto&quot;}

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

如範例所示，`xdm:identityPrivacyInfo`的每個根層級索引鍵都與Identity Service所識別的身分命名空間相對應。 反過來，每個命名空間屬性至少必須有一個子屬性，其索引鍵與該命名空間的客戶對應身分值相符。 在此範例中，識別Experience Cloud的ID(`ECID`)值為`13782522493631189`。

>[!NOTE]
>
>雖然上述範例使用單一命名空間/值組來表示客戶的身分，但您可以為其他命名空間新增其他索引鍵，而每個命名空間可以有多個身分值，每個都有各自專屬的TCF同意偏好設定集。

必須為每個身分值提供`identityIABConsent`屬性，以提供身分的TCF同意值。 此屬性的值必須符合[[!UICONTROL 同意字串]資料類型](../../data-types/consent-string.md)。

如需此欄位群組使用案例的詳細資訊，請參閱Platform](../../../landing/governance-privacy-security/consent/iab/overview.md)中[IAB TCF 2.0支援的指南。 如需欄位群組本身的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
