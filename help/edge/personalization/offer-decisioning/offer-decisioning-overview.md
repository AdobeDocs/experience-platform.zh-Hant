---
title: 搭配Platform Web SDK使用Offer decisioning
description: Adobe Experience Platform Web SDK可提供及呈現以Offer decisioning管理的個人化優惠方案。 您可以使用Offer decisioningUI或API來建立選件和其他相關物件。
keywords: offer decisioning；決策；Web SDK;Platform Web SDK；個人化優惠方案；傳送優惠方案；優惠方案傳送；優惠方案個人化；
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 5%

---

# 搭配Platform Web SDK使用Offer decisioning

>[!NOTE]
>
>Adobe Experience Platform Web SDK中可提前存取特定使用者，以使用Offer decisioning。 並非所有組織都可使用此功能。

Adobe Experience Platform [!DNL Web SDK] 可以提供及呈現以Offer decisioning管理的個人化優惠方案。 您可以使用 Offer Decisioning 使用者介面 (UI) 或 API 建立您的優惠方案與其他相關物件。 

## 先決條件

* 組織已啟用邊緣決策功能
* 選件，已建立的活動
* 資料流已發佈

## 術語

使用Offer decisioning時，請務必了解下列術語。 欲知更多資訊和查看其他條款，請訪問 [offer decisioning字彙表](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **容器：** 容器是隔離機制，可分開不同的關注點。 容器ID是所有存放庫API的第一個路徑元素。 所有決策物件都位於容器中。

* **決策範圍：** 若為Offer decisioning，決策範圍是JSON的Base64編碼字串，其中包含您希望offer decisioning服務用來建議選件的活動和位置ID。

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
   >您可以從 **活動概覽** 頁面。

   ![](assets/decision-scope-copy.png)

* **資料流：** 欲知更多資訊，請閱讀 [資料流](../../datastreams/overview.md) 檔案。

* **身分**:如需詳細資訊，請閱讀本檔案，概述如何 [Platform Web SDK使用Identity Service](../../identity/overview.md).

## 啟用Offer decisioning

要啟用Offer decisioning，請執行以下步驟：

1. 在您的 [資料流](../../datastreams/overview.md) 並勾選「Offer decisioning」方塊

   ![offer-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)

1. 請依照 [安裝SDK](../../fundamentals/installing-the-sdk.md) (SDK可獨立安裝，或透過UI安裝。 請參閱 [標籤快速入門手冊](../../../tags/quick-start/quick-start.md))以取得詳細資訊。
1. [配置SDK](../../fundamentals/configuring-the-sdk.md) offer decisioning。 以下提供其他Offer decisioning特定步驟。

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
   * 透過標籤安裝SDK

      1. [建立標籤屬性](../../../tags/ui/administration/companies-and-properties.md)
      1. [新增內嵌程式碼](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      1. 從「Datastream」下拉式清單中選取設定，使用您建立的Datastream安裝並設定Platform Web SDK擴充功能。 請參閱 [擴充功能](../../../tags/ui/managing-resources/extensions/overview.md).

         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)

      1. 建立必要 [資料元素](../../../tags/ui/managing-resources/data-elements.md). 您至少必須建立Platform Web SDK身分對應和Platform Web SDK XDM物件資料元素。

         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)

      1. 建立 [規則](../../../tags/ui/managing-resources/rules.md).

         * 新增平台Web SDK傳送事件動作並新增相關 `decisionScopes` 至動作的設定

            ![send-event-action-decisionScopes](./assets/send-event-action-decisionScopes.png)
      1. [建立並發佈程式庫](../../../tags/ui/publishing/libraries.md) 包含您所設定的所有相關規則、資料元素和擴充功能



## 範例要求與回應

### 一 `decisionScopes` value

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
| `identityMap` | 是 | 請參閱 [Identity服務檔案](../../identity/overview.md). | 每個請求一個身分。 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`。<br><br> 注意：使用者不需要 `ECID` 參數。 如有需要，此參數會自動新增至呼叫。 |
| `decisionScopes` | 是 | 包含活動和位置ID之JSON的Base64編碼字串陣列。 | 最多30個 `decisionScopes` 每個請求。 | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

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
| `scope` | 產生提議的決定範圍。 | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | 優惠方案活動的唯一ID。 | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | 優惠方案版位的唯一ID。 | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | 建議選件的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 與建議選件相關聯的內容綱要。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 建議選件的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 與建議選件相關聯的內容格式。 | `"format": "text/html"` |
| `language` | 與建議選件之內容相關聯的語言陣列。 | `"language": [ "en-US" ]` |
| `content` | 以字串格式與建議的選件相關聯的內容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式與建議的選件相關聯的影像內容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 與建議的選件相關聯的特性，為JSON物件格式。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### 多個 `decisionScopes` 值

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
| `identityMap` | 是 | 請參閱 [Identity服務檔案](../../identity/overview.md). | 每個請求一個身分。 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`。<br><br> 注意：使用者不需要 `ECID` 參數。 如有需要，此參數會自動新增至呼叫。 |
| `decisionScopes` | 是 | 包含活動和位置ID之JSON的Base64編碼字串陣列。 | 最多30個 `decisionScopes` 每個請求。 | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

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
| `scope` | 產生提議的決定範圍。 | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | 優惠方案活動的唯一ID。 | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | 優惠方案版位的唯一ID。 | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | 建議選件的ID。 | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | 與建議選件相關聯的內容綱要。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | 建議選件的ID。 | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | 與建議選件相關聯的內容格式。 | `"format": "text/text"` |
| `language` | 與建議選件之內容相關聯的語言陣列。 | `"language": [ "en-US" ]` |
| `content` | 以字串格式與建議的選件相關聯的內容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式與建議的選件相關聯的影像內容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 與建議的選件相關聯的特性，為JSON物件格式。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

## 限制

行動體驗邊緣工作流程目前不支援某些選件限制，例如限定上限。 「限定」欄位值會指定可向所有使用者呈現選件的次數。 如需詳細資訊，請參閱 [優惠方案適用性規則與限制檔案](https://experienceleague.adobe.com/docs/offer-decisioning/using/managing-offers-in-the-offer-library/creating-personalized-offers.html#eligibility).
