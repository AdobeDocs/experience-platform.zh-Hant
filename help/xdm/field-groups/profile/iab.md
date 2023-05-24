---
keywords: Experience Platform；主題；熱門主題；模式；模式；XDM；單個配置檔案；欄位；模式；模式；模式；模式設計；欄位組；欄位組；iab;tcf;connection;
solution: Experience Platform
title: IAB TCF 2.0配置檔案架構的同意欄位組
description: 本文檔概述了XDM Individual Profile類的IAB TCF 2.0同意架構欄位組。
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# [!UICONTROL IAB TCF 2.0同意] 配置檔案架構的欄位組

>[!NOTE]
>
>本文檔涵蓋 [!UICONTROL IAB TCF 2.0同意] XDM Individual Profile類的架構欄位組。 有關用於XDM ExperienceEvent類的欄位組，請參閱以下內容 [文檔](../event/iab.md) 的雙曲餘切值。

[!UICONTROL IAB TCF 2.0同意] 是標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md) 用於捕獲時間戳序列IAB同意字串，以便跟蹤隨時間變化的同意更改模式。

![](../../images/field-groups/iab-profile.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `identityPrivacyInfo` | 地圖 | 將客戶的個人身份值與不同的TCF同意字串相關聯的映射類型對象。 下面提供了此對象結構的示例。 |

{style="table-layout:auto"}

以下JSON演示了 `identityPrivacyInfo` 地圖。

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

如示例所示， `xdm:identityPrivacyInfo` 與Identity Service識別的標識命名空間相對應。 而且，每個命名空間屬性必須至少有一個子屬性，其密鑰與該命名空間的客戶相應標識值匹配。 在本示例中，客戶用Experience CloudID(`ECID`)值 `13782522493631189`。

>[!NOTE]
>
>雖然上面的示例使用單個命名空間/值對來表示客戶的標識，但您可以為其他命名空間添加附加的鍵，並且每個命名空間可以具有多個標識值，每個標識值都具有各自的TCF同意首選項集。

對於每個標識值， `identityIABConsent` 必須提供屬性，該屬性提供身份的TCF同意值。 此屬性的值必須符合 [[!UICONTROL 同意字串] 資料類型](../../data-types/consent-string.md)。

請參閱上的指南 [平台中的IAB TCF 2.0支援](../../../landing/governance-privacy-security/consent/iab/overview.md) 的子菜單。 有關欄位組本身的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
