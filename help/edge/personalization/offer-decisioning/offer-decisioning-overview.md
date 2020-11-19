---
title: 選件決策概觀
seo-title: 選件決策與Adobe Experience Platform Web SDK
description: Adobe Experience Platform Web SDK可提供並轉譯選件決策中管理的個人化選件。 您可以使用選件決策UI或API來建立選件和其他相關物件。
seo-description: Adobe Experience Platform Web SDK可提供並轉譯選件決策中管理的個人化選件。 您可以使用選件決策UI或API來建立選件和其他相關物件。
keywords: offer decisioning;decisioning;Web SDK;Platform Web SDK;personalized offers;deliver offers;offer delivery;offer personalization;
translation-type: tm+mt
source-git-commit: 5f90f238a8845cc7bf07d54b89c5c6ccff40469a
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 9%

---


# [!DNL Offer Decisioning] 概述

>[!NOTE]
>
>Adobe Experience Platform Web SDK中的選件決策目前可供特定使用者提早存取。 並非所有IMS組織都可使用此功能。

Adobe Experience Platform可以提 [!DNL Web SDK] 供並轉譯在選件決策中管理的個人化選件。 您可以使用選件決策使用者介面(UI)或API來建立選件和其他相關物件。

## 必要條件

* IMS組織已啟用邊緣決策功能
* 選件、建立的活動
* 已發佈Edge組態

## 術語

使用選件決策時，請務必瞭解下列術語。 如需詳細資訊及檢視其他條款，請造訪選件決策 [辭彙表](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html)。

* **容器：** 容器是隔離機制，可讓不同的顧慮分開。 容器ID是所有儲存庫API的第一個路徑元素。 所有決策物件都位於容器中。

* **決策範圍：** 對於選件決策，這些是Base64編碼的JSON字串，包含您希望選件決策服務用來建議選件的活動和位置ID。

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
   >您可以從UI的「活動概述」頁 **面複製決策範圍** 值。

   ![](assets/decision-scope-copy.png)

* **Edge Configuration:** 如需詳細資訊，請閱讀 [edge組態檔案](../../fundamentals/edge-configuration.md) 。

* **身份**:如需詳細資訊，請閱讀本檔案，說明 [Platform Web SDK如何運用Identity Service](../../identity/overview.md)。

## 啟用選件決策

若要啟用選件決策，您必須執行下列步驟：

1. 在邊緣設定中啟用Adobe Experience Platform [](../../fundamentals/edge-configuration.md) ，並勾選「選件決策」方塊
   ![offer-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)
2. 請依照指示 [安裝SDK](../../fundamentals/installing-the-sdk.md) (SDK可單獨安裝 [，或透過](http://launch.adobe.com/)Adobe Experience Platform Launch安裝。 以下是「平 [台啟動」的快速入門手冊](https://docs.adobe.com/content/help/zh-Hant/launch/using/intro/get-started/quick-start.html))。
3. [設定選件決策的SDK](../../fundamentals/configuring-the-sdk.md) 。 下面提供其他優惠決策的特定步驟。
   * 獨立安裝的SDK
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
   * Platform Launch已安裝SDK
      1. [建立平台啟動屬性](https://docs.adobe.com/content/help/zh-Hant/launch/using/reference/admin/companies-and-properties.html)
      2. [新增平台啟動內嵌代碼](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      3. 從「Edge Configuration」（邊緣設定）下拉式清單中選取設定，以您剛建立的Edge Configuration（邊緣設定）來安裝和設定AEP Web SDK擴充功能。 擴充功能的實用 [檔案](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html)。
         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)
      4. 建立必要的 [資料元素](https://docs.adobe.com/content/help/zh-Hant/launch/using/reference/manage-resources/data-elements.html)。 至少，您需要建立平台網頁SDK識別圖和平台網頁SDK XDM物件資料元素。
         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)
      5. 建立您的 [規則](https://docs.adobe.com/content/help/zh-Hant/launch/using/reference/manage-resources/rules.html)。
         * 新增平台網頁SDK傳送事件動作，並新增 `decisionScopes` 該動作的設定相關內容
            ![send-event-action-decisionScopes](./assets/send-event-action-decisionScopes.png)
      6. [建立並發佈包含](https://docs.adobe.com/content/help/zh-Hant/launch/using/reference/publish/libraries.html) 所有相關規則、資料元素和您已設定之擴充功能的程式庫


## 請求和回應範例

### 一個 `decisionScopes` 值

**請求**

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
| `identityMap` | 是 | 請參閱此 [Identity Service檔案](../../identity/overview.md)。 | 每個請求一個身分。 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | 是 | 包含活動和位置ID的JSON Base64編碼字串陣列。 | 每個請求 `decisionScopes` 最多30個。 | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

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
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
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
| `items.id` | 建議選件的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 與建議選件相關聯之內容的架構。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 建議選件的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 與建議選件相關的內容格式。 | `"format": "text/html"` |
| `language` | 與建議選件內容相關的語言陣列。 | `"language": [ "en-US" ]` |
| `content` | 以字串格式與建議選件相關的內容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式與建議選件關聯的影像內容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 以JSON物件格式與建議選件相關的特性。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### 多個 `decisionScopes` 值

**請求**

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
| `identityMap` | 是 | 請參閱此 [Identity Service檔案](../../identity/overview.md)。 | 每個請求一個身分。 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | 是 | 包含活動和位置ID的JSON Base64編碼字串陣列。 | 每個請求 `decisionScopes` 最多30個。 | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

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
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
              "data": {
                "id": "xcore:personalized-offer:124cc332095cfa74",
                "format": "text/html",
                "language": [
                  "en-US"
                ],
                "content": "<p style=\"color:red;\">20% Off on shipping</p>",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ==",
          "items": [
            {
              "id": "xcore:personalized-offer:235fe313094cdb75",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-text",
              "data": {
                "id": "xcore:personalized-offer:235fe313094cdb75",
                "format": "text/text",
                "language": [
                  "en-US"
                ],
                "content": "20% Off on shipping",
                "characteristics": {
                  "foo2": "bar2",
                  "foo3": "bar3"
                }
              }
            }
          ]
        }
      ],
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyYzkxMzg1Mjc2MDE4YyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMzMxZjU2MTYyYWEyZjcifQ==",
          "items": [
            {
              "id": "xcore:personalized-offer:312de312095cda65",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
              "data": {
                "id": "xcore:personalized-offer:312de312095cda65",
                "format": "image/png",
                "language": [
                  "en-US"
                ],
                "deliveryURL": "https://image.jpeg"
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
| `items.id` | 建議選件的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 與建議選件相關聯之內容的架構。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 建議選件的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 與建議選件相關的內容格式。 | `"format": "text/html"` |
| `language` | 與建議選件內容相關的語言陣列。 | `"language": [ "en-US" ]` |
| `content` | 以字串格式與建議選件相關的內容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式與建議選件關聯的影像內容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 以JSON物件格式與建議選件相關的特性。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
