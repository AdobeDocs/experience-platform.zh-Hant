---
title: 設定Adobe Experience Platform網頁SDK
description: 瞭解如何設定Adobe Experience Platform網頁SDK。
seo-description: 瞭解如何設定Experience Platform網頁SDK
keywords: configure;configuration;SDK;edge;Web SDK;configure;edgeConfigId;context;web;device;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConowensen;web sd設定；prehiningStyle；不透明；cookieDesing;webet;e;web sd;e;e;en;ed;emen;up;en;usen;up;usen;ured;ure;usen;urlEnabled;en;used;urlEnabled;ed;ed;ed;urlEn;en;ed;ed;un;ed;un;um;un;urlDestinationsEnabled;idMigrationEnabled;thirdPartyCookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
translation-type: tm+mt
source-git-commit: 2895975b9c103e6afba7db221223b4ef2116caf3
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 8%

---

# 設定平台網頁SDK

SDK的設定是使用`configure`命令完成。

>[!IMPORTANT]
>
>`configure` 永遠 ** 是第一個叫做的命令。

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

在配置期間可以設定許多選項。 所有選項皆可在下方找到，依類別分組。

## 一般選項

### `edgeConfigId`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 是 | None |

{style=&quot;table-layout:auto&quot;}

您指派的設定ID，會將SDK連結至適當的帳戶和設定。 在單頁內配置多個實例時，必須為每個實例配置不同的`edgeConfigId`。

### `context`

| **類型** | **必填** | **預設值** |
| ---------------- | ------------ | -------------------------------------------------- |
| 字串陣列 | 無 | `["web", "device", "environment", "placeContext"]` |

{style=&quot;table-layout:auto&quot;}

指示要自動收集哪些上下文類別，如[自動資訊](../data-collection/automatic-information.md)中所述。 如果未指定此配置，則預設情況下會使用所有類別。

### `debugEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `false` |

{style=&quot;table-layout:auto&quot;}

指出是否啟用除錯。 將此配置設定為`true`將啟用以下功能：

| **功能** | **函數** |
| ---------------------- | ------------------ |
| 同步驗證 | 驗證針對架構收集的資料，並在下列標籤下的回應中傳回錯誤：`collect:error OR success` |
| 控制台記錄 | 啟用除錯訊息，以便顯示在瀏覽器的JavaScript主控台中 |

{style=&quot;table-layout:auto&quot;}

### `edgeDomain` {#edge-domain}

使用您的第一方網域填入此欄位。 如需詳細資訊，請參閱[檔案](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html)。

網域類似於網站的`data.{customerdomain.com}`，網址為www.{customerdomain.com}。

### `orgId`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 是 | 無 |

{style=&quot;table-layout:auto&quot;}

您指派的[!DNL Experience Cloud]組織ID。 在頁面中配置多個實例時，必須為每個實例配置不同的`orgId`。

## 資料彙集

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

{style=&quot;table-layout:auto&quot;}

指出是否會自動收集與連結點按次數相關的資料。 如需詳細資訊，請參閱[自動連結追蹤](../data-collection/track-links.md#automaticLinkTracking)。

### `onBeforeEventSend`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 函數 | 無 | ()=>未定義 |

{style=&quot;table-layout:auto&quot;}

設定回呼，在每個事件傳送前呼叫它。 欄位`xdm`的對象將發送到回調。 要更改所發送的內容，請修改`xdm`對象。 在回呼中，`xdm`物件已具有在event命令中傳遞的資料，以及自動收集的資訊。 有關此回呼的時間安排和示例的詳細資訊，請參閱[全局修改事件](tracking-events.md#modifying-events-globally)。

## 隱私權選項

### `defaultConsent` {#default-consent}

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 物件 | 無 | `"in"` |

{style=&quot;table-layout:auto&quot;}

設定使用者的預設同意。 當使用者尚未儲存同意偏好設定時，請使用此設定。 其他有效值為`"pending"`和`"out"`。 此預設值不會持續存在於使用者的設定檔中。 只有當呼叫`setConsent`時，才會更新使用者的設定檔。
* `"in"`:當設定此設定或未提供值時，工作會在沒有使用者同意偏好的情況下進行。
* `"pending"`:設定此設定時，工作會排入佇列，直到使用者提供同意偏好為止。
* `"out"`:設定此設定時，工作會被捨棄，直到使用者提供同意偏好為止。在提供使用者的偏好設定後，工作會根據使用者的偏好進行或中止。 如需詳細資訊，請參閱[支援同意](../consent/supporting-consent.md)。

## 個人化選項

### `prehidingStyle`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 無 | 無 |

{style=&quot;table-layout:auto&quot;}

用來建立CSS樣式定義，當從伺服器載入個人化內容時，會隱藏網頁的內容區域。 如果未提供此選項，SDK在載入個人化內容時不會嘗試隱藏任何內容區域，可能會導致「閃爍」。

例如，若您網頁上的元素ID為`container`，當從伺服器載入個人化內容時，您要隱藏其預設內容，請使用下列預先隱藏樣式：

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## 觀眾選項

### `cookieDestinationsEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

{style=&quot;table-layout:auto&quot;}

啟用[!DNL Audience Manager] Cookie目標，允許根據區段限定來設定Cookie。

### `urlDestinationsEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

{style=&quot;table-layout:auto&quot;}

啟用[!DNL Audience Manager] URL目標，允許根據區段限定引發URL。

## 身分選項

### `idMigrationEnabled` {#id-migration-enabled}

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

{style=&quot;table-layout:auto&quot;}

如果為true,SDK會讀取並設定舊的AMCV Cookie。 此選項可協助轉換至使用Adobe Experience Platform網頁SDK，而網站的某些部分仍可能使用Visitor.js。 如果頁面上已定義訪客API,SDK會查詢訪客API以取得ECID。 此選項可讓您使用Adobe Experience Platform網頁SDK進行雙標籤頁面，而且仍有相同的ECID。

### `thirdPartyCookiesEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

{style=&quot;table-layout:auto&quot;}

啟用Adobe協力廠商Cookie的設定。 SDK可將訪客ID保留在協力廠商內容中，以便讓相同的訪客ID可跨網站使用。 如果您有多個網站，或想要與合作夥伴共用資料，請使用此選項；但是，有時出於隱私權原因，不需要這個選項。
