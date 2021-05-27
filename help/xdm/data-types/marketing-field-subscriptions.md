---
solution: Experience Platform
title: 具有訂閱資料類型的一般行銷偏好設定欄位
topic-legacy: overview
description: 本檔案概述「一般行銷偏好設定」欄位與「訂閱XDM」資料類型。
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 3%

---

# [!UICONTROL 具有訂閱資料類型的一般] 行銷偏好欄位

[!UICONTROL 包含訂閱的一般行] 銷偏好設定欄位是標準XDM資料類型，可說明客戶對特定行銷偏好設定的選擇。

>[!NOTE]
>
>此資料類型旨在使用[[!UICONTROL 隱私權/個人化/行銷偏好設定（同意）]欄位群組](../field-groups/profile/consents.md)作為基準，自訂組織同意結構。
>
>若您不需要特定行銷偏好欄位的`subscriptions`對應，則可改用[基本行銷欄位資料類型](./marketing-field.md)。

![](../images/data-types/marketing-field-subscriptions.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `reason` | 字串 | 當客戶選擇退出行銷使用案例時，此字串欄位代表客戶選擇退出的原因。 |
| `subscriptions` | 地圖 | 特定訂閱的客戶行銷偏好設定地圖。 如需詳細資訊，請參閱[subscriptions](#subscriptions)上的區段。 |
| `time` | DateTime | 行銷偏好設定變更時的ISO 8601時間戳記（若適用）。 |
| `val` | 字串 | 此行銷使用案例由客戶提供的偏好選擇。 請參閱[下一節](#val)以了解接受的值和定義。 |

{style=&quot;table-layout:auto&quot;}

## `val` {#val}

下表概述`val`的接受值：

| 值 | 標題 | 說明 |
| --- | --- | --- |
| `y` | 是 | 客戶已選擇加入偏好設定。 換言之，他們&#x200B;**do**&#x200B;同意使用其資料，如相關偏好所示。 |
| `n` | 無 | 客戶已選擇退出首選項。 換言之，他們&#x200B;**不**&#x200B;同意使用其資料，如相關偏好所示。 |
| `p` | 待定驗證 | 系統尚未收到最終首選項值。 這通常用於需要兩步驗證的同意。 例如，如果客戶選擇接收電子郵件，則該同意會設為`p`，直到客戶選擇電子郵件中的連結以確認他們提供了正確的電子郵件地址，此時同意會更新為`y`。<br><br>如果此首選項不使用兩個設定的驗證過程，則 `p` 可以改用該選項指示客戶尚未響應同意提示。例如，您可以在客戶回應同意提示之前，自動將網站第一頁的值設為`p`。 在不需要明確同意的司法管轄區中，您也可以使用該司法管轄區來指出客戶尚未明確選擇退出（亦即假設同意）。 |
| `u` | 未知 | 客戶的首選項資訊未知。 |
| `LI` | 合法利益 | 收集和處理這些資料以達到特定目的的合法商業利益，比它對個人造成的潛在傷害要大。 |
| `CT` | 合約 | 為滿足與個人的合同義務，需要收集特定用途的資料。 |
| `CP` | 遵守法律義務 | 為符合企業的法律義務，需要收集特定用途的資料。 |
| `VI` | 個人的切身利益 | 為了保護個人的切身利益，需要收集資料。 |
| `PI` | 公共利益 | 為特定目的收集資料是為了公共利益或行使官方權力而執行的。 |

{style=&quot;table-layout:auto&quot;}

## `subscriptions` {#subscriptions}

有些企業可讓客戶選擇加入與特定行銷管道相關聯的不同訂閱。 例如，銀行公司可允許客戶訂購超支帳戶的電話警報，或接收忠誠計畫優惠的銷售電話。

下列JSON代表包含`subscriptions`對映之電話呼叫行銷管道的範例行銷欄位。 `subscriptions`物件中的每個索引鍵代表行銷管道的個別訂閱。 接著，每個訂閱都包含選擇加入值(`val`)。

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
| `type` | 訂閱類型。 這可以是任何描述性字串，但須為15個或更少字元。 |
| `subscribers` | 可選的地圖類型欄位，代表已訂閱特定訂閱的一組識別碼（例如電子郵件地址或電話號碼）。 此物件中的每個索引鍵代表相關的識別碼，並包含兩個子屬性： <ul><li>`time`:身分訂閱時的ISO 8601時間戳記（若適用）。</li><li>`source`:訂閱者源。這可以是任何描述性字串，但須為15個或更少字元。</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 其他資源

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
