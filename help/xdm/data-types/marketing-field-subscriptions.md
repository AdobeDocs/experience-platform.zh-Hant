---
solution: Experience Platform
title: 具有訂閱資料類型的一般行銷偏好設定欄位
description: 本檔案概述「一般行銷偏好設定」欄位與「訂閱XDM」資料類型。
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 1%

---

# [!UICONTROL 具有訂閱的一般行銷偏好設定欄位] 資料類型

[!UICONTROL 具有訂閱的一般行銷偏好設定欄位] 是標準XDM資料類型，可說明客戶對特定行銷偏好設定的選擇。

>[!NOTE]
>
>此資料類型旨在使用自訂組織同意結構的結構， [[!UICONTROL 同意和偏好設定] 欄位群組](../field-groups/profile/consents.md) 作為基線。
>
>若您不需要 `subscriptions` 對應特定的行銷偏好欄位，您可以使用 [基本行銷欄位資料類型](./marketing-field.md) 。

![](../images/data-types/marketing-field-subscriptions.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `reason` | 字串 | 當客戶選擇退出行銷使用案例時，此字串欄位代表客戶選擇退出的原因。 |
| `subscriptions` | 地圖 | 特定訂閱的客戶行銷偏好設定地圖。 請參閱 [訂閱](#subscriptions) 以取得更多資訊。 |
| `time` | DateTime | 行銷偏好設定變更時的ISO 8601時間戳記（若適用）。 |
| `val` | 字串 | 此行銷使用案例由客戶提供的偏好選擇。 請參閱 [下一節](#val) 以取得接受的值和定義。 |

{style="table-layout:auto"}

## `val` {#val}

下表概述 `val`:

| 值 | 標題 | 說明 |
| --- | --- | --- |
| `y` | 是（選擇加入） | 客戶已選擇加入偏好設定。 換句話說， **do** 同意使用其資料，如相關偏好設定所示。 |
| `n` | 否（選擇退出） | 客戶已選擇退出首選項。 換句話說， **不** 同意使用其資料，如相關偏好設定所示。 |
| `p` | 待定驗證 | 系統尚未收到最終首選項值。 這通常用於需要兩步驗證的同意。 例如，如果客戶選擇接收電子郵件，則該同意會設為 `p` 直到他們選取電子郵件中的連結，以確認他們提供的電子郵件地址正確，之後同意會更新為 `y`.<br><br>如果此首選項不使用雙集驗證過程，則 `p` 可以使用選擇來指示客戶尚未響應同意提示。 例如，您可以自動將值設為 `p` 在網站的第一頁，客戶回應同意提示之前。 在不需要明確同意的司法管轄區中，您也可以使用該司法管轄區來指出客戶尚未明確選擇退出（亦即假設同意）。 |
| `u` | 未知 | 客戶的首選項資訊未知。 |
| `dy` | 預設為是（選擇加入） | 客戶本身並未提供同意值，預設會視為選擇加入（「是」）。 換言之，在客戶另有指示前，會假設同意。<br><br>請注意，如果您公司的隱私權原則的法律或變更導致部分或所有使用者的預設值變更，您必須手動更新包含預設值的所有設定檔。 |
| `dn` | 預設為否（選擇退出） | 客戶本身並未提供同意值，預設會視為選擇退出（「否」）。 換言之，在客戶另有指明前，假定客戶拒絕同意。<br><br>請注意，如果您公司的隱私權原則的法律或變更導致部分或所有使用者的預設值變更，您必須手動更新包含預設值的所有設定檔。 |
| `LI` | 合法利益 | 收集和處理這些資料以達到特定目的的合法商業利益，比它對個人造成的潛在傷害要大。 |
| `CT` | 合約 | 為滿足與個人的合同義務，需要收集特定用途的資料。 |
| `CP` | 遵守法律義務 | 為符合企業的法律義務，需要收集特定用途的資料。 |
| `VI` | 個人的切身利益 | 為了保護個人的切身利益，需要收集資料。 |
| `PI` | 公共利益 | 為特定目的收集資料是為了公共利益或行使官方權力而執行任務。 |

{style="table-layout:auto"}

## `subscriptions` {#subscriptions}

有些企業可讓客戶選擇加入與特定行銷管道相關聯的不同訂閱。 例如，銀行公司可允許客戶訂購超支帳戶的電話警報，或接收忠誠計畫優惠的銷售電話。

下列JSON代表電話呼叫行銷管道的行銷欄位範例，其中包含 `subscriptions` 地圖。 中的每個鍵 `subscriptions` 物件代表行銷管道的個別訂閱。 接著，每個訂閱都包含選擇加入值(`val`)。

```json
"email-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "topics": ["discounts", "early-access"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "newsletters": {
      "val": "y",
      "type": "advertising",
      "topics": ["hardware"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "tparan@example.com": {
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
| `val` | 此 [同意值](#val) 訂閱。 |
| `type` | 訂閱類型。 這可以是任何描述性字串，但須為15個或更少字元。 |
| `topics` | 代表客戶所訂閱之感興趣區域的字串陣列，可用來傳送相關內容。 |
| `subscribers` | 可選的地圖類型欄位，代表已訂閱特定訂閱的一組識別碼（例如電子郵件地址或電話號碼）。 此物件中的每個索引鍵代表相關的識別碼，並包含兩個子屬性： <ul><li>`time`:身分訂閱時的ISO 8601時間戳記（若適用）。</li><li>`source`:訂閱者源。 這可以是任何描述性字串，但須為15個或更少字元。</li></ul> |

{style="table-layout:auto"}

## 其他資源

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
