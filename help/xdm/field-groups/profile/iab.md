---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；個別設定檔；欄位；結構；結構描述；結構描述設計；欄位群組；欄位群組；iab；tcf；同意；
solution: Experience Platform
title: 設定檔結構描述的IAB TCF 2.0同意欄位群組
description: 瞭解XDM個別設定檔類別的IAB TCF 2.0同意結構描述欄位群組。
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# [!UICONTROL IAB TCF 2.0同意] 設定檔結構描述的欄位群組

>[!NOTE]
>
>本檔案涵蓋 [!UICONTROL IAB TCF 2.0同意] xdm個別設定檔類別的結構描述欄位群組。 若是用於XDM ExperienceEvent類別的欄位群組，請參閱下列內容 [檔案](../event/iab.md) 而非。

[!UICONTROL IAB TCF 2.0同意] 是的標準結構描述欄位群組 [[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md) 用於擷取時間戳記系列IAB同意字串，以追蹤一段時間內的同意變更模式。

![](../../images/field-groups/iab-profile.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `identityPrivacyInfo` | 地圖 | 對應型別物件，將客戶的個別身分值與不同的TCF同意字串建立關聯。 以下提供此物件結構的範例。 |

{style="table-layout:auto"}

下列JSON示範結構 `identityPrivacyInfo` 地圖。

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

如範例所示，的每一個根層級索引鍵 `xdm:identityPrivacyInfo` 對應至Identity Service識別的身分名稱空間。 反過來，每個名稱空間屬性必須至少有一個子屬性，其索引鍵符合該名稱空間中客戶對應的身分值。 在此範例中，客戶以Experience CloudID (`ECID`)值 `13782522493631189`.

>[!NOTE]
>
>雖然上述範例使用單一名稱空間/值組來代表客戶的身分，但您可以為其他名稱空間新增其他金鑰，而每個名稱空間可以有多個身分值，每個值都有自己的TCF同意偏好設定集。

對於每個身分值， `identityIABConsent` 必須提供屬性，此屬性會提供身分的TCF同意值。 此屬性的值必須符合 [[!UICONTROL 同意字串] 資料型別](../../data-types/consent-string.md).

請參閱以下指南： [平台中的IAB TCF 2.0支援](../../../landing/governance-privacy-security/consent/iab/overview.md) 以取得此欄位群組使用案例的詳細資訊。 如需欄位群組本身的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
