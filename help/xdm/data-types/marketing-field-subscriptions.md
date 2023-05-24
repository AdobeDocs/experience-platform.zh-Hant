---
solution: Experience Platform
title: 具有預訂資料類型的一般市場營銷首選項欄位
description: 本文檔提供具有訂閱XDM資料類型的「一般市場營銷首選項」欄位的概覽。
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 1%

---

# [!UICONTROL 具有訂閱的一般市場營銷首選項欄位] 資料類型

[!UICONTROL 具有訂閱的一般市場營銷首選項欄位] 是一個標準XDM資料類型，它描述客戶對特定市場營銷首選項的選擇。

>[!NOTE]
>
>此資料類型用於使用 [[!UICONTROL 同意和首選項] 欄位組](../field-groups/profile/consents.md) 作為基線。
>
>如果你不需要 `subscriptions` 映射特定的市場營銷首選項欄位，您可以使用 [基本市場營銷欄位資料類型](./marketing-field.md) 的雙曲餘切值。

![](../images/data-types/marketing-field-subscriptions.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `reason` | 字串 | 當客戶從市場營銷使用案例中選擇時，此字串欄位表示客戶選擇退出的原因。 |
| `subscriptions` | 地圖 | 特定訂閱的客戶市場營銷首選項的地圖。 請參閱 [訂閱](#subscriptions) 的子菜單。 |
| `time` | 日期時間 | ISO 8601時間戳（如果適用），顯示當市場營銷首選項發生更改時。 |
| `val` | 字串 | 客戶為此市場營銷使用案例提供的首選項選擇。 查看 [下一部分](#val) 以獲取接受的值和定義。 |

{style="table-layout:auto"}

## `val` {#val}

下表概述了 `val`:

| 值 | 標題 | 說明 |
| --- | --- | --- |
| `y` | 是（選擇加入） | 客戶選擇了這種偏好。 換句話說， **做** 同意使用有關優先權所示的資料。 |
| `n` | 否（選擇退出） | 客戶已選擇不參與。 換句話說， **不** 同意使用有關優先權所示的資料。 |
| `p` | 等待驗證 | 系統尚未收到最終首選項值。 這通常是需要兩步驗證的同意的一部分。 例如，如果客戶選擇接收電子郵件，則該同意設定為 `p` 直到他們在電子郵件中選擇一個連結以驗證他們是否提供了正確的電子郵件地址，此時將將同意更新為 `y`。<br><br>如果此首選項不使用兩組驗證進程，則 `p` 而可以使用choice指示客戶尚未響應同意提示。 例如，可以自動將值設定為 `p` 在客戶響應同意提示之前，在網站的首頁上。 在不需要明確同意的管轄區中，您也可以使用它來指示客戶沒有明確選擇不加入（換句話說，假定同意）。 |
| `u` | 未知 | 客戶的首選項資訊未知。 |
| `dy` | 預設為是（選中） | 客戶本身並未提供同意值，預設情況下會被視為選擇加入（「是」）。 換句話說，在客戶另有說明之前，將假定同意。<br><br>請注意，如果法律或公司隱私策略的更改導致某些或所有用戶的預設值發生更改，則必須手動更新包含預設值的所有配置檔案。 |
| `dn` | 預設值為「否」（選擇退出） | 客戶本身並未提供同意值，預設情況下被視為退出（「否」）。 換句話說，假定客戶在表示不同意之前拒絕同意。<br><br>請注意，如果法律或公司隱私策略的更改導致某些或所有用戶的預設值發生更改，則必須手動更新包含預設值的所有配置檔案。 |
| `LI` | 合法利益 | 收集和處理此資料以達到指定目的的合法商業利益超過其對個人的潛在傷害。 |
| `CT` | 合同 | 為了履行與個人的合同義務，需要為特定目的收集資料。 |
| `CP` | 遵守法律義務 | 為履行企業的法律義務，需要為特定目的收集資料。 |
| `VI` | 個人的切身利益 | 為了保護個人的切身利益，需要為特定目的收集資料。 |
| `PI` | 公共利益 | 為特定目的收集資料，是為了公共利益或行使官方權力而執行一項任務。 |

{style="table-layout:auto"}

## `subscriptions` {#subscriptions}

有些企業允許客戶選擇與特定營銷渠道關聯的不同訂閱。 例如，銀行公司可能允許客戶訂閱透支帳戶的電話警報，或接收忠誠計畫優惠的銷售電話。

以下JSON表示電話呼叫市場營銷渠道的示例市場營銷欄位，該渠道包含 `subscriptions` 地圖。 中的每個鍵 `subscriptions` 對象表示市場營銷渠道的單個訂閱。 反過來，每個訂閱都包含一個選擇加入值(`val`)。

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
| `val` | 的 [同意值](#val) 的子菜單。 |
| `type` | 訂閱類型。 這可以是任何描述性字串，前提是它不超過15個字元。 |
| `topics` | 表示客戶所訂閱的感興趣區域的字串陣列，可用於發送相關內容。 |
| `subscribers` | 可選的映射類型欄位，它表示已訂閱特定訂閱的一組標識符（如電子郵件地址或電話號碼）。 此對象中的每個鍵都表示有關的標識符，並包含兩個子屬性： <ul><li>`time`:ISO 8601時間戳（如果適用），指標預訂的時間。</li><li>`source`:訂戶源自的源。 這可以是任何描述性字串，前提是它不超過15個字元。</li></ul> |

{style="table-layout:auto"}

## 其他資源

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
