---
title: 配置Adobe Experience Platform Web SDK
description: 了解如何配置Adobe Experience Platform Web SDK。
seo-description: 了解如何配置Experience PlatformWeb SDK
keywords: 設定；設定；SDK；邊緣；Web SDK；設定；edgeConfigId；內容；網頁；裝置；環境；placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent；網頁設定；prehidingStyle；不透明度；cookieDestinationsEnabled;urlDesitionsEnabled;idMigrationEnabled；第三方CookiesEnabled
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: 549203c8ddc94e00cf4e4ba432f367ddc371cb27
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 14%

---

# 配置平台Web SDK

SDK的設定是使用`configure`命令完成。

>[!IMPORTANT]
>
>`configure` 始終 ** 是第一個命令，稱為。

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
>**Edge Configurations已重新命名為Datastreams。資料流ID與配置ID相同。**

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 是 | None |

{style=&quot;table-layout:auto&quot;}

您指派的設定ID，會將SDK連結至適當的帳戶和設定。 在單一頁面內設定多個執行個體時，您必須為每個執行個體設定不同的`edgeConfigId`。

### `context`

| **類型** | **必填** | **預設值** |
| ---------------- | ------------ | -------------------------------------------------- |
| 字串陣列 | 無 | `["web", "device", "environment", "placeContext"]` |

{style=&quot;table-layout:auto&quot;}

指示要自動收集的上下文類別，如[自動資訊](../data-collection/automatic-information.md)中所述。 如果未指定此配置，預設會使用所有類別。

### `debugEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `false` |

{style=&quot;table-layout:auto&quot;}

指出是否已啟用除錯。 將此配置設定為`true`將啟用以下功能：

| **功能** | **函數** |
| ---------------------- | ------------------ |
| 同步驗證 | 驗證根據結構收集的資料，並在回應中以下列標籤傳回錯誤：`collect:error OR success` |
| 主控台記錄 | 啟用偵錯訊息，以顯示在瀏覽器的JavaScript主控台中 |

{style=&quot;table-layout:auto&quot;}

### `edgeDomain` {#edge-domain}

將您的第一方網域填入此欄位。 有關更多詳細資訊，請參閱[文檔](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=zh-Hant)。

此域類似於網站www的`data.{customerdomain.com}`。{customerdomain.com}。

### `orgId`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 是 | 無 |

{style=&quot;table-layout:auto&quot;}

您指派的[!DNL Experience Cloud]組織ID。 在頁面內設定多個執行個體時，您必須為每個執行個體設定不同的`orgId`。

## 資料彙集

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

{style=&quot;table-layout:auto&quot;}

指出系統是否會自動收集與連結點按次數相關聯的資料。 如需詳細資訊，請參閱[自動連結追蹤](../data-collection/track-links.md#automaticLinkTracking) 。 如果連結包含下載屬性或連結結尾是副檔名，也會標示為下載連結。 下載連結限定符可以使用規則運算式進行設定。 預設值為 `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 函數 | 無 | ()=>未定義 |

{style=&quot;table-layout:auto&quot;}

設定在傳送前對每個事件呼叫的回呼。 欄位`xdm`的物件會傳送至回呼。 要更改發送的內容，請修改`xdm`對象。 在回呼內，`xdm`物件已在event命令中傳遞資料，且已自動收集資訊。 有關此回呼的時間和示例的詳細資訊，請參閱[全局修改事件](tracking-events.md#modifying-events-globally)。

## 隱私權選項

### `defaultConsent` {#default-consent}

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 物件 | 無 | `"in"` |

{style=&quot;table-layout:auto&quot;}

設定使用者的預設同意。 如果尚未為用戶保存同意首選項，請使用此設定。 其他有效值為`"pending"`和`"out"`。 此預設值不會持續存在使用者的設定檔中。 只有在呼叫`setConsent`時，才會更新使用者的設定檔。
* `"in"`:當設定此設定或未提供值時，工作將在不使用者同意偏好設定的情況下進行。
* `"pending"`:設定此設定時，會排入佇列，直到使用者提供同意偏好設定為止。
* `"out"`:設定此設定時，會捨棄工作，直到使用者提供同意偏好設定為止。提供使用者偏好設定後，工作會根據使用者偏好設定而繼續或中止。 如需詳細資訊，請參閱[支援同意](../consent/supporting-consent.md) 。

## 個人化選項

### `prehidingStyle`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 無 | 無 |

{style=&quot;table-layout:auto&quot;}

用於建立CSS樣式定義，在從伺服器載入個人化內容時隱藏網頁的內容區域。 若未提供此選項，則SDK不會在載入個人化內容時嘗試隱藏任何內容區域，這可能會導致「忽隱忽現」。

例如，如果網頁上的元素ID為`container`，當從伺服器載入個人化內容時，您要隱藏其預設內容，請使用下列預先隱藏樣式：

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## 對象選項

### `cookieDestinationsEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

{style=&quot;table-layout:auto&quot;}

啟用[!DNL Audience Manager] Cookie目的地，以便根據區段資格設定Cookie。

### `urlDestinationsEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

{style=&quot;table-layout:auto&quot;}

啟用[!DNL Audience Manager] URL目的地，以便根據區段資格觸發URL。

## 身分選項

### `idMigrationEnabled` {#id-migration-enabled}

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

{style=&quot;table-layout:auto&quot;}

若為true，則SDK會讀取並設定舊的AMCV Cookie。 此選項有助於轉換為使用Adobe Experience Platform Web SDK，而網站的某些部分可能仍使用Visitor.js。 如果頁面上已定義訪客API,SDK會查詢ECID的訪客API。 此選項可讓您使用Adobe Experience Platform Web SDK執行雙標籤頁面，但仍有相同的ECID。

### `thirdPartyCookiesEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

{style=&quot;table-layout:auto&quot;}

啟用Adobe第三方Cookie的設定。 SDK可在協力廠商內容中保留訪客ID，以便跨網站使用相同的訪客ID。 如果您有多個網站，或想要與合作夥伴共用資料，請使用此選項；不過，有時出於隱私權原因，不需要此選項。
