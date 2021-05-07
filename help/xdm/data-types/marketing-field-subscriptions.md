---
solution: Experience Platform
title: 具有訂閱資料類型的一般行銷偏好設定欄位
topic-legacy: overview
description: 本檔案提供「一般行銷偏好設定欄位」與「訂閱XDM」資料類型的概述。
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---

# [!UICONTROL Generic Marketing Preference Field with Subscriptions] 資料類型

[!UICONTROL Generic Marketing Preference Field with Subscriptions] 是標準的XDM資料類型，可說明客戶對特定行銷偏好的選擇。

>[!NOTE]
>
>此資料類型旨在使用[[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)]欄位群組](../field-groups/profile/consents.md)做為基準，自訂您組織的同意結構。
>
>如果您不需要特定行銷偏好設定欄位的`subscriptions`對應，則可改用[基本行銷欄位資料類型](./marketing-field.md)。

![](../images/data-types/marketing-field-subscriptions.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `reason` | 字串 | 當客戶退出行銷使用案例時，此字串欄位代表客戶退出的原因。 |
| `subscriptions` | 地圖 | 特定訂閱的客戶行銷偏好圖。 如需詳細資訊，請參閱[subscriptions](#subscriptions)一節。 |
| `time` | DateTime | 行銷偏好設定變更時的ISO 8601時間戳記（如果適用）。 |
| `val` | 字串 | 此行銷使用案例的客戶提供的偏好選擇。 請參閱[下一節](#val)以取得接受的值和定義。 |

## `val` {#val}

下表概述`val`的接受值：

| 值 | 標題 | 說明 |
| --- | --- | --- |
| `y` | 是 | 客戶已選擇加入偏好設定。 換言之，他們&#x200B;**do**&#x200B;同意使用其資料，如有關偏好所示。 |
| `n` | 無 | 客戶已選擇退出偏好設定。 換言之，他們&#x200B;**不同意按照有關偏好使用其資料。** |
| `p` | 待覈實 | 系統尚未收到最終偏好值。 這通常是需要兩步驟驗證的同意的一部分。 例如，如果客戶選擇接收電子郵件，則該同意會設為`p`，直到他們在電子郵件中選擇連結以確認他們提供了正確的電子郵件地址，此時該同意會更新為`y`。<br><br>如果此偏好不使用兩組驗證程式，則該選 `p` 擇可用於指示客戶尚未響應許可提示。例如，您可以在客戶回應同意提示之前，自動將網站第一頁的值設為`p`。 在不需要明確同意的司法管轄區中，您也可以使用該司法管轄區來指出客戶未明確選擇退出（換言之，假定同意）。 |
| `u` | 未知 | 客戶的偏好資訊未知。 |
| `LI` | 合法利益 | 收集並處理資料以達到特定目的的正當商業利益，比其對個人的潛在傷害要大。 |
| `CT` | 合約 | 為達到特定目的而收集資料，是為了履行與個人的合同義務。 |
| `CP` | 遵守法律義務 | 為達到特定目的而收集資料，是為了履行企業的法律義務。 |
| `VI` | 個人的切身利益 | 為了保護個人的切身利益，必須收集符合特定目的的資料。 |
| `PI` | 公共利益 | 為特定目的收集資料，是為了公共利益或行使官方權力而執行的。 |

## `subscriptions` {#subscriptions}

有些企業允許客戶選擇與特定行銷管道相關的不同訂閱。 例如，銀行公司可能允許客戶訂閱透支帳戶的電話提醒，或接收忠誠度方案優惠的銷售電話。

下列JSON代表電話呼叫行銷渠道的範例行銷欄位，其中包含`subscriptions`對應。 `subscriptions`物件中的每個索引鍵代表行銷管道的個別訂閱。 反過來，每個訂閱都包含選擇加入值(`val`)。

```json
"phone-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "subscribers": {
        "123-555-0928": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "overdrawn-account": {
      "val": "y",
      "type": "issues",
      "subscribers": {
        "123-555-0928": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "301-555-1527": {
          "time": "2020-02-03T07:54:21+07:00",
          "source": "call center"
        }
      }
    }
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `type` | 訂閱類型。 此字串可以是任何描述性字串，但需15個字元或更少。 |
| `subscribers` | 可選的地圖類型欄位，代表已訂閱特定訂閱的一組識別碼（例如電子郵件地址或電話號碼）。 此物件中的每個索引鍵代表相關的識別碼，並包含兩個子屬性： <ul><li>`time`:身分訂閱時的ISO 8601時間戳記（如果適用）。</li><li>`source`:訂閱者的來源。此字串可以是任何描述性字串，但需15個字元或更少。</li></ul> |

## 其他資源

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
