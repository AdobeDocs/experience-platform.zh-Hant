---
title: 選件決策概觀
seo-title: 選件決策與Adobe Experience Platform Web SDK
description: Adobe Experience Platform Web SDK可提供並轉譯選件決策中管理的個人化選件。 您可以使用選件決策UI或API來建立選件和其他相關物件。
seo-description: Adobe Experience Platform Web SDK可提供並轉譯選件決策中管理的個人化選件。 您可以使用選件決策UI或API來建立選件和其他相關物件。
keywords: 選件決策；決策；Web SDK；平台Web SDK；個人化選件；傳遞選件；選件傳遞；選件個人化；
translation-type: tm+mt
source-git-commit: 05049025bdfc67af4d811e90218bf6e2613fab51
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 9%

---


# [!DNL Offer Decisioning] 概述

>[!NOTE]
>
>Adobe Experience Platform Web SDK中的選件決策目前可供特定使用者提早存取。 並非所有IMS組織都可使用此功能。

Adobe Experience Platform [!DNL Web SDK]可提供並轉譯在選件決策中管理的個人化選件。 您可以使用選件決策使用者介面(UI)或API來建立選件和其他相關物件。

## 必要條件

* IMS組織已啟用邊緣決策功能
* 選件、建立的活動
* 已發佈Edge組態

## 術語

使用選件決策時，請務必瞭解下列術語。 如需詳細資訊及檢視其他條款，請造訪[選件決策辭彙表](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html)。

* **容器：** 容器是隔離機制，可區隔不同的顧慮。容器ID是所有儲存庫API的第一個路徑元素。 所有決策物件都位於容器中。

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
   >您可以從UI的&#x200B;**活動概述**&#x200B;頁面複製決策範圍值。

   ![](assets/decision-scope-copy.png)

* **Edge Configuration：如需** 詳細資訊，請閱讀 [Edge Configuration](../../fundamentals/edge-configuration.md) 檔案。

* **身份**:如需詳細資訊，請閱讀本檔案，說明 [Platform Web SDK如何運用Identity Service](../../identity/overview.md)。

## 啟用選件決策

若要啟用選件決策，您必須執行下列步驟：

1. 在您的[edge configuration](../../fundamentals/edge-configuration.md)中啟用Adobe Experience Platform，並勾選「選件決策」方塊
   ![offer-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)
2. 請依照指示[安裝SDK](../../fundamentals/installing-the-sdk.md)(SDK可獨立安裝，或透過[Adobe Experience Platform Launch](http://launch.adobe.com/)安裝。 以下是Platform Launch](https://docs.adobe.com/content/help/zh-Hant/launch/using/intro/get-started/quick-start.html)的[快速入門手冊。
3. [設定選件](../../fundamentals/configuring-the-sdk.md) 決策的SDK。下面提供其他優惠決策的特定步驟。
   * 獨立安裝的SDK
      1. 使用您的`decisionScopes`設定「sendEvent」動作

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
      3. 從「Edge Configuration」（邊緣設定）下拉式清單中選取設定，以您剛建立的Edge Configuration（邊緣設定）來安裝和設定AEP Web SDK擴充功能。 關於[extensions](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html)的實用文檔。
         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)
      4. 建立必要的[資料元素](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/data-elements.html)。 至少，您需要建立平台網頁SDK識別圖和平台網頁SDK XDM物件資料元素。
         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)
      5. 建立[規則](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html)。
         * 新增平台網頁SDK傳送事件動作，並將相關的`decisionScopes`新增至該動作的設定
            ![send-event-action-decisionScopes](./assets/send-event-action-decisionScopes.png)
      6. [建立並發佈包](https://docs.adobe.com/content/help/zh-Hant/launch/using/reference/publish/libraries.html) 含您所設定之所有相關規則、資料元素和擴充功能的資料庫


## 請求和回應範例

### 一個`decisionScopes`值

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
| `identityMap` | 是 | 請參閱此[Identity Service文檔](../../identity/overview.md)。 | 每個請求一個身分。 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | 是 | 包含活動和位置ID的JSON Base64編碼字串陣列。 | 每個請求最多30個`decisionScopes`。 | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

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
| `activity.id` | 選件活動的唯一ID。 | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | 選件位置的唯一ID。 | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | 建議選件的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 與建議選件相關聯之內容的架構。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 建議選件的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 與建議選件相關的內容格式。 | `"format": "text/html"` |
| `language` | 與建議選件內容相關的語言陣列。 | `"language": [ "en-US" ]` |
| `content` | 以字串格式與建議選件相關的內容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式與建議選件關聯的影像內容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 以JSON物件格式與建議選件相關的特性。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### 多個`decisionScopes`值

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
| `identityMap` | 是 | 請參閱此[Identity Service文檔](../../identity/overview.md)。 | 每個請求一個身分。 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | 是 | 包含活動和位置ID的JSON Base64編碼字串陣列。 | 每個請求最多30個`decisionScopes`。 | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

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
| `activity.id` | 選件活動的唯一ID。 | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | 選件位置的唯一ID。 | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | 建議選件的ID。 | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | 與建議選件相關聯之內容的架構。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | 建議選件的ID。 | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | 與建議選件相關的內容格式。 | `"format": "text/text"` |
| `language` | 與建議選件內容相關的語言陣列。 | `"language": [ "en-US" ]` |
| `content` | 以字串格式與建議選件相關的內容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式與建議選件關聯的影像內容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 以JSON物件格式與建議選件相關的特性。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
