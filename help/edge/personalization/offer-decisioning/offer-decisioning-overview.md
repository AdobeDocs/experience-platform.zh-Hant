---
title: 使用Offer decisioning與平台Web SDK
description: Adobe Experience PlatformWeb SDK可以提供和呈現以Offer decisioning管理的個性化服務。 您可以使用Offer decisioningUI或API建立優惠和其他相關對象。
keywords: offer decisioning；決定；Web SDK；平台Web SDK；個性化服務；提供服務；提供服務；提供個性化服務；
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 5%

---

# 使用Offer decisioning與平台Web SDK

>[!NOTE]
>
>在Adobe Experience PlatformWeb SDK中使用Offer decisioning可以提前訪問選定用戶。 此功能不適用於所有組織。

Adobe Experience Platform [!DNL Web SDK] 可以交付和呈現以Offer decisioning管理的個性化優惠。 您可以使用 Offer Decisioning 使用者介面 (UI) 或 API 建立您的優惠方案與其他相關物件。 

## 先決條件

* 已啟用組織以進行邊緣確定
* 優惠、建立的活動
* 資料流已發佈

## 術語

在使用Offer decisioning時，必須瞭解以下術語。 如欲瞭解更多資訊並查看其他條款，請訪問 [offer decisioning辭彙表](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html)。

* **容器：** 容器是一種隔離機構，用於將不同的問題分開。 容器ID是所有儲存庫API的第一個路徑元素。 所有決策對象都駐留在容器中。

* **決策範圍：** 對於Offer decisioning，決策作用域是JSON的Base64編碼字串，包含希望offer decisioning服務用於建議優惠的活動和位置ID。

   *決策範圍JSON:*

   ```json
   {
     "activityId":"xcore:offer-activity:11cfb1fa93381aca",
     "placementId":"xcore:offer-placement:1175009612b0100c"
   }
   ```

   *決策範圍Base64編碼字串：*

   ```json
   "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
   ```

   >[!TIP]
   >
   >您可以從 **活動概述** 的子菜單。

   ![](assets/decision-scope-copy.png)

* **資料流：** 有關詳細資訊，請閱讀 [資料流](../../datastreams/overview.md) 文檔。

* **身份**:有關詳細資訊，請閱讀本文檔，概述如何 [平台Web SDK使用Identity Service](../../identity/overview.md)。

## 啟用Offer decisioning

要啟用Offer decisioning，請執行以下步驟：

1. 已啟用您的Adobe Experience Platform [資料流](../../datastreams/overview.md) 選中「Offer decisioning」框

   ![提供決策邊緣配置](./assets/offer-decisioning-edge-config.png)

1. 按照說明 [安裝SDK](../../fundamentals/installing-the-sdk.md) (SDK可以單獨安裝，也可以通過UI安裝。 查看 [標籤快速入門手冊](../../../tags/quick-start/quick-start.md))。
1. [配置SDK](../../fundamentals/configuring-the-sdk.md) offer decisioning。 下面提供了其他Offer decisioning特定步驟。

   * 安裝獨立SDK

      1. 使用 `decisionScopes`

         ```javascript
          alloy("sendEvent", {
             ...
             "decisionScopes": [
                 "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
                 "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
             ]
          })
         ```
   * 通過標籤安裝SDK

      1. [建立標籤屬性](../../../tags/ui/administration/companies-and-properties.md)
      1. [添加嵌入代碼](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      1. 從「Datastream」下拉清單中選擇配置，使用您建立的Datastream安裝和配置平台Web SDK擴展。 請參閱 [擴展](../../../tags/ui/managing-resources/extensions/overview.md)。

         ![install-aep-web-sdk — 擴展](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk — 擴展](./assets/configure-aep-web-sdk-extension.png)

      1. 建立必要 [資料元素](../../../tags/ui/managing-resources/data-elements.md)。 至少，必須建立平台Web SDK標識映射和平台Web SDK XDM對象資料元素。

         ![標識 — 映射 — 資料元](./assets/identity-map-data-element.png)

         ![xdm對象資料元](./assets/xdm-object-data-element.png)

      1. 建立 [規則](../../../tags/ui/managing-resources/rules.md)。

         * 添加平台Web SDK發送事件操作並添加相關 `decisionScopes` 到該操作的配置

            ![send-event-action-decisionScopes](./assets/send-event-action-decisionScopes.png)
      1. [建立和發佈庫](../../../tags/ui/publishing/libraries.md) 包含您配置的所有相關規則、資料元素和擴展



## 請求和響應示例

### 一 `decisionScopes` 值

**要求**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
          ]
        }
      }
    }
  ]
}
```

| 屬性 | 必填 | 說明 | 限制 | 範例 |
|---|---|---|---|---|
| `identityMap` | 是 | 請參閱此 [Identity Service文檔](../../identity/overview.md)。 | 每個請求一個標識。 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`。<br><br> 注：用戶不需要包括 `ECID` API調用中的參數。 如果需要，此參數將自動添加到調用中。 |
| `decisionScopes` | 是 | 包含活動和位置ID的Base64編碼的JSON字串陣列。 | 最多30 `decisionScopes` 按請求。 | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

**回應**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:124cc332095cfa74",
                "format": "text/html",
                "language": [
                  "en-US"
                ],
                "content": "<p>20% Off on shipping</p>",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| 屬性 | 說明 | 範例 |
|---|---|---|
| `scope` | 導致提議的報價的決定範圍。 | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | 優惠活動的唯一ID。 | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | 聘用位置的唯一ID。 | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | 建議的報價的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 與建議的優惠關聯的內容的模式。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 建議的報價的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 與建議的優惠關聯的內容的格式。 | `"format": "text/html"` |
| `language` | 與建議的服務內容關聯的一組語言。 | `"language": [ "en-US" ]` |
| `content` | 以字串格式與建議的優惠關聯的內容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式與建議的優惠相關聯的影像內容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 與JSON對象格式的建議提供關聯的特性。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### 多重 `decisionScopes` 值

**要求**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyYzkxMzg1Mjc2MDE4YyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMzMxZjU2MTYyYWEyZjcifQ=="
          ]
        }
      }
    }
  ]
}
```

| 屬性 | 必填 | 說明 | 限制 | 範例 |
|---|---|---|---|---|
| `identityMap` | 是 | 請參閱此 [Identity Service文檔](../../identity/overview.md)。 | 每個請求一個標識。 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`。<br><br> 注：用戶不需要包括 `ECID` API調用中的參數。 如果需要，此參數將自動添加到調用中。 |
| `decisionScopes` | 是 | 包含活動和位置ID的Base64編碼的JSON字串陣列。 | 最多30 `decisionScopes` 按請求。 | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

**回應**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MTEyMyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDExMjMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381123",
            "etag": "1"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b01123",
            "etag": "3"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a22954123",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-text",
              "etag": "2",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a22954123",
                "format": "text/text",
                "language": [
                  "en"
                ],
                "content": "20% Off on shipping",
                "characteristics": {
                  "foo2": "bar2"
                }
              }
            }
          ]
        },
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a2295415d",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a2295415d",
                "format": "image/png",
                "language": [
                  "en"
                ],
                "deliveryURL": "https://image.jpeg",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| 屬性 | 說明 | 範例 |
|---|---|---|
| `scope` | 導致提議的報價的決定範圍。 | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | 優惠活動的唯一ID。 | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | 聘用位置的唯一ID。 | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | 建議的報價的ID。 | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | 與建議的優惠關聯的內容的模式。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | 建議的報價的ID。 | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | 與建議的優惠關聯的內容的格式。 | `"format": "text/text"` |
| `language` | 與建議的服務內容關聯的一組語言。 | `"language": [ "en-US" ]` |
| `content` | 以字串格式與建議的優惠關聯的內容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式與建議的優惠相關聯的影像內容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 與JSON對象格式的建議提供關聯的特性。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

## 限制

移動體驗邊緣工作流當前不支援某些服務約束，例如封頂。 「上限設定」欄位值指定可在所有用戶間顯示優惠的次數。 有關詳細資訊，請參閱 [提供資格規則和約束文檔](https://experienceleague.adobe.com/docs/offer-decisioning/using/managing-offers-in-the-offer-library/creating-personalized-offers.html#eligibility)。
