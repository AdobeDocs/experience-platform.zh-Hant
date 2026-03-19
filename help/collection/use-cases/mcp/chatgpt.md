---
title: 在ChatGPT應用程式（MCP資料收集）中收集分析並套用個人化
description: 使用混合MCP伺服器+ Web SDK applyResponse模式，將事件傳送至Adobe Experience Platform Edge Network，並在ChatGPT應用程式UI內呈現個人化。
keywords: Adobe Experience Platform、網頁SDK、Edge Network、MCP、ChatGPT應用程式、applyResponse、interact端點、個人化、分析
source-git-commit: c848f821ea911c82531c6784a17df0116572cd86
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---

# 在ChatGPT應用程式（MCP資料收集）中收集分析並套用個人化

此使用案例顯示如何將ChatGPT應用程式（模型內容通訊協定伺服器+選用的UI元件）連線至Adobe Experience Platform Edge Network。 此類資料收集可讓您記錄對話式互動的分析，這些互動會叫用您的工具，並從Edge Network將個人化決定傳遞到ChatGPT轉譯的Widget中。

>[!NOTE]
>
>本檔案是根據Adobe資料收集團隊的最新可用更新和OpenAI的最新技術更新進行維護。 因此，Adobe預計此檔案將會隨著時間發展，並建議您回訪以取得更新。

此使用案例偏好使用混合方法，使用伺服器端實作來收集資料，並使用使用者端實作來呈現個人化內容。 此方法非常理想，因為MCP工具叫用是收集分析的最可靠時機。 Widget會在瀏覽器內容中執行，且是儲存身分識別（在Cookie中）及套用個人化決定的正確位置。

此使用案例隨附完整作業程式碼範例。 如需範常式式碼和實作指示，請參閱GitHub上[存放庫中的](https://github.com/adobe/alloy-samples/tree/main/chatgpt-app)ChatGPT應用程式+ Adobe Experience Platform Edge`alloy-samples`。

>[!IMPORTANT]
>
>本頁面概述旨在說明整合模式的參考實作。 在應用程式中採取該方法之前，請先檢閱安全性、隱私權、同意和生產需求。

## 架構

在高層面上，有五個移動零件：

1. **MCP主機(ChatGPT)**： ChatGPT會叫用您的MCP伺服器公開的工具，並在要求中繼資料中提供穩定的假名使用者識別碼。
1. **MCP伺服器（後端）**：由您的組織所擁有。 它會實作列示專案、擷取詳細資料或提交請求等工具。
1. **Adobe IMS**：您的MCP伺服器呼叫Adobe資料收集API所使用的存取權杖發生問題。
1. **Adobe Experience Platform Edge Network**：接收您的MCP伺服器傳送的體驗事件，並傳回Analytics通知、狀態更新（例如身分）和個人化決策。
1. **內嵌Web UI （由MCP主機轉譯的前端Widget）**：顯示結構化結果，並套用從MCP伺服器後端接收的Adobe中繼資料。

## 資料流程

1. **使用者**&#x200B;使用您的MCP伺服器提示&#x200B;**ChatGPT**。
1. **ChatGPT**&#x200B;會解譯提示的意圖，並呼叫適當的&#x200B;**後端MCP工具**。
1. **後端MCP伺服器**&#x200B;使用資料收集API （`interact`端點）將體驗事件傳送至&#x200B;**Edge Network**，以進行分析收集和選用的個人化。
1. **Edge Network**&#x200B;將回應控制代碼（包括狀態更新和個人化決策）傳回至&#x200B;**後端MCP工具**。
1. **後端MCP工具**&#x200B;傳回的工具結果包含`structuredContent`中的商業資料，以及`_meta`到&#x200B;**ChatGPT**&#x200B;的Adobe中繼資料。
1. **ChatGPT**&#x200B;將工具結果傳送至&#x200B;**前端介面工具集**，它會轉譯業務資料，並使用Web SDK JavaScript資料庫的`applyResponse`命令套用Adobe中繼資料。 這個命令會為使用者端狀態提供水合，並在UI中呈現合格的個人化決策。

以下各節將詳細說明每個步驟。

## 步驟1：使用者提示ChatGPT使用您的MCP伺服器

此步驟是工作流程的入口點。 使用者提供自然語言意圖：

```text
"Use the Adobe Office Information Tool to show me details about which office that is the most pet-friendly."
```

如需詳細資訊，請參閱OpenAI開發人員檔案中的[建置您的MCP伺服器](https://developers.openai.com/apps-sdk/build/mcp-server/)。

## 步驟2：ChatGPT解譯意圖並呼叫MCP工具

ChatGPT會根據MCP伺服器的中繼資料，解譯意圖並在MCP伺服器上叫用適當的工具處理常式。 此工具呼叫會為互動建立伺服器端真實點，其獨立於UI呈現成功。 您的其中一項工具可能有下列中繼資料：

```json
{
  "name": "office_details",
  "description": "Fetch details for a single office by ID and return personalization handles for the UI.",
  "inputSchema": {
    "type": "object",
    "properties": {
      "sessionId": { "type": "string", "description": "Server-issued session identifier." },
      "officeId": { "type": "string", "description": "Office identifier." }
    },
    "required": ["sessionId", "officeId"],
    "additionalProperties": false
  },
  "_meta": {
    "ui": {
      "visibility": ["model", "app"]
    }
  }
}
```

請參閱OpenAI開發人員檔案中的[定義工具](https://developers.openai.com/apps-sdk/plan/tools/)，以取得如何告訴ChatGPT每個MCP工具功能的詳細資訊。

## 步驟3：您的MCP伺服器傳送體驗事件至Edge Network

當您的MCP伺服器收到請求時，會觸發對Adobe Experience Platform Edge Network的呼叫，以記錄分析資料並選擇性地請求決策/個人化。 由於此要求是伺服器對伺服器，請使用已驗證的[`interact`](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)端點做為[資料收集API](https://developer.adobe.com/data-collection-apis/docs/)的一部分。 Adobe建議使用[自訂名稱空間](https://experienceleague.adobe.com/zh-hant/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities)來傳遞OpenAI唯一識別碼。 請確定您在身分UI中建立的名稱空間，與您在呼叫中定義的身分名稱空間相符（區分大小寫）。

```sh
curl -X POST "https://server.adobedc.net/ee/v2/interact?datastreamId={DATASTREAM_ID}"
  -H "Authorization: Bearer {TOKEN}"
  -H "x-gw-ims-org-id: {ORG_ID}"
  -H "x-api-key: {API_KEY}"
  -H "Content-Type: application/json"
  -d '{
    "event": {
      "xdm": {
        "eventType": "office.details.view",
        "identityMap": {
          "{IDENTITY_NAMESPACE}": [
            { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
          ]
        },
        "timestamp": "YYYY-02-20T19:00:00.000Z"
      }
    },
    "query": {
      "personalization": {
        "decisionScopes": ["__view__"]
      }
    },
    "meta": {
      "state": {
        "entries": [
          { "key": "kndctr_orgid_cluster", "value": "{CLUSTER_HINT_IF_KNOWN}" },
          { "key": "kndctr_orgid_identity", "value": "{ECID_BLOB_IF_KNOWN}" }
        ]
      }
    }
  }'
```

## 步驟4：Edge Network傳回控制代碼

Edge Network收到您的`interact`呼叫時，會以`handle`陣列回應。 此陣列可包含身分和個人化決策，具體取決於您的資料流設定。 範例回應可能如下所示：

```json
{
  "requestId": "60a2f...2294d",
  "handle": [
    {
      "type": "locationHint:result",
      "payload": [
        { "scope": "EdgeNetwork", "hint": "or2", "ttlSeconds": 1800 }
      ]
    },
    {
      "type": "state:store",
      "payload": [
        { "key": "kndctr_..._identity", "value": "CiYzM...snTI=", "maxAge": 34128000 },
        { "key": "kndctr_..._cluster", "value": "or2", "maxAge": 1800 }
      ]
    }
  ]
}
```

您的MCP伺服器可以從Edge Network回應中擷取資訊，以儲存身分資訊：

```ts
type EdgeHandle = { type: string; payload?: Array<{ key?: string; value?: string }> };

export function extractStateStore(handles: EdgeHandle[]) {
  const store = handles.find(h => h.type === "state:store");
  const entries = store?.payload ?? [];

  const identity = entries.find(e => e.key?.includes("_identity"))?.value;
  const cluster  = entries.find(e => e.key?.includes("_cluster"))?.value;

  return { identity, cluster };
}
```

## 步驟5： MCP伺服器傳回結構化工具輸出以及Adobe中繼資料給ChatGPT

您的MCP工具回應包含Edge Network的結構化工具輸出和個人化。

* `structuredContent`物件包含ChatGPT可以安全讀取及敘述的商業資料。
* `_meta`物件包含Adobe回應控制代碼和伺服器運算的`identityMap`，讓Widget可以讀取它們，而不需將該資料公開給ChatGPT。 將此資訊保留在`_meta.adobe`中，可讓您一致地判斷資料所在的位置。 向前傳遞相同的`identityMap`有助於Widget在任何後續的UI端事件中使用相同的自訂身分。

```json
{
  "content": "Displayed details for office seattle.",
  "structuredContent": {
    "office": {
      "id": "seattle",
      "name": "Seattle",
      "amenities": ["Pet Friendly", "Cafe", "Bike Storage"]
    }
  },
  "_meta": {
    "adobe": {
      "identityMap": {
        "{IDENTITY_NAMESPACE}": [
          { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
        ]
      },
      "handles": [
        {
          "type": "state:store",
          "payload": [
            { "key": "kndctr_..._identity", "value": "..." }
          ]
        },
        {
          "type": "personalization:decisions",
          "payload": [
            { "id": "..." }
          ]
        }
      ]
    }
  }
}
```

如需詳細資訊，請參閱OpenAI開發人員參考中的[工具結果](https://developers.openai.com/apps-sdk/reference/#tool-results)。

## 步驟6： Widget轉譯結果並使用`_adobe.handles`套用`applyResponse`

Widget會轉譯`structuredContent`的商業資料，然後從`_meta.adobe`讀取Adobe中繼資料。 在ChatGPT中，Widget可透過相容性層取得相同的資料：

* `window.openai.toolOutput`包含`structuredContent`
* `window.openai.toolResponseMetadata`包含`_meta`

Widget使用Web SDK JavaScript程式庫的[`applyResponse`](../../js/commands/applyresponse.md)命令來結合使用者端狀態，並轉譯伺服器端`interact`呼叫傳回的個人化決策。 呼叫[`configure`](../../js/commands/configure/overview.md)之前，請務必先呼叫`applyResponse`命令。 由於您的MCP伺服器已執行`interact`呼叫，因此您不需要立即呼叫工具呼叫互動的[`sendEvent`](../../js/commands/sendevent/overview.md)命令。

```js
// Configure the Web SDK before any other commands.
alloy("configure", {
  datastreamId: "YOUR_DATASTREAM_ID",
  orgId: "YOUR_EXPERIENCE_CLOUD_ORG_ID"
});

// Business data exposed to ChatGPT and the widget.
const { office } = window.openai?.toolOutput ?? {};

// Adobe metadata available only to the widget.
const adobe = window.openai?.toolResponseMetadata?.adobe ?? {};
const { identityMap, handles } = adobe;

// Hydrate client-side state and render personalization decisions from the
// server-side interact response.
alloy("applyResponse", {
  renderDecisions: true,
  responseBody: { handle: handles ?? [] }
});
```

如果介面工具集稍後傳送其他UI端事件，您可以在這些呼叫中包含相同的`identityMap`：

```js
alloy("sendEvent", {
  xdm: {
    eventType: "office.details.widgetView",
    identityMap
  }
});
```

此模式保持伺服器端和UI端身分使用方式一致，同時仍允許伺服器端`interact`呼叫保持分析收集和決策的真實來源。

## 驗證

設定上述所有步驟後，您即可驗證下列專案：

* **資料集合：**&#x200B;確認事件已到達所需的資料集，且每個事件都已如預期般處理。
* **Personalization：**&#x200B;確認Edge Network已傳回決定，且決定是由您的Widget轉譯。

## 安全性與隱私權考量事項

* 將ChatGPT的識別碼視為敏感的，即使是以假名輸入。
* 請務必將貴組織的同意和資料控管實務套用至此工作流程。
* Adobe建議使用OAuth 2.1工作流程進行授權。
* 確儲存取權杖和密碼絕對不會連線至使用者端或UI。
