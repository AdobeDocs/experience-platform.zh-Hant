---
title: 使用邊緣網路伺服器API的伺服器端個人化
description: 本文示範如何使用Edge Network Server API在您的Web屬性上部署伺服器端個人化。
keywords: 個人化；伺服器api;邊緣網路；伺服器端；
source-git-commit: 3e7084953a5e158059074c857bfce4940a83661b
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 2%

---


# 使用邊緣網路伺服器API的伺服器端個人化

## 總覽 {#overview}

伺服器端個人化包含使用 [邊緣網路伺服器API](../../server-api/overview.md) 個人化您Web屬性上的客戶體驗。

在本文所述的範例中，個人化內容是使用伺服器API在伺服器端擷取。 然後，根據擷取的個人化內容在伺服器端轉譯HTML。

下表顯示個人化和非個人化內容的範例。

| 未個人化的範例頁面 | 具有個人化的範例頁面 |
|---|---|
| ![沒有個人化的範例網頁](assets/plain.png) | ![具有個人化的範例網頁](assets/personalized.png) |

## 考量事項 {#considerations}

### Cookie {#cookies}

Cookie可用來保存使用者身分和叢集資訊。  使用伺服器端實作時，應用程式伺服器會在請求生命週期期間處理這些Cookie的儲存和傳送作業。

| Cookie | 用途 | 儲存者 | 傳送者 |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | 包含使用者身分詳細資料。 | 應用程式伺服器 | 應用程式伺服器 |
| `kndctr_AdobeOrg_cluster` | 指示應使用哪個邊緣網路群集來滿足請求。 | 應用程式伺服器 | 應用程式伺服器 |

### 請求投放 {#request-placement}

需要個人化請求才能取得主張並傳送顯示通知。 使用伺服器端實作時，應用程式伺服器會向邊緣網路伺服器API提出這些要求。

| 請求 | 製作者 |
|---|---|
| Interact請求以檢索主張 | 應用程式伺服器呼叫邊緣網路伺服器API。 |
| 傳送顯示通知的互動請求 | 應用程式伺服器呼叫邊緣網路伺服器API。 |

## 範例應用程式 {#sample-app}

以下說明的程式使用範例應用程式，您可以從此作為起點，來實驗並深入了解此類個人化。

您可以下載此範例，並根據您自己的需求加以自訂。 例如，您可以變更環境變數，讓範例應用程式從您自己的Experience Platform設定提取選件。

若要這麼做，請開啟 `.env` 檔案（位於存放庫根目錄），並根據您的設定修改變數。 重新啟動範例應用程式，即可開始使用您自己的個人化內容進行實驗。

### 執行範例 {#running-sample}

請依照下列步驟執行範例應用程式。

1. 原地複製 [此存放庫](https://github.com/adobe/alloy-samples) 到你的本地機器。
2. 開啟終端機並導覽至 `personalization-server-side` 檔案夾。
3. 執行 `npm install`.
4. 執行 `npm start`.
5. 開啟網頁瀏覽器並導覽至 `http://localhost`.

## 程式概述 {#process}

本節說明擷取個人化內容時所使用的步驟。

1. [Express](https://expressjs.com/) 用於精益伺服器端實作。 這可處理基本伺服器請求和路由。
2. 瀏覽器要求網頁。 瀏覽器先前儲存的任何Cookie，首碼為 `kndctr_`，則會納入。
3. 從應用程式伺服器要求頁面時，會將事件傳送至 [互動式資料收集端點](../../../server-api/interactive-data-collection.md) 擷取個人化內容。 範例應用程式使用協助方法來簡化建立請求及傳送請求至API的程式(請參閱 [aepEdgeClient.js](https://github.com/adobe/alloy-samples/blob/main/common/aepEdgeClient.js))。 此 `POST` 要求包含 `event` 和 `query`. 前一步驟的Cookie（若有）會包含在 `meta>state>entries` 陣列。

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

4. 從回應中讀取表單式活動的Target選件，並在產生HTML回應時使用。
5. 對於表單式活動，必須在實作中手動傳送顯示事件，以指出選件已顯示的時間。 在此範例中，通知會在請求生命週期期間由伺服器端傳送。

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

6. [!DNL Visual Experience Composer (VEC)] 選件會遭到忽略，因為只能透過Web SDK轉譯。
7. 傳回HTML回應時，應用程式伺服器會在回應上設定身分和叢集Cookie。