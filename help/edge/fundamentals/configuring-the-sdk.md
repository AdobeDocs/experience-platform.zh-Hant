---
title: 配置Adobe Experience Platform Web SDK
description: 了解如何配置Adobe Experience Platform Web SDK。
seo-description: Learn how to configure the Experience Platform Web SDK
keywords: 設定；設定；SDK；邊緣；Web SDK；設定；edgeConfigId；內容；網頁；裝置；環境；placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent；網頁設定；prehidingStyle；不透明度；cookieDestinationsEnabled;urlDesitionsEnabled;idMigrationEnabled；第三方CookiesEnabled
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: ed39d782ba6991a00a31b48abb9d143e15e6d89e
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 10%

---

# 配置平台Web SDK

SDK的設定已完成， `configure` 命令。

>[!IMPORTANT]
>
>`configure` is *always* 第一個命令稱為。

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

設定期間可設定許多選項。 所有選項均可在下方找到，依類別分組。

## 一般選項

### `edgeConfigId`

>[!NOTE]
>
>**Edge Configurations已重新命名為Datastreams。 資料流ID與設定ID相同。**

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 是 | None |

{style="table-layout:auto"}

您指派的設定ID，會將SDK連結至適當的帳戶和設定。 在單一頁面中設定多個例項時，您必須設定不同的 `edgeConfigId` ，針對每個例項。

### `context` {#context}

| **類型** | **必填** | **預設值** |
| ---------------- | ------------ | -------------------------------------------------- |
| 字串陣列 | 無 | `["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]` |

{style="table-layout:auto"}

指示要自動收集的上下文類別，如 [自動資訊](../data-collection/automatic-information.md). 如果未指定此配置，預設會使用所有類別。

>[!IMPORTANT]
>
>所有上下文屬性， `highEntropyUserAgentHints`，則預設為啟用。 如果您在Web SDK設定中手動指定內容屬性，必須啟用所有內容屬性才能繼續收集所需資訊。

啟用 [高熵客戶端提示](user-agent-client-hints.md#enabling-high-entropy-client-hints) 在您的Web SDK部署中，您必須包含 `highEntropyUserAgentHints` 內容選項，以及您現有的設定。

例如，要從Web屬性中檢索高熵客戶端提示，您的配置如下所示：

`context: ["highEntropyUserAgentHints", "web"]`


### `debugEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `false` |

{style="table-layout:auto"}

指出是否已啟用除錯。 將此設定設為 `true` 啟用下列功能：

| **功能** | **函數** |
| ---------------------- | ------------------ |
| 主控台記錄 | 啟用偵錯訊息，以顯示在瀏覽器的JavaScript主控台中 |

{style="table-layout:auto"}

### `edgeDomain` {#edge-domain}

將您的第一方網域填入此欄位。 如需詳細資訊，請參閱 [檔案](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=zh-Hant).

網域類似 `data.{customerdomain.com}` 網站www.{customerdomain.com}。

### `edgeBasePath` {#edge-base-path}

用於與Adobe服務通訊及互動的edgeDomain後面的路徑。  這通常只有在不使用預設生產環境時才會變更。

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 無 | ee |

{style="table-layout:auto"}

### `orgId`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 是 | None |

{style="table-layout:auto"}

您的指派 [!DNL Experience Cloud] 組織ID。 在頁面內設定多個例項時，您必須設定不同的 `orgId` ，針對每個例項。

## 資料收集

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

{style="table-layout:auto"}

指出系統是否會自動收集與連結點按次數相關聯的資料。 請參閱 [自動連結追蹤](../data-collection/track-links.md#automaticLinkTracking) 以取得更多資訊。 如果連結包含下載屬性或連結結尾是副檔名，也會標示為下載連結。 下載連結限定符可以使用規則運算式進行設定。 預設值為 `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 函數 | 無 | ()=>未定義 |

{style="table-layout:auto"}

設定在傳送前對每個事件呼叫的回呼。 具有欄位的物件 `xdm` 會傳送至回呼。 若要變更已傳送的內容，請修改 `xdm` 物件。 在回呼內， `xdm` 物件已在event命令中傳遞資料，且已自動收集資訊。 如需此回呼的時間和範例的詳細資訊，請參閱 [全域修改事件](tracking-events.md#modifying-events-globally).

## 隱私權選項

### `defaultConsent` {#default-consent}

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 物件 | 無 | `"in"` |

{style="table-layout:auto"}

設定使用者的預設同意。 如果尚未為用戶保存同意首選項，請使用此設定。 其他有效值為 `"pending"` 和 `"out"`. 此預設值不會持續存在使用者的設定檔中。 只有在 `setConsent` 的URL。
* `"in"`:當設定此設定或未提供值時，工作將在不使用者同意偏好設定的情況下進行。
* `"pending"`:設定此設定時，會排入佇列，直到使用者提供同意偏好設定為止。
* `"out"`:設定此設定時，會捨棄工作，直到使用者提供同意偏好設定為止。
提供使用者偏好設定後，工作會根據使用者偏好設定而繼續或中止。 請參閱 [支援同意](../consent/supporting-consent.md) 以取得更多資訊。

## 個人化選項 {#personalization}

### `prehidingStyle` {#prehidingStyle}

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 無 | None |

{style="table-layout:auto"}

用於建立CSS樣式定義，在從伺服器載入個人化內容時隱藏網頁的內容區域。 若未提供此選項，則SDK不會在載入個人化內容時嘗試隱藏任何內容區域，這可能會導致「忽隱忽現」。

例如，若您網頁上的元素ID為 `container`，其預設內容會在從伺服器載入個人化內容時隱藏，請使用下列預先隱藏樣式：

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

### `targetMigrationEnabled` {#targetMigrationEnabled}

將個別頁面從 [!DNL at.js] 至Web SDK。

使用此選項可讓Web SDK讀取和寫入舊版 `mbox` 和 `mboxEdgeCluster` 由 [!DNL at.js]. 這可協助您從使用Web SDK的頁面移至使用的頁面時，保留訪客設定檔 [!DNL at.js] 程式庫，反之亦然。

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `false` |

## 對象選項

### `cookieDestinationsEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

{style="table-layout:auto"}

啟用 [!DNL Audience Manager] cookie目的地，可根據區段資格來設定cookie。

### `urlDestinationsEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

{style="table-layout:auto"}

啟用 [!DNL Audience Manager] URL目的地，可根據區段資格觸發URL。

## 身分選項

### `idMigrationEnabled` {#id-migration-enabled}

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

{style="table-layout:auto"}

若為true，則SDK會讀取並設定舊的AMCV Cookie。 此選項有助於轉換為使用Adobe Experience Platform Web SDK，而網站的某些部分可能仍使用Visitor.js。

如果頁面上已定義訪客API,SDK會查詢ECID的訪客API。 此選項可讓您使用Adobe Experience Platform Web SDK執行雙標籤頁面，但仍有相同的ECID。

### `thirdPartyCookiesEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

{style="table-layout:auto"}

啟用Adobe第三方Cookie的設定。 SDK可在協力廠商內容中保留訪客ID，以便跨網站使用相同的訪客ID。 如果您有多個網站，或想要與合作夥伴共用資料，請使用此選項；不過，有時出於隱私權原因，不需要此選項。
