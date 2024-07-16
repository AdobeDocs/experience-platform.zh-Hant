---
solution: Experience Platform
title: 具有訂閱資料型別的通用行銷偏好設定欄位
description: 瞭解具有訂閱XDM資料型別的通用行銷偏好設定欄位。
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 1%

---

# [!UICONTROL 具有訂閱]資料型別的通用行銷偏好設定欄位

[!UICONTROL 具有訂閱的通用行銷偏好設定欄位]是標準的XDM資料型別，說明客戶針對特定行銷偏好設定的選擇。

>[!NOTE]
>
>此資料型別旨在使用[[!UICONTROL 同意和偏好設定]欄位群組](../field-groups/profile/consents.md)做為基準，用來自訂您組織的同意結構描述的結構。
>
>如果您不需要特定行銷偏好設定欄位的`subscriptions`對應，可以改用[基本行銷欄位資料型別](./marketing-field.md)。

![](../images/data-types/marketing-field-subscriptions.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `reason` | 字串 | 當客戶選擇退出行銷使用案例時，此字串欄位代表客戶選擇退出的原因。 |
| `subscriptions` | 地圖 | 特定訂閱的客戶行銷偏好設定地圖。 如需詳細資訊，請參閱[訂閱](#subscriptions)的相關章節。 |
| `time` | 日期時間 | 行銷偏好設定變更時間的ISO 8601時間戳記（如適用）。 |
| `val` | 字串 | 此行銷使用案例的客戶提供偏好設定選擇。 如需接受的值和定義，請參閱[下一節](#val)。 |

{style="table-layout:auto"}

## `val` {#val}

下表概述`val`的接受值：

| 值 | 標題 | 說明 |
| --- | --- | --- |
| `y` | 是（選擇加入） | 客戶已選擇加入偏好設定。 換言之，他們&#x200B;**同意**&#x200B;使用相關偏好設定所指示的資料。 |
| `n` | 否（選擇退出） | 客戶已選擇退出偏好設定。 換句話說，他們&#x200B;**不**&#x200B;同意使用相關偏好設定所指示的資料。 |
| `p` | 待處理的驗證 | 系統尚未收到最終偏好設定值。 這最常用於需要兩步驟驗證的同意作業。 例如，如果客戶選擇接收電子郵件，該同意會設為`p`，直到他們在電子郵件中選取連結，以驗證他們是否已提供正確的電子郵件地址，屆時同意會更新為`y`。<br><br>如果此喜好設定未使用兩集驗證程式，則可能改為使用`p`選項來表示客戶尚未回應同意提示。 例如，您可以在客戶回應同意提示前，在網站的第一頁自動將值設為`p`。 在不要求明確同意的管轄區中，您也可以使用它來表示客戶尚未明確選擇退出（換言之，假設您同意）。 |
| `u` | 未知 | 客戶的偏好設定資訊不明。 |
| `dy` | 預設為「是（選擇加入）」 | 客戶本身並未提供同意值，且預設會被視為選擇加入（「是」）。 換言之，除非客戶另有指示，否則假定您同意。<br><br>請注意，如果法律或您公司隱私權政策的變更導致部分或所有使用者的預設值變更，您必須手動更新包含預設值的所有設定檔。 |
| `dn` | 「否」的預設值（選擇退出） | 客戶本身並未提供同意值，且預設會視為選擇退出（「否」）。 換言之，在客戶指出不同意見之前，他們會被假定為已拒絕同意。<br><br>請注意，如果法律或您公司隱私權政策的變更導致部分或所有使用者的預設值變更，您必須手動更新包含預設值的所有設定檔。 |
| `LI` | 合法利益 | 為了特定目的收集和處理這些資料的合法商業利益，壓倒了它對個人造成的潛在傷害。 |
| `CT` | 合約 | 為特定目的收集資料是履行與個人的合約義務所必需的。 |
| `CP` | 遵守法律義務 | 為了符合企業的法律義務，必須針對特定目的收集資料。 |
| `VI` | 個人的重大利益 | 為了保護個人切身利益，必須針對特定目的收集資料。 |
| `PI` | 公共利益 | 為特定目的收集資料是執行符合公眾利益或行使官方權力的任務所必需的。 |

{style="table-layout:auto"}

## `subscriptions` {#subscriptions}

某些企業允許客戶選擇加入與特定行銷管道相關的不同訂閱。 例如，銀行公司可讓客戶訂閱超額帳戶的電話警示，或接收忠誠計畫優惠的銷售電話。

以下JSON代表包含`subscriptions`對應之電話行銷管道的行銷欄位範例。 `subscriptions`物件中的每個索引鍵代表行銷管道的個別訂閱。 每個訂閱都包含選擇加入值(`val`)。

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
| `val` | 訂閱的[同意值](#val)。 |
| `type` | 訂閱型別。 這可以是任何描述性字串，但前提是長度不超過15個字元。 |
| `topics` | 一組字串，代表客戶訂閱的興趣區域，可用來傳送相關內容給客戶。 |
| `subscribers` | 選用的對應型別欄位，代表已訂閱特定訂閱的一組識別碼（例如電子郵件地址或電話號碼）。 此物件中的每個索引鍵都代表相關識別碼，並包含兩個子屬性： <ul><li>`time`：身分訂閱時間的ISO 8601時間戳記（如適用）。</li><li>`source`：訂閱者源自的來源。 這可以是任何描述性字串，但前提是長度不超過15個字元。</li></ul> |

{style="table-layout:auto"}

## 其他資源

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
