---
title: 配置Adobe Experience PlatformWeb SDK
description: 瞭解如何配置Adobe Experience PlatformWeb SDK。
seo-description: Learn how to configure the Experience Platform Web SDK
keywords: configure;configuration;SDK;edge;Web SDK;configure;edgeConfigId;context;web；設備；環境；placeContext;debugEnabled;egdeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsendw;web sdk設定；predkdk;predddkStyle;compent;cons;cons;ce;cond;cons;T;Tons;T;T;Tsts;went;Tings;wets;T;Tings;T;Cookies;D;Tewed;Web stings;Comped;DestinationsEnabled;idMigrationEnabled;thirdPartyCookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: 4d0f1b3e064bd7b24e17ff0fafb50d930b128968
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 15%

---

# 配置平台Web SDK

SDK的配置是使用 `configure` 的子菜單。

>[!IMPORTANT]
>
>`configure` 是 *總是* 第一個命令叫做。

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

在配置過程中可以設定許多選項。 所有選項都可在下面找到，按類別分組。

## 常規選項

### `edgeConfigId`

>[!NOTE]
>
>**邊緣配置已重新標籤為資料流。 資料流ID與配置ID相同。**

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 是 | None |

{style=&quot;table-layout:auto&quot;}

您分配的配置ID，它將SDK連結到相應的帳戶和配置。 在單頁內配置多個實例時，必須配置其他實例 `edgeConfigId` 例。

### `context`

| **類型** | **必填** | **預設值** |
| ---------------- | ------------ | -------------------------------------------------- |
| 字串陣列 | 無 | `["web", "device", "environment", "placeContext"]` |

{style=&quot;table-layout:auto&quot;&quot;

指示要自動收集的上下文類別（如所述） [自動資訊](../data-collection/automatic-information.md)。 如果未指定此配置，則預設使用所有類別。

### `debugEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布爾型 | 無 | `false` |

{style=&quot;table-layout:auto&quot;&quot;

指示是否啟用調試。 將此配置設定為 `true` 啟用以下功能：

| **功能** | **函數** |
| ---------------------- | ------------------ |
| 控制台日誌記錄 | 允許調試消息顯示在瀏覽器的JavaScript控制台中 |

{style=&quot;table-layout:auto&quot;&quot;

### `edgeDomain` {#edge-domain}

使用第一方域填充此欄位。 有關詳細資訊，請參閱 [文檔](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=zh-Hant)。

域類似於 `data.{customerdomain.com}` 網址為：{customerdomain.com}。

### `edgeBasePath` {#edge-base-path}

用於與Adobe服務通信和交互的edgeDomain之後的路徑。  通常，只有在不使用預設生產環境時才會更改。

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 無 | e |

{style=&quot;table-layout:auto&quot;&quot;

### `orgId`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 是 | 無 |

{style=&quot;table-layout:auto&quot;&quot;

您分配的 [!DNL Experience Cloud] 組織ID。 在頁內配置多個實例時，必須配置其他實例 `orgId` 例。

## 資料收集

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布爾型 | 無 | `true` |

{style=&quot;table-layout:auto&quot;&quot;

指示是否自動收集與連結按一下相關聯的資料。 請參閱 [自動連結跟蹤](../data-collection/track-links.md#automaticLinkTracking) 的子菜單。 如果連結包含下載屬性或連結以檔案副檔名結尾，則也會將其標籤為下載連結。 下載連結限定詞可以使用規則運算式進行配置。 預設值為 `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 函數 | 無 | （=>未定義） |

{style=&quot;table-layout:auto&quot;&quot;

配置在發送每個事件之前調用的回調。 帶欄位的對象 `xdm` 已發送到回調。 要更改發送的內容，請修改 `xdm` 的雙曲餘切值。 在回電中， `xdm` 對象已在event命令中傳遞了資料，並自動收集了資訊。 有關此回調時間的詳細資訊和示例，請參見 [全局修改事件](tracking-events.md#modifying-events-globally)。

## 隱私選項

### `defaultConsent` {#default-consent}

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 物件 | 無 | `"in"` |

{style=&quot;table-layout:auto&quot;&quot;

設定用戶的預設同意。 如果尚未為用戶保存同意首選項，則使用此設定。 其他有效值為 `"pending"` 和 `"out"`。 此預設值不會永續到用戶的配置檔案。 僅當在以下情況下才更新用戶的配置檔案 `setConsent` 。
* `"in"`:設定此設定或未提供值時，工作將在未經用戶同意首選項的情況下進行。
* `"pending"`:設定此設定後，工作將排入隊列，直到用戶提供同意首選項。
* `"out"`:設定此設定後，工作將被丟棄，直到用戶提供同意首選項。
在提供用戶的首選項後，根據用戶的首選項繼續或中止工作。 請參閱 [支援同意](../consent/supporting-consent.md) 的子菜單。

## 個性化選項

### `prehidingStyle`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 無 | 無 |

{style=&quot;table-layout:auto&quot;&quot;

用於建立CSS樣式定義，該定義在從伺服器載入個性化內容時隱藏網頁的內容區域。 如果未提供此選項，則SDK在載入個性化內容時不會嘗試隱藏任何內容區域，這可能會導致「閃爍」。

例如，如果網頁上的元素的ID為 `container`在從伺服器載入個性化內容時要隱藏其預設內容，請使用以下預隱藏樣式：

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## 受眾選項

### `cookieDestinationsEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布爾型 | 無 | `true` |

{style=&quot;table-layout:auto&quot;&quot;

啟用 [!DNL Audience Manager] cookie目標，允許根據段限定設定cookie。

### `urlDestinationsEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布爾型 | 無 | `true` |

{style=&quot;table-layout:auto&quot;&quot;

啟用 [!DNL Audience Manager] URL目標，它允許基於段限定觸發URL。

## 標識選項

### `idMigrationEnabled` {#id-migration-enabled}

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布爾型 | 無 | `true` |

{style=&quot;table-layout:auto&quot;&quot;

如果為true，則SDK讀取並設定舊的AMCV Cookie。 此選項有助於過渡到使用Adobe Experience PlatformWeb SDK，而站點的某些部分可能仍使用Visitor.js。 如果訪問者API在頁面上定義，則SDK將查詢訪問者API以獲取ECID。 此選項使您能夠使用Adobe Experience PlatformWeb SDK進行雙標籤頁面，並且仍然具有相同的ECID。

### `thirdPartyCookiesEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布爾型 | 無 | `true` |

{style=&quot;table-layout:auto&quot;&quot;

啟用Adobe第三方Cookie的設定。 SDK可以將訪問者ID保留在第三方上下文中，以使同一訪問者ID能夠跨站點使用。 如果您有多個站點，或希望與合作夥伴共用資料，請使用此選項；但是，有時出於隱私原因，不需要此選項。
