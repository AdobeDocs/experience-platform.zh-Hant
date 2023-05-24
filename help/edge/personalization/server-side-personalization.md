---
title: 使用邊緣網路伺服器API的伺服器端個性化
description: 本文演示了如何使用邊緣網路伺服器API在Web屬性上部署伺服器端個性化設定。
keywords: 個性化；伺服器api;邊緣網路；伺服器端；
source-git-commit: 3e7084953a5e158059074c857bfce4940a83661b
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 2%

---


# 使用邊緣網路伺服器API的伺服器端個性化

## 總覽 {#overview}

伺服器端個性化包括使用 [邊緣網路伺服器API](../../server-api/overview.md) 個性化您的Web屬性上的客戶體驗。

在本文中描述的示例中，使用伺服器API檢索個性化內容伺服器端。 然後，基於檢索到的個性化內容，在伺服器端呈現HTML。

下表顯示了個性化和非個性化內容的示例。

| 未個性化的示例頁 | 具有個性化的示例頁 |
|---|---|
| ![沒有個性化的示例網頁](assets/plain.png) | ![具有個性化的示例網頁](assets/personalized.png) |

## 考量事項 {#considerations}

### Cookie {#cookies}

Cookie用於保留用戶標識和群集資訊。  當使用伺服器端實現時，應用伺服器在請求生命週期中處理這些cookie的儲存和發送。

| Cookie | 用途 | 儲存者 | 發送者 |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | 包含用戶標識詳細資訊。 | 應用程式伺服器 | 應用程式伺服器 |
| `kndctr_AdobeOrg_cluster` | 指示應使用哪個邊緣網路群集來滿足請求。 | 應用程式伺服器 | 應用程式伺服器 |

### 請求放置 {#request-placement}

需要個性化請求才能獲取建議併發送顯示通知。 當使用伺服器端實現時，應用伺服器向邊緣網路伺服器API發出這些請求。

| 請求 | 製作者 |
|---|---|
| 交互請求以檢索主張 | 調用邊緣網路伺服器API的應用程式伺服器。 |
| 交互請求以發送顯示通知 | 調用邊緣網路伺服器API的應用程式伺服器。 |

## 示例應用程式 {#sample-app}

下面描述的過程使用示例應用程式，您可以將該應用程式用作實驗和瞭解此類個性化的詳細資訊的起點。

您可以下載此示例並根據自己的需要對其進行自定義。 例如，您可以更改環境變數，以便示例應用從您自己的Experience Platform配置中引入優惠。

為此，請開啟 `.env` 檔案，並根據您的配置修改變數。 重新啟動示例應用，您就可以嘗試使用自己的個性化內容。

### 運行示例 {#running-sample}

按照以下步驟運行示例應用。

1. 克隆 [此儲存庫](https://github.com/adobe/alloy-samples) 你的本地機器。
2. 開啟終端並導航至 `personalization-server-side` 的子菜單。
3. 運行 `npm install`。
4. 運行 `npm start`。
5. 開啟Web瀏覽器並導航到 `http://localhost`。

## 流程概述 {#process}

本節介紹檢索個性化內容時使用的步驟。

1. [快](https://expressjs.com/) 用於精益伺服器端實現。 這可處理基本伺服器請求和路由。
2. 瀏覽器請求網頁。 瀏覽器先前儲存的所有Cookie，前置詞為 `kndctr_`的雙曲餘切值。
3. 當從應用伺服器請求頁面時，會向 [互動式資料收集終結點](../../../server-api/interactive-data-collection.md) 獲取個性化內容。 示例應用使用幫助程式方法簡化生成和向API發送請求（請參見） [aepEdgeClient.js](https://github.com/adobe/alloy-samples/blob/main/common/aepEdgeClient.js))。 的 `POST` 請求包含 `event` 和 `query`。 上一步中的Cookie（如果可用）包含在 `meta>state>entries` 陣列。

   ```js
   fetch(
   "https://edge.adobedc.net/ee/v2/interact?dataStreamId=abc&requestId=123",
   {
      headers: {
         accept: "*/*",
         "accept-language": "en-US,en;q=0.9",
         "cache-control": "no-cache",
         "content-type": "text/plain; charset=UTF-8",
         pragma: "no-cache",
         "sec-fetch-dest": "empty",
         "sec-fetch-mode": "cors",
         "sec-fetch-site": "cross-site",
         "sec-gpc": "1",
         "Referrer-Policy": "strict-origin-when-cross-origin",
         Referer: "http://localhost/",
      },
      body: JSON.stringify({
         event: {
         xdm: {
            web: {
               webPageDetails: {
               URL: "http://localhost/",
               },
               webReferrer: {
               URL: "",
               },
            },
            identityMap: {
               FPID: [
               {
                  id: "xyz",
                  authenticatedState: "ambiguous",
                  primary: true,
               },
               ],
            },
            timestamp: "2022-06-23T22:21:00.878Z",
         },
         data: {},
         },
         query: {
         identity: {
            fetch: ["ECID"],
         },
         personalization: {
            schemas: [
               "https://ns.adobe.com/personalization/default-content-item",
               "https://ns.adobe.com/personalization/html-content-item",
               "https://ns.adobe.com/personalization/json-content-item",
               "https://ns.adobe.com/personalization/redirect-item",
               "https://ns.adobe.com/personalization/dom-action",
            ],
            decisionScopes: ["__view__", "sample-json-offer"],
         },
         },
         meta: {
         state: {
            domain: "localhost",
            cookiesEnabled: true,
            entries: [
               {
               "key": "kndctr_XXX_AdobeOrg_identity",
               "value": "abc123"
               },
               {
               "key": "kndctr_XXX_AdobeOrg_cluster",
               "value": "or2"
               }
            ],
         },
         },
      }),
      method: "POST",
   }
   ).then((res) => res.json());
   ```

4. 從基於表單的活動中讀取目標服務，並在生成HTML響應時使用。
5. 對於基於表單的活動，必須在實施中手動發送顯示事件，以指示何時顯示了優惠。 在本示例中，通知在請求生命週期期間在伺服器端發送。

   ```js
   function sendDisplayEvent(aepEdgeClient, req, propositions, cookieEntries) {
   const address = getAddress(req);
   
   aepEdgeClient.interact(
      {
         event: {
         xdm: {
            web: {
               webPageDetails: { URL: address },
               webReferrer: { URL: "" },
            },
            timestamp: new Date().toISOString(),
            eventType: "decisioning.propositionDisplay",
            _experience: {
               decisioning: {
               propositions: propositions.map((proposition) => {
                  const { id, scope, scopeDetails } = proposition;
   
                  return {
                     id,
                     scope,
                     scopeDetails,
                  };
               }),
               },
            },
         },
         },
         query: { identity: { fetch: ["ECID"] } },
         meta: {
         state: {
            domain: "",
            cookiesEnabled: true,
            entries: [...cookieEntries],
         },
         },
      },
      {
         Referer: address,
      }
   );
   }
   ```

6. [!DNL Visual Experience Composer (VEC)] 服務將被忽略，因為只能通過Web SDK呈現這些服務。
7. 當返回HTML響應時，在應用伺服器的響應上設定標識和群集cookie。