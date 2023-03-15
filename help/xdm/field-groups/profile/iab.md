---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；個別設定檔；欄位；結構；結構；結構；結構設計；欄位群組；欄位群組；iab;tcf；同意；
solution: Experience Platform
title: 設定檔結構的IAB TCF 2.0同意欄位群組
description: 本檔案概述XDM個別設定檔類別的IAB TCF 2.0同意結構欄位群組。
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# [!UICONTROL IAB TCF 2.0同意] 設定檔結構的欄位群組

>[!NOTE]
>
>本檔案涵蓋 [!UICONTROL IAB TCF 2.0同意] XDM個別設定檔類別的架構欄位群組。 有關用於XDM ExperienceEvent類別的欄位群組，請參閱下列內容 [檔案](../event/iab.md) 。

[!UICONTROL IAB TCF 2.0同意] 是的標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md) 用於擷取時間戳記系列IAB同意字串，以追蹤隨時間變化的同意變更模式。

![](../../images/field-groups/iab-profile.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `identityPrivacyInfo` | 地圖 | 將客戶的個別身分值與不同TCF同意字串建立關聯的對應類型物件。 以下提供此物件結構的範例。 |

{style="table-layout:auto"}

下列JSON示範的結構 `identityPrivacyInfo` 地圖。

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

如範例所示， `xdm:identityPrivacyInfo` 與身分識別服務所識別的身分識別命名空間對應。 反過來，每個命名空間屬性至少必須有一個子屬性，其索引鍵與該命名空間的客戶對應身分值相符。 在此範例中，會以Experience CloudID來識別客戶(`ECID`)值 `13782522493631189`.

>[!NOTE]
>
>雖然上述範例使用單一命名空間/值組來表示客戶的身分，但您可以為其他命名空間新增其他索引鍵，而每個命名空間可以有多個身分值，每個都有各自專屬的TCF同意偏好設定集。

對於每個身分值， `identityIABConsent` 必須提供屬性，以提供身分的TCF同意值。 此屬性的值必須符合 [[!UICONTROL 同意字串] 資料類型](../../data-types/consent-string.md).

請參閱 [平台中的IAB TCF 2.0支援](../../../landing/governance-privacy-security/consent/iab/overview.md) 有關此欄位組的使用案例的詳細資訊。 如需欄位群組本身的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
